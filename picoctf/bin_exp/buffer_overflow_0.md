## Challenge

"Let's start off simple, can you overflow the correct buffer?"

The source code and program were given. I understood from the source code that we have to trigger a segmentation fault for it to output the flag. The challenge then was to figure out the number of characters required to trigger that. I initially looked into only buf1 which had a cap of 100 so I looked to do cross 100. 

_Now here began the issue._ I didn't go into the instance provided in the challenge because it slipped my mind that I had to do that. I ran the program normally through my terminal which triggered a stack canary that didn't allow me to overflow it. So then I spent the hours that followed that trying to figure out how to bypass a stack canary. 

## Bypassing the Stack Canary

I found that there's a command that I can use to just "disable" it but I felt that that was too easy so I wanted to include the canary's values in my payload to bypass it. In order to do that though, I needed to find the canary in the assembly code and check its values from there. I spent a lot of time learning how to use gdb and navigate it to find the canary. After a lot of time trying to learn how to do that and still not really getting where the canary is, I looked at the challenge again and realized I had to go into the instance. I tried continuing with my method for a while still cause I wasn't satisfied with not being able to bypass the stack canary but unless I brute-forced 1024 attempts to guess it, I wasn't getting it.

## How I got the flag 

I checked the source code again to make sure I knew how many values to put and found that there is a function where `strcpy` is taking the input from the user and copying it into buf2.

```
void vuln(char *input){
  char buf2[16];
  strcpy(buf2, input);
```

The limit for buf2 is 16 characters so that would mean anything above that is enough. I went into the instance, put in any random values above 16 characters and got the flag. 

## Flag

`picoCTF{ov3rfl0ws_ar3nt_that_bad_9f2364bc}`

## Resources

- [Buffer Overflow by Aaron Yoo](https://www.youtube.com/watch?v=AD-iXWANggo)

- [Stack Canary by Aaron Yoo](https://www.youtube.com/watch?v=N7kGd76evsM)

- [GDB Tutorial by Low Level](https://www.youtube.com/watch?v=Dq8l1_-QgAc)

- [Stack Canaries by Boston Cybernetics](https://www.youtube.com/watch?v=Xt3eWaplMd0)
