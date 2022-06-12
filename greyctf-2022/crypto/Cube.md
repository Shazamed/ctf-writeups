# Cube
## Crypto - 271 pts (51 Solves)

> I have a super computer so I can run this!

``` python
from Crypto.Util.number import bytes_to_long, getPrime, isPrime

FLAG = <REDACTED>

def gen(n):
    while True:
        p = getPrime(n - 1) * 2 + 1
        if (isPrime(p)):
            return p

def cube(m, n, p):
    res = m
    for i in range(n):
        res = (res * res * res) % p
    return res

p = gen(1024)
m = bytes_to_long(FLAG)
c = cube(m, 2 ** 100, p)

print(p)
print(c)

# p = 147271787827929374875021125075644322658199797362157810465584602627709052665153637157027284239972360505065250939071494710661089022260751215312981674288246413821920620065721158367282080824823494257083257784305248518512283466952090977840589689160607681176791401729705268519662036067738830529129470059752131312559
# c = 117161008971867369525278118431420359590253064575766275058434686951139287312472337733007748860692306037011621762414693540474268832444018133392145498303438944989809563579460392165032736630619930502524106312155019251740588974743475569686312108671045987239439227420716606411244839847197214002961245189316124796380
```

# Solution
This appears to be a RSA problem with a few twists. Which is that the modulus is prime and that the exponent is extremely huge.

Looking at the ```cube``` function, we can determine that in every loop, the value of ```res``` will be cubed. 
Since there are ```2 ** 100``` loops, the total exponent of the message, m, is equivalent to ```3 ** 2 ** 1000```.

Additionally, we can easily determine the euler totient function of ```p``` as ```p``` is prime. Giving  ```Φ(p) = p-1```.
With this we can easily obtain the private key, ```d```, by calculating e<sup>-1</sup> mod Φ(p). Where e<sup>-1</sup> is the modolar inverse of the exponent, e.

We could express the above in the following python code:
``` python
d = pow(3 ** 2 ** 100,-1,p-1)
```

However, running this as is will not give you the private key. The exponent is too large! We need to first simplify e, ```3 ** 2 ** 100```.
The equation, e<sup>-1</sup> mod Φ(p) ≡ d, can be rewritten as  (e mod p-1)<sup>-1</sup> mod p-1 ≡ d. 

We just need to calculate (e mod p-1) before calculating d:
``` python
exponent = pow(3, 2 ** 100, p-1)
d = pow(exponent,-1,p-1)
```

Now with the private key, we can obtain the plaintext message using:
c<sup>d</sup> mod p ≡ m

In python:
``` python
m = pow(c,d,p)
```
Printing m after converting it to bytes will give the plaintext message:
```grey{CubeIsSquarerThanSquare_FjUFynTNUdTyJu5x}```

# Source
``` python
from Crypto.Util.number import long_to_bytes
c = 117161008971867369525278118431420359590253064575766275058434686951139287312472337733007748860692306037011621762414693540474268832444018133392145498303438944989809563579460392165032736630619930502524106312155019251740588974743475569686312108671045987239439227420716606411244839847197214002961245189316124796380
p = 147271787827929374875021125075644322658199797362157810465584602627709052665153637157027284239972360505065250939071494710661089022260751215312981674288246413821920620065721158367282080824823494257083257784305248518512283466952090977840589689160607681176791401729705268519662036067738830529129470059752131312559

exponent = pow(3, 2 ** 100, p-1)
d = pow(exponent,-1,p-1)
m = pow(c,d,p)
print(long_to_bytes(m))
```
# Flag
```grey{CubeIsSquarerThanSquare_FjUFynTNUdTyJu5x}```
