# Notes 


## RSA

RSA - Rivest Shamir Adleman. This system has two keys - encryption and decryption. Encryption key is public but decryption key is private.

- Encrypting a message - m^e % N 
- Decrypting a message - c^d % N

How are these keys generated? - Using two prime numbers i.e., say p and q.

- N = p*q
- phi = (p-1)(q-1) -> phi is the number of numbers that are coprime with N.

`e` (public encryption key) has to satisfy two conditions -

1. 1<e<phi
2. coprime with N and phi

`d` (private decryption key) has to satisfy the condition - d*e % phi = 1

- d*e = 1 mod(phi)

## Ciphers discovered

1. RSA
2. Atbash 
3. Vigenere 
4. Substitution
5. Rail Fence 
6. Cyclical Cipher 