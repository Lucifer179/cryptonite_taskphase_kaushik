## Challenge
"How about some hide and seek heh?"
Hints: Download the image and try to extract it.

## Solve

My first assumption was that there's some form of steganography done to the image so I have to extract the password which would be encrypted in atbash cipher. I started trying to crack away at it with `steghide`, guessing the password each time with whatever may work (like "HideToSee", "AtbashCipher", etc.).

When that didn't work, I looked into more details of the image with `exiftool` and found that it has `Baseline DCT, Huffman coding` encryption. I started extracting raw binary and hex data to see if I can decode the Huffman coding encryption in it to get some information. I tried that for a while and then decided to try out steghide for a while again. I accidentally didn't put in a passphrase one time and it gave me the flag encrypted in atbash cipher. Turns out no passphrase is also an option that I was not aware of.

## Flag

Steghide output - `krxlXGU{zgyzhs_xizxp_zx751vx6}`

Atbabsh decoded - `picoCTF{atbash_crack_ac751ec6}`