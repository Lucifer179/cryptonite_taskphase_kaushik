### The challenge
For this challenge, I was given a website `http://mercury.picoctf.net:27177/` and I had to "figure out the best cookie" to find the flag.

### How I approached it 
The website had a "snickerdoodles" placeholder so I tried that first and it showed "I love snickerdoodle cookies! Not very special though...". 

I looked into the cookies of the website and there was only one cookie which was "name" and the value was set to 0 when I tried snickerdoodles. I tried another cookie that said invalid input and the value went to -1. I tried "chocolate chip cookies" and got another value - 1.

From this I inferred that each valid cookie name gives a different value for the name. So then I went into inspect tools and started changing the value of the cookies to get the different ones. I tried till about 8 and thought this could take forever if there are a lot so I started putting in larger values to narrow down the range. I first tried 50, then 40 so on till I got my range as 0-29 for the valid cookies.

After that, I just kept trying different values successively until the cookie "18" gave me the flag.

### Final flag
`picoCTF{3v3ry1_l0v3s_c00k135_064663be}`