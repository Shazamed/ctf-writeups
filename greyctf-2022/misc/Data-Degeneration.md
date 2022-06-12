# Data Degeneration
## Misc - 388 pts (36 solves)

>Generating data is ez but recovering is >< I lost the mean I used to generate it, can you find the most probable one for me? #bigdata #helpmepliz


# Solution

We are given Chall.py

```python
import numpy as np
import random as r
from math import sqrt
import time

r.seed(time.time())

def rand(start, end) -> float:
  return r.random() * (end - start) + start

count = 3
interval = [-30, 30]

means = [rand(*interval) for _ in range(count)]
variance = 1
std_dev = round(sqrt(variance))

def sample(mu, sigma):
    return np.random.normal(mu, sigma)

points = []
for _ in range(800):
    mean = means[r.randint(0, len(means)-1)]
    points.append(sample(mean, std_dev))

with open("data.txt", "w") as f:
    inter = list(map(str,interval))
    ps = list(map(str, points))

    f.write(", ".join(ps))
```

From this, it tells us that 3 means are generated within the range of -30 to 30.

The means are then used to generate multiple samples from a normal distribution with the same mean and standard deviation of 1.

Our first step is to visualise the numbers in a histogram graph using matplotlib.

``` python
import matplotlib.pyplot as plt

with open("data.txt", "r") as f:
    input_data = f.read()

number_list = input_data.split(", ")
number_list = [float(n) for n in number_list]

plt.hist(number_list, bins=150)
plt.show()
```
Running the above code gives the figure:

![data histogram](misc/Data-Degeneration/data-hist.png)

This shows 3 distinct normal distrubution curves.

Knowing this we can just simply seperate the numbers into 3 distinct groups and find the mean of each group to obtain the 3 means.

```python
group0 = []
group1 = []
group2 = []
for n in number_list:
    if n < -8:
        group0.append(n)
    elif -3 < n < 8:
        group1.append(n)
    else:
        group2.append(n)

print(sum(group0)/len(group0))
print(sum(group1)/len(group1))
print(sum(group2)/len(group2))
```
Running the above code prints:
```
-12.338427064508242
1.957759288444758
15.138693435527586
```

Now we just need to connect to the remote connection and input our 3 means to obtain our flag:
```
Here is your flag: grey{3m_iS_bL4cK_mAg1C}
```

# Source
``` python
import matplotlib.pyplot as plt

with open("data.txt", "r") as f:
    input_data = f.read()

number_list = input_data.split(", ")
number_list = [float(n) for n in number_list]

plt.hist(number_list, bins=150)
plt.show()

group0 = []
group1 = []
group2 = []
for n in number_list:
    if n < -8:
        group0.append(n)
    elif -3 < n < 8:
        group1.append(n)
    else:
        group2.append(n)

print(sum(group0)/len(group0))
print(sum(group1)/len(group1))
print(sum(group2)/len(group2))
```

# Flag
```
grey{3m_iS_bL4cK_mAg1C}
```
