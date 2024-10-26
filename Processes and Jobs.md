### Listing Processes
```ps``` stands for either "process snapshot" or "process status" and basically lists all the processes going on. 

#### ```ps``` arguments:
```-e```: every process <br>
```-f```: full format <br>
`-o`: shows the stat column <br>
```a```: processes of all users <br>
```x```: processes not running in the terminal <br>
```u```: user-readable output <br>
Generally used: ```ps -ef``` and ```ps aux``` which give similar outputs except ```ps -ef``` also gives the PPID (Parent Process ID) and ```ps aux``` gives percentage of total system cpu and memory used.

I got the flag by running ```ps aux``` then running the challenge command shown in the process list.
#
### Killing Processes
Processes can be terminated using ```kill <PID>``` command. 

For the challenge, I listed the processes and grepped `/challenge/dont_run` by running ```ps -ef | grep /challenge/dont_run``` and then killing the "dont_run" process. After that I ran `/challenge/run` to get the flag.
#
### Interrupting Processes
A process can be interrupted if it clogs up the terminal by doing ctrl+c.

For the challenge, I just had to interrupt `/challenge/run` and got the flag.
#
### Suspending Processes
By doing ctrl+z, we can suspend a process instead of terminating it completely. 

For the challenge, I did the same thing as last time except with ctrl+z instead and then ran `/challenge/run` again to start another copy of the process in the terminal.
#
### Resuming Processes
A process can be resumed by running the `fg` command which resumes a process and brings it to the foreground.

For the challenge, I ran `/challenge/run`, suspended it and then resumed it through the command `fg /challenge/run` and got the flag.
#
### Backgrounding Processes
If we want to resume a process in the background instead of foreground after suspending it then we can just do `bg` instead of `fg`. 

'S' in bash means it's sleeping, waiting for input. 'R' means it's running. '+' means it's in the foreground. 

For the challenge, I did everything from the previous challenge and then instead of `fg`, I did `bg` to resume the process in the background.
#
### Foregrounding Processes
A process in the background can be foregrounded by running the `fg <process>` command.
#
### Starting Background Processes
A process can be started in the background right away by appending it with `&`.

For the challenge, I ran ```/challenge/run &```.
#
### Process Exit Codes
Every process has an exit code when it terminates. The exit code of a process can be determined using the special variable '?' and prepending it with '$' for it to read its value. Basically we can run `echo $?` after a process terminates to get its exit code. Commands that run typically return 0 and commands that fail give a non-zero (but usually 1) value.

For the challenge, I ran `/challenge/get-code`, got the exit code from `echo $?` and ran `/challenge/submit-code 155` where '155' was the exit code of the get-code command.
#
