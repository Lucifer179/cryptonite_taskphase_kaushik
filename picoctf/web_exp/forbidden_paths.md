Presented with a website where you can enter the file you wish to view, I had to access `flag.txt` which was in `/usr/share/html/` as mentioned in the challenge.

I tried putting in flag.txt directly, that didn't work. I went into the inspect tool to see if there was a chance for an XXE. However, this didn't use XML for its requests, so that was out of question.

Since the website blocks absolute paths, I didn't really bother to try something using that. After a while of trying to figure out if there was something else I could do, I tried the absolute path. Since that didn't work, I wrote it in a different format where the enclosing directories were represented as `..`. So `flag.txt` would lie in `../../../flag.txt`. 

I tried that, got the flag - `picoCTF{7h3_p47h_70_5ucc355_e5fe3d4d}`.