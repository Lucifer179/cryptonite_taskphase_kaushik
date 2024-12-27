## Challenge
"One of our Detective tapped a channel to intercept this signal but couldn't read it, HELP HIM"

Given was a `signal.sr` file.

## Solve

After checking it with `file signal.sr`, I found that it could be extracted. After doing that I found a bunch of "logic" files. I tried reading the contents of them but I couldn't. 

I knew the challenge had something to do with UART so I started looking into decoding a received UART signal and found that I could use a logic analyzer for the same. I first tried using Logic2 from Saleae but it wasn't accepting my file and said I need it in `.SAL` format so I looked for other logic analyzers and finally found PulseView. Putting in the extracted files individually didn't work so I thought that was a problem with it being extracted (I don't know what logic that was but I rolled with it) and tried the original `signal.sr` file which worked.

The issue now was that I found a bunch of lines without any disturbances as such so then I again started looking into what I may have done wrong. From the writeup, I knew that I needed the baud rate to be able to solve the challenge so I thought that since there aren't any waves as such, I have to count it using the bits themselves. I did that for a while and was getting a very high number like 16 million but I figured that's just how it is so I went with it and continued. I started looking for a UART decoder online that would take the baud rate as a parameter and solve from the file but to no avail.

I went back to the writeups and found that there _should_ be waves somewhere. I restarted the whole process in case I made a mistake somewhere along the way and this time I found the waves. I started calculating the bits from there taking denominations of 3 cause that just made the most sense to me. I knew that the flag has to begin with `nite{`, but it wasn't when I was taking the bits as is. I dug into it more and found that I have to reverse it cause it's taken LSB to MSB instead of the other way round so I reversed the binaries and started calculating again.

In the end, I got the flag by doing that and didn't need the baud rate at all so I'm not sure what the point of that was.

## Flag

`nite{n0n_std_b4ud_r4t3s_ftw}`