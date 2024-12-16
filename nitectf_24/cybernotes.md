## Challenge
"I created the world's most secure notes app, but might have uploaded and forgotten about some personal files. Whatever,even if they try to look they will go in the wrong place."
The challenge is to first log in to the website and then find the flag after logging in through a secret jwt key.

## My Approach
I tried running SQL injections repeatedly to log in. When it didn't work, I tried looking through pentesting resources to find other methods
of getting into the website, and also tried to find other SQLi payloads in case the problem was with the one I was using.

## The Actual Solution
The background image lies in the webpage `./uploads`. By simply going to that page, I can find chat logs and a "Dockerfile". The logs contained the 
login username and password required. After logging in, I could see the authorization key. I simply had to take that, put it in a JWT decoder and put in the key found in `Dockerfile` and resend that request to get the flag.

## Flag
`nite{7rY_XKcD_S3b_f0R_3xPl4nA7i0n}`