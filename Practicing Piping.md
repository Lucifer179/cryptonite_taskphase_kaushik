### Redirecting output
This is used to redirect the output of a command to the file specified as the argument of '>' . <br>
Example: ```echo hi > file``` <br>
Here, when you run ```cat file``` it will output "hi". <br>
For the challenge, I ran the command ```echo PWN > COLLEGE``` and got the flag.
#
### Redirecting more output
I did ```/challenge/run > myflag``` to send the output of the command to "myflag" and then did ```cat myflag``` when it said all the requirements were satisfied to receive the flag.
#
### Appending output
To add on multiple outputs to a file - aggregating outputs to a single file (usually for the purpose of analyzing it all later). `>` would delete the old output and put the new one in so `>>` is used for the purpose of _appending_ it. <br>
Example: 
```
echo output > my-output
echo another_output >> my-output
cat my-output
output
another_output
```
I solved the challenge by appending /challenge/run to "/home/hacker/the-flag" file through the ```/challenge/run >> ~/the-flag``` command. Then I got the flag in the flag file by running ```cat ~/the-flag```.
#
### Redirecting errors
A File Descriptor describes a communication channel in Linux where <br>
FD 1 - Standard Output <br>
FD 2 - Standard Error <br>
A simple `>` without FD number specified just means FD 1 which makes it an **implicit** FD number. <br>
For redirecting errors to a file, you can:
```
echo hi 2> errors.log
```
You can also redirect multiple FDs at a time:
```
command > output.log 2> errors.log
```
which would redirect the output to output.log and errors to errors.log. <br>
Notice that when you redirect errors, nothing would be printed on the terminal whereas when you redirect only the output, the command communicates its instructions and feedback _over_ standard error and only prints the output over standard out. <br>
In the challenge, I ran the command ```/challenge/run > myflag 2> instructions``` to redirect output to 'myflag' and errors to 'instructions'. Therefore, when I catted instructions, it gave me the errors message and catting myflag gave the flag.
#
### Redirecting input
As mentioned earlier, for redirecting output one can do '1>' or simply '>' and for errors '2>'. However, for redirecting input one would have to do '<'. <br>
Example:
```
echo hi > message
cat message
hi
rev < message
ih
```
which takes the input for the command 'rev' from the 'message' file. <br>
In order to write the value 'COLLEGE' to the PWN file I used the command ```echo COLLEGE > PWN``` and then the challenge said to redirect the PWN file to ```/challenge/run``` for which I ran ```/challenge/run < PWN``` by which /challenge/run essentially takes the input from the PWN file to run itself. I ran into some confusion in doing this because I understood how to write 'COLLEGE' to PWN but then overthought what /challenge/run is supposed to do. Then realized I'm probably overthinking, read the challenge again, ran the commands simply according to what it was asking, and got the flag. 
#
### Grepping stored results
For this challenge, I had to grep the flag from the ```/tmp/data.txt``` file to which I had redirected the output of ```/challenge/run``` to. <br>
I ran the following set of commands to do so:
```
/challenge/run > /tmp/data.txt
grep pwn /tmp/data.txt
```
Initially I tried ```grep flag/tmp/data.txt``` then realized the flag itself has the keyword 'pwn' in it, not 'flag'. 
#
### Grepping live output
By using ```|```, which is called a pipe operator, one can connect the standard output of the command on the left of it to the standard input of the command to the write of it which cuts out the need to store the output to a file first then run the command needed. If I ran an echo and grep command then the grep would automatically search for the keyword in its argument in the output of the echo command. <br>
For example: 
```
echo yes-yes-yes-no-no | grep no
yes-yes-yes-no-no
```

```
echo yes-no | grep maybe

```
<br>
For the challenge I had to search for the flag in the output of ```/challenge/run``` so I used this command: ```/challenge/run | grep pwn``` and found the flag.
#
### Grepping errors
Alternate way of looking at the '|' operator is that it redirects standard output to another program. However, that is all it can do alone i.e., it can redirect standard output _only_. It cannot redirect standard error of the command to the left of it to the command to the right of it. To work around that, there is the ```>&``` operator which redirects a file descriptor to _another_ file descriptor. So we can redirect standard error to standard output by doing ```2>&1``` then pipe as normal. <br>
For the challenge, I did exactly that by running ```/challenge/run 2>&1 | grep pwn``` and got the flag.
#
### Duplicating piped data with tee
When we're piping one command to another, it doesn't show us the output of the first command and would directly run both commands (naturally, because that is the intention) but sometimes we would want to see the output of it for the purpose of debugging if anything has gone wrong. <br>
For that, ```tee``` is used. It prints the output of the first command to whichever file is provided as its argument and runs the full pipe command as per normal. <br>
Example: 
```
echo hi whats up | tee echo_output | grep whats
```
If I were to run ```cat echo_output``` I would be able to see the output of the first command which is "hi whats up" here. <br>
For the challenge, I used the above logic to create a random file "search_flag" where the output of /challenge/run would be printed. <br>
[insert image in personal notes group here] 
#
### Writing to multiple programs
So process substitution is used when you want to pipe the _stdout_ of a command to **multiple** commands. It feeds the output of a process into the _stdin_ of another process. If I wished to take the _stdout_ of a command (say echo) as the _stdin_ of two other commands (say rev and ls) then I could pipe echo and cat as per usual with a ```tee >(rev)``` in between. 
```
echo hello | tee >(rev) | ls
```
Here, it uses the output of ```echo``` as the input for both ```ls``` and ```rev```.  <br>
What >(rev) does is that it creates a temporary file called a _named pipe_ which is hooked up to rev's input. The output of echo writes itself to the named pipe and the 'rev' command is made to run on that temporary file. Writing to this file will pipe data to the _stdin_ of the command in the brackets. Usually this is done using commands that take output files as arguments (like tee). <br>
Following this understanding, I approached the challenge with the goal to take the output of ```/challenge/hack``` as the input for both ```/challenge/the``` and ```/challenge/planet```. In order to do so, I ran the command ```/challenge/hack | tee >(/challenge/the) | /challenge/planet``` and got the flag.
#
### Split-piping stderr and stdout
This took me the entire evening, lol. I was trying something along the lines of:
```
/challenge/hack 2&>1 | tee >(/challenge/the) | /challenge/planet
```
which instead gave the stdout of /challenge/the as stdin of /challenge/planet. So the main challenge I was trying to work around was the fact that I had write both the stderr and stdout of /challenge/hack to them simultaneously. I kept trying different combinations of these to try to make it work. Going back to what the previous challenge explained: ```echo hi | rev``` is the same as ```echo hi > >(rev)```. This and what this challenge mentioned specifically about using "2>", I finally tried ```/challenge/hack > >(/challenge/planet) 2> >(/challenge/the)``` and got the flag. The main issue was that I was approaching it wrong to begin with.  
