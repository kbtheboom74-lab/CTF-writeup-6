# CTF-writeup-6
CTF Writeup: Mind your Ps and Qs The name's a pretty big hint here — this is about the two prime numbers, p and q, that make up an RSA key.




How I Approached It
Got handed the usual RSA stuff: ciphertext c, modulus n, and exponent e. With a title like "Mind your Ps and Qs," it was obvious the weakness was in how n was generated, not in e.

What Was Actually Going On
Took a look at n and it turned out to be way smaller than a real, secure RSA modulus should ever be — small enough to actually factor. That's the whole point of RSA security: n is supposed to be basically impossible to factor. Not here.

How I Solved It
Ran n through a factoring tool (there's online factor databases, or you can just script Pollard's rho) and got p and q back pretty quickly. From there it's textbook RSA: compute φ(n) = (p-1)(q-1), get the private key d as the modular inverse of e, then decrypt with m = c^d mod n. Converted that number back into text and there was the flag (had to reverse the string in my case, but that's a minor detail).

What I Took Away From It
RSA lives and dies by how good your primes are. If n can be factored, the whole scheme falls apart instantly no matter what exponent you picked — factoring n basically hands you the private key.
