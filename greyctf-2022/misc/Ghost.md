# Ghost

## Misc - 50 pts (132 Solves)

I tried to send you a bunch of messages :)

```
I got message for you:

NTQgNjggNjkgNzMgMjAgNjkgNzMgMjAgNmUgNmYgNzQgMjAgNjkgNzQgMjAgNmQgNjEgNmUgMmMgMjAgNzQgNzIgNzkgMjAgNjggNjEgNzIgNjQgNjUgNzIgMjE=

++++++++++[>+>+++>+++++++>++++++++++<<<<-]>>>++++++++++++++.>++++.+.++++++++++.<<++.>>----------.++++++++++.<<.>>----------.+++++++++++.<---------------------.<.>>------.-------------.+++++++.

pi pi pi pi pi pi pi pi pi pi pika pipi pi pipi pi pi pi pipi pi pi pi pi pi pi pi pipi pi pi pi pi pi pi pi pi pi pi pichu pichu pichu pichu ka chu pipi pipi pipi pipi pi pi pi pi pi pi pi pi pikachu pi pi pi pikachu ka ka ka pikachu pichu pichu pi pi pikachu pipi pipi pi pi pikachu pi pikachu
 		  			 			  	  		  	 	 				  	 				 		 		  			 		 	     		     			  		  		 			 	 					 		   	  				  	 			 	    		  		  	  	   	 					 		 			   		     			 	   	 					  		   	 		 			  			 		  		 	  	 			  		 	  	  	 		   	  		 		    		  		 					 	
KRUGS4ZANFZSA3TPOQQHI2DFEBTGYYLHEBWWC3RAIQ5A====

synt{abgGungFvzcyr:C}

Me: Message received.
```

# Solution

We are presented with a list of messages, and we can try to decode each message.

The first line, `NTQgNjggNjkgNzMgMjAgNjkgNzMgMjAgNmUgNmYgNzQgMjAgNjkgNzQgMjAgNmQgNjEgNmUgMmMgMjAgNzQgNzIgNzkgMjAgNjggNjEgNzIgNjQgNjUgNzIgMjE=`, is encoded in Base64. Decoding it returns `This is not it man, try harder!`. sadge

The second line, consisting of `+`, `[`, `>` etc., is quite clearly [brainfuck](https://esolangs.org/wiki/Brainfuck). Putting it through a decoder gives `This is it? nah`. pepehands

The third line, with the `pi` and the `ka` and the `pika`, is yet another esolang, Pikalang, which is pretty much identical to Brainfuck. Intepreting this results in `lol no`. widepeeposad

We go to the fourth line but discover that there is a bunch of whitespace between the `pika` and the `KRUG`. We can try to decode this and find that there are 2 kinds of whitespace, the space `0x20` and the tab `0x09`. Playing around we discover that we can treat it as binary by replacing the spaces with 0s and the tabs with 1:

``` python
def decode(s):
    new_s = ""
    for i in range(0, len(s)):
        if i and i % 8 == 0:
            new_s += " "
        if s[i] == ' ':
            new_s += "0"
        else:
            new_s += "1"
    print(new_s)
```

which gives `01100111 01110010 01100101 01111001 01111011 01100111 01101000 00110000 01110011 00110111 01011111 01100010 01111001 01110100 00110011 00100100 01011111 01101110 00110000 01110100 01011111 00110001 01101110 01110110 01101001 01110011 01001001 01100010 01101100 00110011 01111101`

Putting this through a decoder gives us `grey{gh0s7_byt3$_n0t_1nvisIbl3}`

btw, the next lines decode to:

KRUGS4ZANFZSA3TPOQQHI2DFEBTGYYLHEBWWC3RAIQ5A==== 
> (Base32) `This is not the flag man D:`

synt{abgGungFvzcyr:C}
> (rot13) `flag{notThatSimple:P}`

# Flag

`grey{gh0s7_byt3$_n0t_1nvisIbl3}`