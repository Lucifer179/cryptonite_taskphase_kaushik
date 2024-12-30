## Challenge

"In RSA, a small e value can be problematic, but what about N? Can you decrypt this?"

Contents of `values` - 
```
Decrypt my super sick RSA:
c: 964354128913912393938480857590969826308054462950561875638492039363373779803642185
n: 1584586296183412107468474423529992275940096154074798537916936609523894209759157543
e: 65537
```

## Solve

`n` is the result of multiplication of two random prime numbers (say p and q) and phi is `(p-1)*(q-1)`. We need the value of `d` to decrypt the message which can be found from the following relation - `d*e mod phi = 1`, so to get d I have to take the modular inverse of e and phi. 

In order to get the values of p and q, I needed to factorize `n`. In my search for a good factorization website for RSA challenges, I finally found `Factor db`. Using that, I got the values of p and q mentioned in the code.

I made the following program to carry out these calculations -

```
from Crypto.Util.number import inverse, long_to_bytes

c = 964354128913912393938480857590969826308054462950561875638492039363373779803642185
n = 1584586296183412107468474423529992275940096154074798537916936609523894209759157543
e = 65537
p = 2434792384523484381583634042478415057961
q = 650809615742055581459820253356987396346063

phi = (p-1)*(q-1)

d = inverse(e, phi)

m = pow(c, d, n)

print(long_to_bytes(m))
```

## Flag

`picoCTF{sma11_N_n0_g0od_73918962}`