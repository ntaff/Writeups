# Misc - Randomito - 25 pts - 292 solves

First challenge of `Misc` category

Here's the code given in `randomito.py` :

We clearly see that the server generate two "random" numbers `secret_a` and `secret_b`, and ask the user to guess them.

```Python
#!/usr/local/bin/python2

import sys
import signal
from random import randint

# Time allowed to answer (seconds)
DELAY = 10

def handler(signum, frame):
   raise Exception("Time is up!\n")

def p(s):
	sys.stdout.write(s)
	sys.stdout.flush()

def challenge():

	for _ in range(10):
		p("[+] Generating a 128-bit random secret (a, b)\n")
		secret_a = randint(0, 2**64 - 1)
		secret_b = randint(0, 2**64 - 1)
		secret   = "{:016x}{:016x}".format(secret_a, secret_b)
		p("[+] Done! Now, try go guess it!\n")
		p(">>> a = ")
		a = int(input())
		p(">>> b = ")
		b = int(input())
		check = "{:016x}{:016x}".format(a, b)
		p("[-] Trying {}\n".format(check))
		if check == secret:
			flag = open("flag.txt").read()
			p("[+] Well done! Here is the flag: {}\n".format(flag))
			break
		else:
			p("[!] Nope, it started by {}. Please try again.\n".format(secret[:5]))

if __name__ == "__main__":
	signal.alarm(DELAY)
	signal.signal(signal.SIGALRM, handler)
	try:
		challenge()
	except Exception, e: 
		exit(0)
	else:
		exit(0)
 ```
 
 You have first to note that we are in `Misc` category, not `Crypto` one. The hint is here. No need to pwn the prng :flushed:. 
 After some minutes of reflexion, I'll just try to enter `secret_a` and `secret_b` as inputs. And guess what ? IT WORKS ! :flushed:
 
 !["flag!"](https://github.com/ntaff/Writeups/blob/master/assets/images/FCSC%202020/randomito1.png)
 
 (In french, `randomito` is a contractions of words "random" and "mytho" (who mean "liar"))
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
