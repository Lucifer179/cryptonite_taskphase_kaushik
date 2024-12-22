## Challenge

"Can you get sense of this code file and write the function that will decode the given encrypted file content. Find the encrypted file here flag_info and code file might be good to analyze and get the flag."

Contents of `enc_flag` - 
```
a = 94
b = 21
cipher is: [131553, 993956, 964722, 1359381, 43851, 1169360, 950105, 321574, 1081658, 613914, 0, 1213211, 306957, 73085, 993956, 0, 321574, 1257062, 14617, 906254, 350808, 394659, 87702, 87702, 248489, 87702, 380042, 745467, 467744, 716233, 380042, 102319, 175404, 248489]
```

## Analyzing the source code

There are two levels of encryption done on the flag - XOR encryption and Diffie-Hellman key exchange.

**XOR encryption -** 
```
def dynamic_xor_encrypt(plaintext, text_key):
    cipher_text = ""
    key_length = len(text_key)
    for i, char in enumerate(plaintext[::-1]):
        key_char = text_key[i % key_length]
        encrypted_char = chr(ord(char) ^ ord(key_char))
        cipher_text += encrypted_char
    return cipher_text
```
The `plaintext` is reversed by `plaintext[::-1]`, the XOR function is done on each character's ASCII code with its `text_key`.

**Diffie-Hellman key exchange -** 
```
def test(plain_text, text_key):
    p = 97
    g = 31
    if not is_prime(p) and not is_prime(g):
        print("Enter prime numbers")
        return
    a = randint(p-10, p)
    b = randint(g-10, g)
    print(f"a = {a}")
    print(f"b = {b}")
    u = generator(g, a, p)
    v = generator(g, b, p)
    key = generator(v, a, p)
    b_key = generator(u, b, p)
    shared_key = None
    if key == b_key:
        shared_key = key
    else:
        print("Invalid key")
        return
    semi_cipher = dynamic_xor_encrypt(plain_text, text_key)
    cipher = encrypt(semi_cipher, shared_key)
    print(f'cipher is: {cipher}')
```
Random integers `a` and `b` are generated based on the public parameters `p` and `g`. These are the private parameters. Based on these, the public keys (u and v) are generated. After this, the shared secret is made - `key` and `b_key`. If `key` and `b_key` are the same then the shared key is equal to the key. This shared key is then used for the encryption - `cipher = encrypt(semi_cipher, shared_key)`.

## Solve

For the `encrypt` function, I wrote the following `decrypt` code - 
```
def decrypt (cipher, key):
    plaintext = ""
    for encrypted_char in cipher:
        plaintext.append(((ord(encrypted_char) // (key*311))))
    return plaintext
```

Initially, for the `dynamic_xor_encrypt` function, I wrote the following `xor_decrypt` code -
```
def xor_decrypt(cipher_text, text_key):
    decrypted_text = ""
    key_length = len(text_key)
    for i, enc_char in enumerate(cipher_text[::-1]):
        key_char = text_key[i % key_length]
        decrypted_char = chr(ord(enc_char)^(1/ord(key_char)))
        decrypted_text += decrypted_char 
    return decrypted_text
```
so as to take the root as we take it to the power in the encryption process. However, this showed me an error when I ran the program. I spent a lot of time trying to figure out why this was since if say $ enc = num^{key} $ then $ num = enc^{1/key} $. Eventually, I just tried it with the power of it directly, which gave me a closer result - `e~r~TAFntdbczmJs#re%pa!uN/w4$q(&!h`. This still wasn't the flag in any way though so I went back to the drawing board to figure out what caused it to be that way. I removed the `[::-1]` part and that gave me the reversed flag. I left it in there hoping it would just reverse the flag and give it to me directly but it would seem it isn't that simple so I just reversed it myself.

Finally, the full `custom_decryption.py` code was 
```
from random import randint
import sys


def generator(g, x, p):
    return pow(g, x) % p # g^x mod p


def decrypt (cipher, key):
    decrypted_text = ""
    for encrypted_num in cipher:
        decrypted_num = encrypted_num // (key*311)
        decrypted_text += chr(decrypted_num)
    return decrypted_text

def xor_decrypt(cipher_text, text_key):
    decrypted_text = ""
    key_length = len(text_key)
    for i, enc_char in enumerate(cipher_text):
        key_char = text_key[i % key_length]
        decrypted_char = chr(ord(enc_char)^(ord(key_char)))
        decrypted_text += decrypted_char 
    return decrypted_text

a = 94
b = 21
p = 97
g = 31
cipher = [131553, 993956, 964722, 1359381, 43851, 1169360, 950105, 321574, 1081658, 613914, 0, 1213211, 306957, 73085, 993956, 0, 321574, 1257062, 14617, 906254, 350808, 394659, 87702, 87702, 248489, 87702, 380042, 745467, 467744, 716233, 380042, 102319, 175404, 248489]
    
u = generator(g, a, p)
v = generator(g, b, p)
shared_key = generator(v,a,p)
cipher_text = decrypt(cipher, shared_key)
print(xor_decrypt(cipher_text, "trudeau"))
```

## Flag
The output from the program was `}679f14b8_d6tp0rc2d_motsuc{FTCocip` which when reversed gave the flag - `picoCTF{custom_d2cr0pt6d_8b41f976}`.