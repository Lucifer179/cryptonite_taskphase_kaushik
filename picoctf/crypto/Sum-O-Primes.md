## Challenge

"We have so much faith in RSA we give you not just the product of the primes, but their sum as well!"

`gen.py` - 
```
#!/usr/bin/python

from binascii import hexlify
from gmpy2 import mpz_urandomb, next_prime, random_state
import math
import os
import sys

if sys.version_info < (3, 9):
    import gmpy2
    math.gcd = gmpy2.gcd
    math.lcm = gmpy2.lcm

FLAG  = open('flag.txt').read().strip()
FLAG  = int(hexlify(FLAG.encode()), 16)
SEED  = int(hexlify(os.urandom(32)).decode(), 16)
STATE = random_state(SEED)

def get_prime(bits):
    return next_prime(mpz_urandomb(STATE, bits) | (1 << (bits - 1)))

p = get_prime(1024)
q = get_prime(1024)

x = p + q
n = p * q

e = 65537

m = math.lcm(p - 1, q - 1)
d = pow(e, -1, m)

c = pow(FLAG, e, n)

print(f'x = {x:x}')
print(f'n = {n:x}')
print(f'c = {c:x}')

```

Contents of `output.txt` -
```
x = 152a1447b61d023bebab7b1f8bc9d934c2d4b0c8ef7e211dbbcf841136d030e3c829f222cec318f6f624eb529b54bcda848f65574896d70cd6c3460d0c9064cd66e826578c2035ab63da67d069fa302227a9012422d2402f8f0d4495ef66104ebd774f341aa62f493184301debf910ab3d1e72e357a99c460370254f3dfccd9ae
n = 6fc1b2be753e8f480c8b7576f77d3063906a6a024fe954d7fd01545e8f5b6becc24d70e9a5bc034a4c00e61f8a6176feb7d35fe39c8c03617ea4552840d93aa09469716913b58df677c785cd7633d1b7d31e2222cab53be235aa412ac5c5b07b500cf3fd5d6b91e2ddc51bff1e6eec2cb68723af668df36e10e332a9cbb7f3e2df9593fa0e553ed58afec2aa3bc4ae8ef1140e4779f61bdeae4c0b46136294cf151622e83c3d71b97c815b542208baa28207225f134c5a4feac998aeb178a5552f08643717819c10e8b5ec7715696c3bf4434fbea8e8a516dfd90046a999e24a0fb10d27291eb29ef3f285149c20189e7d0190417991094948180196543b8c91
c = 16acf84a73cefd321ed491a15c640a495b09050cdce435ec37442faf9a694775e1ebffb6dbad6133cbc54e3f641506b0613f711625594fcb467f915f2708714b4c9936f5f4752c3299157cff4eb68eb82c0054dae351314829974f4feadaf126cda92b97e348dbef2640ec3a729a064e615df73d644700f93bf87579683e253d29622525bea3644f59aac8e0b2553bfea48d99e9b323e03cbf55166659974eb8c51cc7b2c2c5d6aa6c01b056a8ed7283d96656a3496f266726605af1be139d586f208d4d7c59c2771dc8036d490d3672ee4513301002775d7c39eac421c6cb4f01344e061549a4cb11c057accef1726572e447501004c772ec91b4a55811280f

```

## Solve

After converting the hex into decimals for the values in `output.txt`, I put `n` in [FactorDB](https://factordb.com/index.php?showid=1100000007583928732) and got the factors of `n` which are 'p' and 'q' which aligned with `x` which was `p+q` (since the units place digit was 0).

```
p = 113555373192500943757347200537661553211456236794837122880601113555854781406339483423434917996351857545875405098238265321751218735544249960436269109023300381364677749208091802101469817073745908605989047665985314018377915624692143738631532769850077802552967686024344490545101481143954168442661650896889584367639
q = 124238665297436351535057644565670615375443538969172645932414670332019048252346424732454374287700184761196786959193566174940923144061340753375696812236797799085284060917522754635338715470410049507726019057956507759394465391650189663615302576713255389112522546651929487111766739718243933329068430413385177473431
```

From here, I put the values of e, d, n, p and q along with ciphertext c in my custom decryption program -
```
from Crypto.Util.number import inverse, long_to_bytes

c = 2862537339040469147429657894344199928557031834390107583219729603518151458232752655435765178741847862681985518014369908230465656681188452816388220057841477741951807370846472046013718654924186479831297315008200827303965506316115312185032136602875438400387736740902196374239905780326853099910635897462206320968355042526152404835351422548524752308082386282793614300087991456840160462341088790668081742054292524665828459909511307682427456625705560299547231552417332610842874439163798240180613567066151575717456490027272337259628798278336279800627826934011806508731399100283618512809664315701708126217489999299504239618063
n = 14107968002788601163232271919683185628377930258855714024361251700443482916159477972019175057249307805020558833578002642814353244251935462643122106832841875886751834868578847553067993029534859873400111872030760141512265217100084094768240561746973517000260205166788073707007901559501857058570047904411103289205303895005723927634856272992046301957255183083869294681094092965797803167854696071500371486827898745037887826839037430790364261755123274123835361705705618196178336329858713462923973567226715396383555224515182961278023099436837662748725809380387313268345922304316857780150905037767522499166165808213903858699409
e = 65537
p = 113555373192500943757347200537661553211456236794837122880601113555854781406339483423434917996351857545875405098238265321751218735544249960436269109023300381364677749208091802101469817073745908605989047665985314018377915624692143738631532769850077802552967686024344490545101481143954168442661650896889584367639
q = 124238665297436351535057644565670615375443538969172645932414670332019048252346424732454374287700184761196786959193566174940923144061340753375696812236797799085284060917522754635338715470410049507726019057956507759394465391650189663615302576713255389112522546651929487111766739718243933329068430413385177473431

phi = (p-1)*(q-1)

d = inverse(e, phi)

m = pow(c, d, n)

print(long_to_bytes(m))
```
and got the flag.

## Flag

`picoCTF{pl33z_n0_g1v3_c0ngru3nc3_0f_5qu4r35_3921def5}`