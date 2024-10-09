## Matching with *
\'*' replaces the argument with any file that matches the pattern shown. <br>
Example: ```/cha*/run``` <br>
For the challenge, I did the following:
```
hacker@globbing~matching-with-:~$ cd /ch*
hacker@globbing~matching-with-:/challenge$ /ch*/ru*
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{EnFVvoNVw1g9X7iSVST1JGXlxI4.dFjM4QDL3QjN0czW}
```
#
## Matching with ?
'?' replaces the argument with only a **single** character. <br>
Example: ```/cha?leng?/r?n``` <br>
I solved the challenge as follows:
```
hacker@globbing~matching-with-:~$ cd /?ha??enge
hacker@globbing~matching-with-:/challenge$ /challenge/run
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{0WJKi-7eGg0qZiNOcsGqZ6p9WVl.dJjM4QDL3QjN0czW}
```
#
## Matching with []
\'[]' is basically a more specific form of '?'. It replaces the argument with whatever subset of characters is provided inside the square brackets. <br>
Example: ```/challenge/run flag_[abc]``` for the results ```flag_a```, ```flag_b``` and ```flag_c```. <br>
**Note:** The order of the characters don't make a difference. It'll print the files out in the format they're in. <br>
For the challenge, I changed my directory to ```/challenge/files``` then ran the command ```/challenge/run file_[bash]``` for the flag.
#
## Matching paths with []
You can expand absolute paths with globs cause they happen on a path basis. <br> 
For the challenge, I initially tried running ```/challenge/run /challenge/run/file_[bash]``` to get the flag but then got the hint that I'm trying to define the absolute path of the files in "/challenge/run" when it's in "/challenge/files" after which I corrected it to ```/challenge/run /challenge/files/file_[bash]``` and got the flag. 
#
## Mixing globs
Didn't understand initially how to expand it to (challenging, educational, pwning). It kept expanding to the argument I provided in square brackets, like ```[cepw]```. <br>
Then I tried a bunch of stuff for a _long_ time (like ```[clw], n*[gl], e*[dw], ``` etc.) and finally got an expanded version with ```?*[ce]```. From there I was essentially trying to figure out which exact combination of keywords would give only the required files. This again went on for a long time. Finally I did ```[cep]*```. And that gave me the flag. <br> 
All of this is to say that I basically overthought the hell out of it and it was actually simple. 
#
## Exclusionary Globbing
Gives all files except ones mentioned in the square brackets by adding a '^' to it. <br> 
Example: ```ls [^abc]``` <br>
For the challenge, I changed to the /challenge/files directory then ran  ```/challenge/run [^pwn]*```.
