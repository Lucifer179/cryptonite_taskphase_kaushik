## Challenge
"How about we take you on an adventure on exploring certificate signing requests

Take a look at this csr file here."

The contents of the csr file were - 
```
-----BEGIN CERTIFICATE REQUEST-----
MIICpzCCAY8CAQAwPDEmMCQGA1UEAwwdcGljb0NURntyZWFkX215Y2VydF82OTNm
N2MwM30xEjAQBgNVBCkMCWN0ZlBsYXllcjCCASIwDQYJKoZIhvcNAQEBBQADggEP
ADCCAQoCggEBAPp+XuDB3ZkmrkvAsgtjP+mjIcYDWfptuZsJieu6eRl39wl4Sg38
+/OfY24LV9sNmgKyTGvpmCaUoZMYkvkulYSoFzE0xqPBo6kruLEyIvqqpAFqRH2b
mierLT6RcKgJHYr/Vt6SwP8NCCawCrvhQ4NZcuB49Hr/2AiGHzmf86/lG/c+lhmH
gyqPb1kDghsVxi/GNs9i7AgniZikqT8OTp0INmmCgZtJn1Jo615Iu/tFiC8Sfhhg
QHmTDLjgx1oP1kvZV2PE5UUN/oC05Zup8f31LksXZwpazZKwYC/LbN96HdqgVQ9K
S8e/4I7MJQmPmLIsLp3sdL2FiDGML3smAi0CAwEAAaAmMCQGCSqGSIb3DQEJDjEX
MBUwEwYDVR0lBAwwCgYIKwYBBQUHAwIwDQYJKoZIhvcNAQELBQADggEBAOxSR8Fs
Tdjfu9e0vRNqKWd09ISmYDQc3qnSbLRlYZyMK4pguALq310h/1nNgURWESbNJPOp
FkBWG0XWhWyWP7rTqxo/pk9AKx0TNbHDrS6KiBnKPq0mxjPZsH1L7wNYDc5OANDl
btvn3zT7lMms6z1qM7xUWXR76n2xL/81cdF725nBZ00mWmPW0S1pSmA4EEHCEgNW
0vWQqsIDki3gYc4NCm8OHjx79kcwE+ksyc6vHgMOwsYoOFJnyayhl15oN/3x7hW3
G1xovPupABpfOSNOcTwbgfrfjUDOLx/wirvj9L1N5EGDh4FOLaRZDs+tMrimGBBS
zGU13BnykmQ5jOQ=
-----END CERTIFICATE REQUEST-----

```

A CSR file stands for Certificate Signing Request and is encrypted in RSA and follows the "PKCS #10 standard" for doing so.

## Solve

After googling a little bit about the CSR file, I found that the public key should be built into the CSR file itself and the private key should be a separate file that we end up installing but obviously we had only one file so I began looking into how I can figure out the private key.

That's when I found [this website](https://www.ssls.com/knowledgebase/how-can-i-find-the-private-key-for-my-ssl-certificate/). Under the cPanel section of it, in the SSL/TLS Manager subsection, I found an SSL and CSR decoder tool. I pasted the contents of the CSR file in it and found the flag under the "Common Name" of the request.

![](2024-12-30-01-55-04.png)

Initially, I was going down the rabbit hole of `openssl` and how the key is generated to find out how to get the key to decrypt the file but it would seem I didn't have to do that anyway.

## Flag

`picoCTF{read_mycert_693f7c03} `