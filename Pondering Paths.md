# Position Elsewhere

So this one required me to change my directory to the root directory and that was presented as "You are not currently in the / directory." I was pretty confused cause I thought it was an error that they left it blank after /. But I tried doing that anyway and got the flag after which Ashwin explained to me that they asked me to set it to the root directory.

# Home Sweet Home

This one definitely took me a long time. I couldn't figure out initially how to execute /challenge/run/ in a way that would write it to a file of my choice. The way I understood it from the previous challenges of this module, if we're executing a run file then /challenge would be the directory and then the /run that follows it is the file we're executing. That understanding as I would come to realize doesn't exactly work here. I figured if I want to execute /challenge/run to any random file in the home directory, I would just have to do /challenge/run/~/d. That did not work. Finally after messing around for a long time, I figured since they're asking an argument, I'll try giving it a space and _then_ putting a random file in the home directory. That gave me a hint as to what I might have to do. After that, a couple of tries in I managed to get the flag. 
![Pasted image 20241002131142](https://github.com/user-attachments/assets/ba5ae832-2c2f-47a9-9db9-566138002baf)
