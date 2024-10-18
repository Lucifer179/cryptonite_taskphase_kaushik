## Format of the ls -l information

`-` - indicates that it's a file.

`d` - indicates that it's a directory.

The next 9 are split in 3-3-3: First 3 indicating owner/user permissions, Second 3 indicating group permissions and Third 3 indicating others permissions.

The next two columns indicate the owning user and the owning group.
#
### Changing File Ownership
By use of the `chown` command, the ownership of a file can be changed. 

Format: `chown [user] [file]`

Note: Typically, chown can only be invoked by the root user.

For the challenge, I listed the permissions of `/flag` using `ls -l /flag` and then changed the ownership of `/flag` to 'hacker' through `chown hacker /flag`. Then I catted the flag file and got the flag.
#
### Groups and Files
We can check which groups we're a part of using the `id` command. We're usually part of multiple groups for control access to different system resources.

The group that a file is owned by can be changed using the `chgrp` command.

Format: `chgrp [group] [file]`

For the challenge, I changed the group of `/flag` using `chgrp hacker /flag` and then catted it to get the flag.
#
### Fun With Groups Names
First I used `id` to figure out which groups I can change the ownership of `/flag` to. Then seeing as how I was in `grp13314`, I changed the group of `/flag` using `chgrp grp13314 /flag` and then catted it per usual.
#
### Changing Permissions
`r` - user/group/other can **r**ead the file.

`w` - user/group/other can **w**rite to the file/modify it/create or delete the file.

`x` - user/group/other can e**x**ecute the file.

`-` - nothing.

Permissions can be changed using the `chmod` command.

Format: `chmod [u/g/o/a][+/-][r/w/x]` where, 

u - user, g - group, o - others, a - all,

`+/-` - to remove or add the permission,

r - read, w - write, x - execute.

Even if you don't own a file, if you have write access to a file, you can change its permissions to be able to read/write/execute it.

For the challenge, I first tried to change the permissions of the /flag file for the user (me) to be able to read it using the command `chmod u+r /flag` but then it didn't work so then I tried the same with group, which didn't work either. Finally, it was changing the permissions for "others" through `chmod o+r /flag` that worked in allowing me to cat the flag file.
#
### Executable Files
I changed the permissions of `/challenge/run` for others to be able to execute it this time, thinking I'd learn from the previous challenge. Alas, this challenge decided to screw me over as well. 

So then this time I did `id` to check whether I'm part of the group that has access to the file. I was both the owning user and the group, from which I (thought I) understood that changing permissions for either the user or the group will do the trick. I changed it for the group. That did not work, which meant my previous hypothesis was wrong. I changed it for the user, and it finally worked. 

What confused me about this ordeal was that if I'm part of the owning group then changing permissions for that group should've done the trick too, but it didn't. After this I asked Ashwin and found out that there's an order with which it checks the perms. If I'm the owner of the file then it would check the owner's permissions. If I'm not then it would check group followed by others.
#
### Permission Tweaking Practice
I was pretty glad this was a challenge, since I was just thinking at that point that it'd be nice to practice that command a little more. I messed up a few times in this challenge due to which I had to restart cause I was playing around with what works and what doesn't. Got the hang of it eventually, completed the challenge, got the flag.
#
### Permissions Setting Practice
Permissions can be simply be set directly instead of adding/subtracting from them. By setting permissions, you overwrite the old ones. It's done by using `=` instead of `+/-`. 

Multiple permissions can be set using commas in between. Note that there should be no gap between each of them. Permissions can also be zeroed out entirely by doing `u/g/o=-`.

Format: `chmod u/g/o=r/w/x [file]`

For the challenge, I did the same thing as last time except setting them instead of adding/subtracting perms. I got the flag eventually.
#
### The SUID Bit
The Set User ID permission bit allows users that aren't the system admins run programs as owners of that program's file. This means that if a file/program has `s` in place of `x` then any user that has execute permissions can execute the program as the owner user. 

As an owner, a file's SUID can be set using `chomd u+s [program/file]`.

For the challenge, I set an SUID on `/challenge/getroot` through `chmod u+s /challenge/getroot` command. It spawned a root shell for me and then I did `cat /flag` and got the flag.
#
