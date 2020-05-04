# Reverse - Infiltrate - 25 pts - 188 solves

First challenge of `reverse` category ! Here we just have an image at our disposal : 

!["Challenge image"](https://github.com/ntaff/Writeups/blob/master/assets/images/FCSC%202020/infiltrate.png)

We clearly see that there are two colors on the image : black and white. Let's decode it as bytes !


We print the first 20 first bytes and we notice that it must be a binary file hidden in the image (because of the `ELF`) :
`b'\x04Q\x81\x91UP\x89\xd5\xc0\xe4M=j\xe7\x1d\xed\x7fELF\x02\x01\x01\x00\x00\x00\x00\x00\x00`

We also notice the first 16 bytes garbage, that we can remove. Here's the final code (just need to install PIL with `pip3 install PIL`) :

```Python
from PIL import Image

i = Image.open("infiltrate.png", "r")
pix_val = list(i.getdata())
tab = ''
for j in range(len(pix_val)):
	if pix_val[j] == (255,255,255):
		tab = tab+'1'
	else:
		tab = tab+'0'

f = open("infiltrate.bin","wb")
binaries = int(tab,2).to_bytes((len(tab) + 7) // 8, 'big')
binaries = binaries[16:]
f.write(binaries)
f.close()
```

Now, we have a ELF to examinate. I will use IDA Pro, but you can use another reverse tool like Ghidra or R2 :


!["IDA1"](https://github.com/ntaff/Writeups/blob/master/assets/images/FCSC%202020/infiltrate2.png)

When we take a look at the `main` function, we see that the program display a message "Hello ! Entrez la clé" (Hello ! Enter the key).
Next, he call `fgets`, and then `doit`, which is not a standard function. Let's see what it do :

It seems that the function compare the SHA-1 hash of the key to the hash of what the user input (`a1` here). 
Here, the characters are ASCII-encoded, but we can retrieved them in the graph view. Notice that the comparison is disordered. 
The for loop is totally useless.

!["IDA2"](https://github.com/ntaff/Writeups/blob/master/assets/images/FCSC%202020/infiltrate3.png)

Finally, we retrieve the key hash, `5823DB976801C4A0E2D7A330B2BB82FE27CC2612`.
Now, just reverse it to get the [flag](https://sha1.gromweb.com/?hash=5823DB976801C4A0E2D7A330B2BB82FE27CC2612) 
