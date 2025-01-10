## Challenge

"We found this file. Recover the flag."

## The file

The file is a bmp file that doesn't display the image. When I checked it with `file tunn3l_v1s10n`, I saw that it has data in it. I looked at it in a text editor and found a lot of gibberish. To pull out some meaningful data, I piped the strings in it into another file and tried to analyze and decipher it with base64 and shift cipher which didn't work. I spent a long time trying to figure out what else I could do. I tried using objdump but that didn't work cause that's generally used if it has executable binary data, which this didn't.

Then I remembered that the reason for the image not showing up was that the header had an error, so there must be something I could do to fix that. I tried using exiftool to find the header size but it wasn't displaying that so to that end, I ran a python program drawn up by chatgpt that'll do it for me. I found that the DIB header size is 53434 bytes. To find the size of the header in the file, I needed to look at its hex.

## The hex

I dumped the hex code of the bmp file into another file and started analyzing it. After a lot of research and harassing chatgpt, I found that the header size is too small and that the pixel array offset may be too small or too large which can cause the image to not load. 

The pixel array offset values in the hex code didn't match with the correct value. It has to be equal to 14 + the DIB Header size which was 53434 = 53448.

My hex values: `424d 8e26 2c00 0000 0000 bad0 0000` where `BA D0 00 00` reflects the header size. BAD0 is 47824 so I had to change that to reflect 53448 which was D0C8 in hex. 

Therefore, the corrected values were: `424d 8e26 2c00 0000 0000 d0c8 0000`. To put in these values in the file I needed a hex editor that could directly modify the file. I tried using vim but it just converted the bmp file into a blob of hex. So I looked into other editors and found 'Bless'. I used it to fix the hex and the bmp file remained bmp. 

However, this didn't fix the problem. The image still wasn't loading, so I looked into what else could be the reason for that. I found that it could be because the DIB header size isn't correct, whose information is in bytes 14-17 - `BA D0 00 00`. It has to be 40 bytes long, so I replaced it with `28 00 00 00`. 

_Ah, now it's finally visible._ But the only part I can see is "notaflag{sorry}". The image seemed cropped, so I decided to play around with the width and length of it to see if that would uncover the actual flag. The information for the width and length lied in bytes 18-21 and 22-25 respectively. 

## Flag

After accidentally changing the values too much and opening the file to see an abomination of my own creation, I finally managed to come to a sweet spot with the values `6E 04 00 00 32 0A 00 00` and got the final flag - `picoCTF{qu1t3_a_v13w_2020}`.
