## Challenge
"Here's a file that was recovered from a 32-bits system that organized the bytes a weird way. We're not even sure what type of file it is."

## Solve

I started with checking what the file type was with which just showed that it's a data file. Then I looked into the contents of the file itself to see if that would give me any clues on what it is and what it does. When that didn't work out I used exiftool to get more details about the file which is when I found something interesting. In the warnings section it showed - "Processing JPEG-like data after unknown 1-byte header". Then I dumped its hex into another file to try and find info about the header. 

The first four bytes contain information about the header. After digging into what the JPEG header is, I realized that the header bits were just the reversed JPEG header. After fixing that, the `challengefile` turned into a jpeg file. However, the image still wasn't visible.

I dug around for a while to figure out why that may be then realized that each 4 bits are probably reversed so I needed a way to rectify that. I first thought of writing a program that would get the hex of a file, reverse every 4 bits then give it back but that seemed complicated without some serious digging into syntax for achieving that. 

The name of the challenge is usually a hint so I looked into little endian and big endian once again and realized that I could just swap the endianness of the file itself to reverse every 4 bytes. 

## Flag

Using CyberChef, I did the reversal and got the flag - `picoCTF{cert!f1Ed_iNd!4n_s0rrY_3nDian_188d7b8c}`.