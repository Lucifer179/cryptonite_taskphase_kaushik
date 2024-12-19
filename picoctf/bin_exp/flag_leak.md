## Challenge

"Story telling class 1/2 I'm just copying and pasting with this program. What can go wrong? You can view source here."

The source code given to us showed that it had a format string vulnerability `printf(story)` where "story" is the input from the user because it doesn't specify what type of input it wants so we can give any type of input with different format specifiers to leak information.

After testing that with format specifiers like `%s` and `%p`, I confirmed that there definitely was a vulnerability. I know that if I use the specifier `%n$s` which leaks info of the $ n^{th} $ element, I'll get the flag at _some_ point but it didn't seem feasible to just brute force it so what I needed to know was where the flag was. 

Looking at the disassembled code of `vuln`, I tried finding where exactly the `readflag` function has the flag. I spent a long time trying to do this and trying to figure out other ways to pinpoint where it is but to no avail so eventually I decided to brute force it anyway. 

After some time, I got the flag at the 24th element.

## Flag

```
$ nc saturn.picoctf.net 53704
Tell me a story and then I'll tell you one >> %24$s
Here's a story - 
CTF{L34k1ng_Fl4g_0ff_St4ck_999e2824}
```

## Resources

- [Format String Vulnerabilities by CryptoCat](https://www.youtube.com/watch?v=iwNYoDw1hW4)

- [Format String exploit by LiveOverflow](https://www.youtube.com/watch?v=0WvrSfcdq1I)