### Chaining with Semicolons
Multiple commands can be executed at once using a `;`. 

Example: `echo imahacker > hacker.md; cat hacker.md`

For the challenge, I used the command `/challenge/pwn; /challenge/college`.
#
### Your First Shell Script
Chaining commands gets cumbersome for a higher number of commands so instead we can just create a file (generally named like `<file>.sh`) with all the commands in it in the sequence we want and then execute that file using the command `bash <file>`. 

For the challenge, I created a x.sh file through `touch x.sh`. I put the commands `/challenge/pwn` and `/challenge/college` using vim and then executed the file through `bash x.sh`. 
#
### Redirecting Script Output
The output of a script can be piped, redirected etc. using the same `>`, `>>`, `2>`, `2>>`, `<`, `>&`, `|` functions that we've been using. 

For the challenge, I piped the output of a shell script containing the `/challenge/pwn` command followed by the `/challenge/college` command into the input of `/challenge/solve` using the command `bash challenge.sh | /challenge/solve`, where challenge.sh was my shell script.
#
### Executable Shell Scripts
A script can be executed directly by invoking instead of having to manually mention bash for it if the shell script is executable. If it isn't then we can just change the permissions as we learnt earlier.

For the challenge, I made some random shell script `challenge.sh`, put `/challenge/solve` into it using vim, changed the perms using `chmod a+x challenge.sh` and then executed it through `~/challenge.sh`.
#
