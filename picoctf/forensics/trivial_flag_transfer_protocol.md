## Challenge

"Figure out where they moved the flag."

Provided was a `.pcapng` file which after a quick google search I found out stores packet records with timestamps, length and data for each captured packet. 

## tftp.pcapng

Opening the file with Wireshark, I found an overwhelming amount of logs so I started going through it to find anything out of the ordinary. Most of them were TFTP logs (Trivial File Transfer Protocol) which made requests to the following files - `instructions.txt`, `picture1.bmp`, `picture2.bmp`, and `picture3.bmp`. 

I wanted to find a way to view these files. After realizing I could extract them, I opened the window where I could do that and found two extra files - `plan` and `program.deb`. 

## Plan and Instructions

These files were just (seemingly) gibberish so I put it into a cipher detector and tried the first few options that came up. ROT-13 encryption worked. 

Instructions - which contained `GSGCQBRFAGRAPELCGBHEGENSSVPFBJRZHFGQVFTHVFRBHESYNTGENAFSRE.SVTHERBHGNJNLGBUVQRGURSYNTNAQVJVYYPURPXONPXSBEGURCYNA` meant "TFTPDOESNTENCRYPTOURTRAFFICSOWEMUSTDISGUISEOURFLAGTRANSFER.FIGUREOUTAWAYTOHIDETHEFLAGANDIWILLCHECKBACKFORTHEPLAN"

And plan - which contained `VHFRQGURCEBTENZNAQUVQVGJVGU-QHRQVYVTRAPR.PURPXBHGGURCUBGBF` meant "IUSEDTHEPROGRAMANDHIDITWITH-DUEDILIGENCE.CHECKOUTTHEPHOTOS".

I had to analyze the photos and find a way to get some data out of them. I jumped into trying to figure out how to do that and forgot that I have another element I haven't checked out yet - program.deb.

## program.deb

I opened, found a bunch of files that would resemble an application so I decided to try and run the program to see if something would happen. Nothing did so I tried digging into it to figure how to make sense of it. Then I tried installing it and that said "Note, selecting 'steghide' instead of './program.deb'". I looked into steghide and found out that it's a Steganography tool. 

Steganography - to conceal information within something else.

Sounds familiar, doesn't it? The images contain data about our flag. 

I installed steghide and started cracking away at the images.

## Steghide

After running `steghide extract -sf picture1.bmp`, it asked me to enter a passphrase. Looking into the code in program.deb didn't give me any hints and nothing else struck me right away so I looked into `instructions.txt` and `plan` again. `plan` says that the program was used and hidden with "DUEDILIGENCE" with a hyphen clearly separating it. I put in `DUEDILIGENCE` as the passphrase and got a response `steghide: could not extract any data with that passphrase!`. I thought the passphrase itself was wrong so I looked into it again and spent a while trying to figure it out. Eventually I tried it with the other two as well and got the flag for `picture3.bmp`.

## Flag

`picoCTF{h1dd3n_1n_pLa1n_51GHT_18375919}`