## Challenge

"Every file gets a flag. 

The SOC analyst saw one image been sent back and forth between two people. They decided to investigate and found out that there was more than what meets the eye here."

## Solve

The png file given had just "picoCTF" written on it so I dug deeper. Using `exiftool` on it didn't really give me any information. I thought this could be a case of steganography so I tried using `steghide` but it didn't accept png format so I converted it to jpg and tried it with multiple keywords but that didn't work. 

I decided to put steganography aside for a while to see if I could find anything by doing the regular inspection methods. I ran `strings hideme.png` on it and found a hint - "secret/flag.pngUT". It's possible that there are more files inside this png. I used `binwalk` on it and indeed there were multiple files embedded in it.
```
DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 512 x 504, 8-bit/color RGBA, non-interlaced
41            0x29            Zlib compressed data, compressed
39739         0x9B3B          Zip archive data, at least v1.0 to extract, name: secret/
39804         0x9B7C          Zip archive data, at least v2.0 to extract, compressed size: 2997, uncompressed size: 3152, name: secret/flag.png
43036         0xA81C          End of Zip archive, footer length: 22

```

I used `binwalk -e hideme.png` and got the files, went into the `secret` folder and looked at `flag.png` to get the final flag.

## Flag

`picoCTF{Hiddinng_An_Imag3_within_@n_ima9e_85e04ab8}`