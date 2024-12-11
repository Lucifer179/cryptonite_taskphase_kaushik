

I haven't learnt C properly so I couldn't figure this challenge out myself. I got the final flag by basic trial and error initially but obviously there's no point in solving a challenge like that if I haven't actually understood anything to take away from it.

I watched a couple of  videos on format string exploitation from LiveOverflow to see if that would give me enough knowledge to work off of for this challenge but as I would come to realize, I needed knowledge of C as well to properly implement it. 

After trying to figure it out myself and getting intimidated by the source code, I gave up on trying to solve it and looked up the challenge to understand which direction to be going in. I found a writeup (reference provided below) and began from there.

### Patrick's Order
First I understood where to look for the condition to be satisfied for the first order (Patrick's order). The code was
```
int count = printf(choice1);
        if (count > 2 * BUFSIZE) {
            serve_bob();
        }
```
BUFSIZE refers to 32 bytes, so we needed an input that was greater than 64 bytes. The options provided were `Breakf@st_Burger`, `Gr%114d_Cheese` and `Bac0n_D3luxe`, none of which were exceeding the required amount of characters. 

However, `%d` is a format specifier and when the `d` is prepended with a number, it expects to print a number with the width of that many characters, as I read in the writeup. So, `%114d` would print a number with a width of 114 characters but since we haven't provided a number for it to print, it would put garbage values to fill that in. That in turn would give us a value that would satisfy the requirement for the first part of the challenge.

### Bob's Order
Following this understanding, I figured there should be a similar condition that would satisfy this order as well, but there was nothing in the source code that would point to that like in the previous order. The requirement this time was to "serve something outrageous that would break the shop". The options were `Pe%to_Portobello`, `$outhwest_Burger` and `Cla%sic_Che%s%steak`.

I knew the order should be something with a `%` in it, so the correct option had to be either `Pe%to_Portobello` or `Cla%sic_Che%s%steak`. After cross-checking with a list of format specifiers, I knew that `%t` wasn't one in C so the correct answer _had_ to be the one with `%s` in it. I tried `Pe%to_Portobello` anyway and indeed it didn't work. I restarted and tried `Cla%sic_Che%s%steak` and it gave me the flag. 

I didn't understand why that specifically matches the "outrageous" request for the order so I read the writeup again and understood that `%s` expects a string of characters as the argument to process it. `%steak` isn't a valid argument for it, but `%s` still tries to process it. This triggers "undefined behaviour", which either accesses arbitrary memory or causes the program to crash. This fulfills Bob's outrageous order request.
### References
[Eric H writeup](https://medium.com/@erichdryn/format-string-0-picoctf-writeup-9e8af9e163ff)

### Final Flag
`picoCTF{7h3_cu570m3r_15_n3v3r_SEGFAULT_dc0f36c4}`