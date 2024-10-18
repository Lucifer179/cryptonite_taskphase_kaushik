## Preliminary Information
In the information of `/etc/passwd` or `/etc/shadow` - the first part represents the user, the second represents the password (if it has * or ! it means the password has been disabled) and it contains an 'x' in `/etc/passwd` since it doesn't still contain passwords. A blank space means there is no password for that file.
#
### Becoming root with su
`su` and `sudo` are used to run commands as the root user. 

`su` has the SUID bit set so `su` runs as root and by doing so, it starts a root shell. It asks for the root password before giving a user root privileges first though. 

For the challenge, I ran `su`, put the password that they gave, got the flag.
```
hacker@users~becoming-root-with-su:~$ su
Password:
root@users~becoming-root-with-su:/home/hacker# cat /flag
pwn.college{83VuvwyhUV3P6Nh8qQL2lpzRp4Z.dVTN0UDL3QjN0czW}
```
#
### Other users with su
Giving a username as the argument to `su` allows you to switch to that user instead of root.

Format: `su [user]`

For the challenge, I switched to the _zardus_ user through `su zardus`, put in the password provided and ran `/challenge/run` to get the flag.
#
### Cracking passwords
Since `/etc/passwd` was a globally readable file, passwords were shifted to `/etc/shadow`. Someone that cats that file as the root user can see the passwords in it.  

When a password is inputted into su, it one-way-encrypts it and compares it to the stored value for the password. If they match then the user is given access by `su`.

If there is a leak of `/etc/shadow`, the hashed value of a password can be cracked using **John The Ripper**. 

Format: `john [file]` 

For the challenge, I ran `john /challenge/shadow-leak`, got the password as "aardvark", su'd to zardus using the password and ran `/challenge/run` to get the flag.
#
### Using sudo
`sudo` runs a command as a root unlike `su` which just directly launches a shell as the root user. Instead of a password, `sudo` relies on policies that checks the user's authorization to run programs as root. `sudo`'s security log is stored in `/etc/sudoers`. 

For the challenge, I just had to do `sudo cat /flag`.
#
