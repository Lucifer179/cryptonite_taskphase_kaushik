### The PATH Variable
PATH is a variable where the information for executable files resides in our computers. If the PATH variable is made blank then it cannot run commands that aren't inbuilt (like cat and ls). 

For the challenge, I set the value to nothing with `PATH=""` and then ran `/challenge/run` so that it couldn't delete the flag file.
#
### Setting PATH
We can change the PATH variable to a directory of our choice too by setting it as so. This is useful for when we have commands in nonstandard places which we have to invoke via their path. If we want to launch them by their bare name then we can set PATH to the directory containing those commands and invoke it directly.

For the challenge, I set the PATH variable to `/challenge/more_commands`. Since the win command is the _only_ thing that `/challenge/run` needed to print the flag, we could set the PATH to that directory directly, overwriting the previous PATH value. I ran `/challenge/run` after that and got the flag.
#
### Adding Commands
As we saw in the last challenge, by setting the PATH variable to a directory that contained our command, we could invoke it directly. We can use the same principle for adding commands of our own. 

For this challenge, I had to set the PATH variable to a directory which contained a _win_ shell script that I had to create for `/challenge/run` to run. The purpose of win is to cat the flag and so the shell script should contain a similar command. 

I didn't realize that initially and simply first created a "win.sh" in the home directory which contained the `win` commmand in it. After that didn't work, I read a hint that said since win is the _only_ command that `/challenge/run` needs, we can set it to that directory directly. Following this logic I figured making a directory (which I named "winning") that contained only the `win` shell script would make it work. It did not.

Then I finally did come to the revelation that since win doesn't exist, creating a shell script _with "win" in it_ doesn't exactly make much sense. _But..._ the purpose of win in the previous challenge was to cat the flag file. To emulate that function I dug around the PATH variable using `echo $PATH` and looked for the directory that contained the `cat` command to invoke it directly in the shell script (since changing PATH makes it so that it can't be invoked the normal way). 

Eventually I found it, modified the shell script to have `/usr/bin/cat /flag`, ensured that it could be executed (using `chmod a+x winning/win`) and then set the PATH to "winning" through `PATH=~/winning` and ran `/challenge/run` which gave me the flag.
#
### Hijacking Commands
In the previous challenge, I created a file "win" whose purpose was to cat the flag. This time, `/challenge/run` would execute `rm` and delete the flag if I ran it so I needed to make it so that it can't do that. Easy enough, changing the PATH variable does that anyway. But I also needed it to the print the flag.

So, to trick it into doing that, I made the same shell script as last time that would invoke the cat command through its path and cat the flag and named it as `rm` instead of `win`. I set the PATH variable to the directory `rm` resided in (which was still `~/winning` in this case) and ran `/challenge/run`. It didn't delete the flag and instead printed it.
#
