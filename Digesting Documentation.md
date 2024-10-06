# Learning from Documentation
For this challenge, I used this command: ```/challenge/challenge --giveflag``` where /challenge/challenge is the command and --giveflag is its argument.
#
# Learning Complex Usage
There are some commands that have arguments to arguments. An example of that is the ```find``` command which has an argument ```-name``` which has a corresponding argument.
For the challenge, I first listed the files in the root directory to check where the flag would be. Then I used ```/challenge/challenge --printfile /flag``` to print the flag file as it was the mentioned that --printfile is the argument and the file we wish to print is the argument to --printfile.
```
hacker@man~learning-complex-usage:~$ ls /
bin  boot  challenge  dev  etc  flag  home  lib  lib32  lib64  libx32  media  mnt  nix  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
hacker@man~learning-complex-usage:~$ /challenge/challenge --printfile /flag
Correct argument! Here is the /flag file:
pwn.college{08_x6uk_oTvD1K6pQsGZJDNG3Lj.dVjM5QDL3QjN0czW}
```
#
# Reading Manuals
```man``` command is used for displaying a manual (if there is one) for the command you provide as its argument. You can move around using PgUp/PgDown and quit using 'q'.
#
_**In a manual:**_

**Name:** Gives a short description of the command

**Synopsis:** Gives a usage synopsis. Each line is a different valid invocation of the command
```
command [optional_argument] single_mandatory_argument
command [optional_argument] multiple_arguments
```

**Description:** Gives details of the command

**See also:** Other resources that might be useful
#
For the challenge, I used the ```man challenge``` command. In the synopsis, one of the ways of using the arguments was ```/challenge/challenge --txdal 413``` to print the flag. I ran that command and got the flag.
#
# Searching Manuals
You can search by using '/'. After searching, you can use 'n' for next result, 'N' for previous result and '?' instead of '/' for searching backwards.
For the challenge, I ran ```man challenge``` then used ```/flag``` to search for arguments about the flag. Found the right one, ran that and got the flag.
#
# Searching for Manuals
For this challenge, I ran ```man man``` and searched through its synopsis. In it, it was mentioned that there is a ```man -k``` command which shows short descriptions and manual page names for the keyword provided to it as the argument. Knowing that, I ran ```man -k challenge``` and found the renamed challenge manual. Ran the command as required from there and got the flag.
#
# Helpful Programs
Learned that ```command --help``` gives a man page of sorts.
For the challenge, I ran ```/challenge/challenge --help``` since it's usually ```/challenge/challenge``` we use to get the flag. From there, I followed the instructions given.
![image](https://github.com/user-attachments/assets/ed05f822-f463-4a5a-b8d8-a4f94d4305ad)
#
# Help for Builtins
For builtin commands, ```help``` can be used directly to get more information about it. <br>
Example: ```help cd```
For the challenge, I did ```help challenge``` and then ran the command ```challenge --secret 4bFDmiTy``` as mentioned in the help page to get the flag.
#
