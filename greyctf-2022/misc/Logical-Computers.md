# Logical Computers
## Misc - 456 pts (23 Solves)
> Teaching computers is like teaching children, you gotta start simple.
> Today I taught it to recognize the flag!

In this challenge, we are given a chall.py file, and a model.pth file which contains the weights of the trained model.

Looking at chall.py:

```python
import torch

def tensorize(s : str) -> torch.Tensor:
  return torch.Tensor([(1 if (ch >> i) & 1 == 1 else -1) for ch in list(map(ord, s)) for i in range(8)])

class NeuralNetwork(torch.nn.Module):
  def __init__(self, in_dimension, mid_dimension, out_dimension=1):
    super(NeuralNetwork, self).__init__()
    self.layer1 = torch.nn.Linear(in_dimension, mid_dimension)
    self.layer2 = torch.nn.Linear(mid_dimension, out_dimension)

  def step_activation(self, x : torch.Tensor) -> torch.Tensor:
    x[x <= 0] = -1
    x[x >  0] = 1
    return x

  def forward(self, x : torch.Tensor) -> int:
    x = self.layer1(x)
    x = self.step_activation(x)
    x = self.layer2(x)
    x = self.step_activation(x)
    return int(x)

flag = input("Enter flag: ")
in_data = tensorize(flag)
in_dim	= len(in_data)

model = NeuralNetwork(in_dim, 1280)
model.load_state_dict(torch.load("model.pth"))

if model(in_data) == 1:
	print("Yay correct! That's the flag!")
else:
	print("Awww no...")
  ```


We can tell that the model has 3 layers of in_dim, 1280, and 1 node(s) respectively.

Running the program and entering any input not 20 chars long will give an error containing:
> size mismatch for layer1.weight: copying a param with shape torch.Size([1280, 160]) from checkpoint

Which tells us that the in_dim must be of size 160.

Then looking at the tensorise function:
```python
def tensorize(s : str) -> torch.Tensor:
  return torch.Tensor([(1 if (ch >> i) & 1 == 1 else -1) for ch in list(map(ord, s)) for i in range(8)])
```
Basically it is equivalent to iterating over each char in the input string, converting them into binary, changing all zeros to -1 and then reversing the order of the bits before adding each bit to the weight.

From this, we now know that the input string must be 20 chars long.

In a neural network, each node in a layer will have the same number of weights as the number of nodes in the next layer.

So, layer1 has a size of [1280, 160] and layer2 has a size of [1, 1280]

Knowing this, we simply just obtained the weights from each layer in the trained model and matrix multiplied them together to get a matrix of size 160

```python
weights1 = model.layer1.weight.data
weights2 = model.layer2.weight.data
np_weights1 = weights1.numpy()
np_weights2 = weights2.numpy()

matrix_mult = np.matmul(np_weights2,np_weights1)
print(matrix_mult)
```
The first 8 elements of the matrix gives:
``` 253. 240. 224. -16. -16. 234. 239. -13.```

Printing and looking at the resultant matrix, we noticed that the each element is either greater than 200 or smaller than 0. So we decided to convert each positive result to 1 and each negetive result to 0.

``` python
binary_str = ""
for idx, i in enumerate(matrix_list):
  if idx % 8 == 0 and idx != 0:
    binary_str += " "
  if i > 0:
    binary_str += "1"
  else:
    binary_str += "0"

binary_str = binary_str.split(" ")
binary_list = [chr(int(binary[::-1], 2)) for binary in binary_str]
print("".join(binary_list))
```

Running the above gives the flag:
```grey{sM0rT_mAch1nE5}```

## Source 
``` python
import torch
import numpy as np

def tensorize(s : str) -> torch.Tensor:
  return torch.Tensor([(1 if (ch >> i) & 1 == 1 else -1) for ch in list(map(ord, s)) for i in range(8)])

class NeuralNetwork(torch.nn.Module):
  def __init__(self, in_dimension, mid_dimension, out_dimension=1):
    super(NeuralNetwork, self).__init__()
    self.layer1 = torch.nn.Linear(in_dimension, mid_dimension)
    self.layer2 = torch.nn.Linear(mid_dimension, out_dimension)

  def step_activation(self, x : torch.Tensor) -> torch.Tensor:
    x[x <= 0] = -1
    x[x >  0] = 1
    return x

  def forward(self, x : torch.Tensor) -> int:
    x = self.layer1(x)
    x = self.step_activation(x)
    x = self.layer2(x)
    x = self.step_activation(x)
    return int(x)

model = NeuralNetwork(160, 1280)
model.load_state_dict(torch.load("model.pth"))

weights1 = model.layer1.weight.data
weights2 = model.layer2.weight.data
np_weights1 = weights1.numpy()
np_weights2 = weights2.numpy()

matrix_mult = np.matmul(np_weights2,np_weights1)
matrix_list = np.ndarray.tolist(matrix_mult)[0]

binary_str = ""
for idx, i in enumerate(matrix_list):
  if idx % 8 == 0 and idx != 0:
    binary_str += " "
  if i > 0:
    binary_str += "1"
  else:
    binary_str += "0"

binary_str = binary_str.split(" ")
binary_list = [chr(int(binary[::-1],2)) for binary in binary_str]
print("".join(binary_list))
```
