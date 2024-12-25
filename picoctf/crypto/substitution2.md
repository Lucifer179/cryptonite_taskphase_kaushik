## Challenge

"It seems that another encrypted message has been intercepted. The encryptor seems to have learned their lesson though and now there isn't any punctuation! Can you still crack the cipher?"

## Solve

Despite any punctuation, the steps to follow were pretty much the same. It was just more tedious to do so. I first began with the key given in `substitution0` to see if that would give me anything. It didn't, so I started replacing the letters for "picoCTF" and "the flag is" from the ciphertext. From here, I had a base to go off from because I was able to make out some words or the other. Following this, I just kept replacing and checking the sample text and then replacing more from what I could make out. 

Finally, I had only a few letters missing which were `j, w and z` for plain text and `l, w and y`. The flag I was getting after all this was `PICOCTF{N6R4M_4N41Y515_15_73D10U5_702F03FC}`, which had `y`. So then by that logic replacing that Y with j, w or z should get me the flag. What I failed to consider was that the Y I had there was a Y received after decoding. So after wasting my time trying to figure out why trial and error wasn't getting my flag, I used my brain for 2 seconds and realized what I did wrong and put the flag as is. 

## Flag
`PICOCTF{N6R4M_4N41Y515_15_73D10U5_702F03FC}`