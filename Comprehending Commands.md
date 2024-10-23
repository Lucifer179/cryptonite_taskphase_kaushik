# Cat
It is used for reading out files
```
cat file
```
#
# Grep
It is used to search a keyword in directories/files
```
grep search_string /path/of/file
```
#
# Listing Files
It is used to list all the files in a directory
```
ls /file
ls -a /file
```
For the challenge, I used ```ls /challenge``` to find all the files in ```/challenge``` and then used ```cat /challenge/18082-renamed-run-22786``` to list the contents of file which contained the flag.
#
# Touching Files
It is used to create files
```
touch file
touch file1 file2 file3
```
#
# Removing Files
It is used to remove files in a directory
```
rm file
rm ~/file/in/this/path
```
#
# An Epic Filesystem Quest
This challenge was basically a repeated process of ```ls```, ```cat``` and ```cd```. Kept running that until I eventually found the flag.
#
# Making directories
It is used to make directories
```
mkdir my_directory
mkdir /a/directory
```
For the challenge, I did as follows:
```
hacker@commands~making-directories:~$ mkdir /tmp/pwn
hacker@commands~making-directories:~$ touch /tmp/pwn/college
hacker@commands~making-directories:~$ /challenge/run
Success! Here is your flag:
pwn.college{QPuCpTM7I8sogUAqbVnDQjciCnE.dFzM4QDL3QjN0czW}
```
#
# Finding files
It is used to find files
```
find /some/file
find -name my_file
find /some/file -name my_file_
```
For the challenge, I used ```file / -name flag``` and tested cat on the files that showed up containing the word 'flag'. One of them turned out not to be a directory for which I did ```cat``` directly and found the flag.
#
# Linking Files
It is used to create a soft link (or a symbolic link/symlink) which is basically a file that contains the original file name and when it's executed, linux will realize that it's a symlink, read the original file name and access that original file instead.
There is another link which is a hard link which is essentially an alternate address for a file. Access to the hard link and the original file are completely identical.
```
ln -s /original/file /symbolic/link
```
For the challenge, I created a symlink between ~/not-the-flag and /flag using ```ln -s /flag ~/not-the-flag``` and ran /challenge/catflag which gave me the flag.
#
