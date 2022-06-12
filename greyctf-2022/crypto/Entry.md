# Entry

## Crypto - 50 pts (184 Solves)

Entry task for crypto

``` python
import secrets

FLAG = b'grey{...}'

assert len(FLAG) == 40

key = secrets.token_bytes(4)

def encrypt(m):
    return bytes([x ^ y for x, y in zip(m,key)])

c = b''
for i in range(0, len(FLAG), 4):
    c += encrypt(bytes(FLAG[i : i + 4]))

print(c.hex())

# 982e47b0840b47a59c334facab3376a19a1b50ac861f43bdbc2e5bb98b3375a68d3046e8de7d03b4
```

# Solution

We should try to understand what the script is doing first. It first checks that the flag is of length 40, and then generates a random key of 4 bytes. Next, every group of 4 characters of the flag is passed into the `encrypt` function.

In the `encrypt` function, the following happens:

1. Pairs each character of the input string `m` and each character of the `key`, i.e. m[0] with key[0], m[1] with key[1] etc.
2. Takes the `xor` of the two in each pair, so m[0] ^ key[0]
3. Returns the bytes of the `xor` of all 4 pairs

Now we can attempt to reverse the encryption. First of all, since the key is randomly generated, we need to try to get the key from the original output string we are given. Fortunately, we know the first 4 characters of the flag, it is none other than `grey`!

One very useful property of the `xor` operation is: if `a ^ b = c`, then `a ^ c = b` and `b ^ c = a`. In other words, `bytes('grey') ^ key = bytes(output)`, thus to find the key we can take `bytes('grey') ^ bytes(output) = key`.

To do so, we can essentially reuse the `encrypt` function, inputting into encrypt the first 4 bytes of the output string `982e47b0` (1 byte is represented by 2 hex digits, so we take the first 4 characters of the hex string):

``` python
key = b'grey'

def encrypt(m):
    return bytes([x ^ y for x, y in zip(m,key)])

grey_bytes = bytearray.fromhex("982e47b0")
key = encrypt(grey_bytes)
```

Once we have run it through the `encrypt` function, we set the key variable back to the actual key. Now we can pretty much get back the original flag, recycling pretty much all of the original code:

``` python
FLAG = bytearray.fromhex("982e47b0840b47a59c334facab3376a19a1b50ac861f43bdbc2e5bb98b3375a68d3046e8de7d03b4")

c = b''
for i in range(0, len(FLAG), 4):
    c += encrypt(bytes(FLAG[i : i + 4]))

print(c)
```

Running this will print out the flag `grey{WelcomeToTheGreyCatCryptoWorld!!!!}`.

# Source

``` python
key = b'grey'

def encrypt(m):
    return bytes([x ^ y for x, y in zip(m,key)])

grey_bytes = bytearray.fromhex("982e47b0")
key = encrypt(grey_bytes)

FLAG = bytearray.fromhex("982e47b0840b47a59c334facab3376a19a1b50ac861f43bdbc2e5bb98b3375a68d3046e8de7d03b4")

c = b''
for i in range(0, len(FLAG), 4):
    c += encrypt(bytes(FLAG[i : i + 4]))

print(c)
```

# Flag

`grey{WelcomeToTheGreyCatCryptoWorld!!!!}`