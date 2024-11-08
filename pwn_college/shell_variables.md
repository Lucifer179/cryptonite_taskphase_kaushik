### Printing Variables
```echo variable``` would just print "variable", but by prepending it with ```$``` we can print the variable.  
```
echo $variable
``` 
I got the flag by running ```echo $FLAG```.
#
### Setting Variables
Note that $ is used to only _access_ variables, not to set them. $ triggers variable expansion. We can set a variable in the following way: ```var=182``` with no spaces between them. <br>
I set the variable PWN to COLLEGE to get the flag by running ```PWN=COLLEGE``` command.
#
### Multi-word Variables
To set a variable to multiple words, enclose them in quotations ("") so that it recognizes the words as a single token. <br>
For the flag, I set 'PWN' to 'COLLEGE YEAH' using ```PWN="COLLEGE YEAH"``` command.
#
### Exporting Variables
"sh" is another shell's process. When we invoke it in our regular session, it's invoked as a child of the main shell process. So when we set a variable in our regular session, it's not stored as a variable in other processes too. In order to do that, we'd have to export it which passes them into the environment variables of the child processes. 

To export a variable, we simply have to run the 'export' command with the variable we want exported as its argument.

For the challenge, I set the PWN variable to COLLEGE and exported it and then set the COLLEGE variable to PWN (and didn't export that one). I ran /challenge/run and got the flag.
```
hacker@variables~exporting-variables:~$ PWN=COLLEGE
You've set the PWN variable to the proper value!
hacker@variables~exporting-variables:~$ export PWN
You've set the PWN variable to the proper value!
hacker@variables~exporting-variables:~$ COLLEGE=PWN
You've set the PWN variable to the proper value!
You've set the COLLEGE variable to the proper value!
hacker@variables~exporting-variables:~$ /challenge/run PWN
CORRECT!
You have exported PWN=COLLEGE and set, but not exported, COLLEGE=PWN. Great
job! Here is your flag:
pwn.college{4UEooPoXYg2AxZjXgtKfc6owZmg.dJjN1QDL3QjN0czW}
You've set the PWN variable to the proper value!
You've set the COLLEGE variable to the proper value!
hacker@variables~exporting-variables:~$
```
#
### Printing Exported Variables
```env``` prints every **exported** variable set in our shell.
#
### Storing Command Output
I was wondering about this actually when the concept of variables got introduced - as to whether we could set variables to a certain command, or something similar to it.

Command substitution: Used for storing the output of some command into a variable.
```
VAR=$(cat /abc)
VAR=$(ls)
```
For the challenge, I set the variable PWN to contain the output of /challenge/run by running ```PWN=$(/challenge/run)``` and got the flag through ```echo $PWN```.
#
### Reading Input
'read' prompts input from the user and sets the variable accordingly. By running the read command, we can feed _input_ to it.

For the challenge, I gave the input of PWN as COLLEGE by running ```read PWN``` then putting "COLLEGE".
#
### Reading Files
'read' can be used to take input for a variable from a file directly by running the command in the following manner:
```
echo test > some_file
read VAR < some_file
```
Here, it takes input from "some_file" for setting the variable. The final result is basically ```VAR=test```.

For the challenge, I ran the command ```read PWN < /challenge/read_me``` and got the flag
#
