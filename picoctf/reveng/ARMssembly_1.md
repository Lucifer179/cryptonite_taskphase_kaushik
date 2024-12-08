For this challenge, I had analyze an assembly code to figure out what argument would give the output 'win' for the variables 79, 7 and 3.


### Analyzing 'func'
The first value in the stack is stored in `sp + 12`, the decimal 79 is stored in `sp + 16`, 7 in `sp + 20` and 3 in `sp + 24`. 

After that, the data in `sp + 20` i.e., the number 7 is loaded into the w0 register and the data in `sp + 16` i.e., 79 is loaded into the w1 register. Then the command `lsl w0, w1, w0` is carried out which basically shifts the number 79 in binary by 7 bits to the left (lsl means Logical Shift Left) and stores that in w0. To find the value of w0 directly, we can simply multiply 79 with 2^n where n is the number of bits to be shifted i.e., 7 in this case. So the final decimal value in w0 is 79\*2^9 which is 10112.

Moving forward, the data in w0 is stored into `sp + 28` and then that is loaded into w1. So effectively, w1 now has 10112 in it. The data from `sp + 24` is loaded into w0 which means that the number 3 is now in w0. Then the command `sdiv w0, w1, w0` is carried out which divides w1 with w0 and stores the result in w0. w0 therefore has the quotient of 10112/3 in it which is 3370.

In a similar fashion as earlier, the data in w0 gets stored into w1, `sp + 12` i.e., the first value in the stack - let's say X - gets loaded into w0 and the command `sub w0, w1, w0` is carried out giving the data in w0 as `3370 - X`. This is our final value in w0 and is temporarily stored there.

### Analyzing 'main'

I didn't really understand how a lot of what was happening in it played into our requirement of finding an argument that would give the 'win' result. However, there is one line that relates to it which is `cmp w0, 0`. This compares the value in w0 with zero. My takeaway from that was that if w0 is zero then we would get the 'win' output. So the argument we need i.e., X to get the required output is 3370 itself. 

### Final flag

3370 in hex is 0xD2A. To get it in the required format, we have to remove 0x, make it all lowercase and make it 32 bits. I didn't really grasp the 'make it 32 bits' part initially and spent a long time trying to understand why my answer was incorrect and since it was showing as so, I kept going back to the code to understand what I did wrong. Eventually, I actually read it and the final flag was `picoCTF{00000d2a}`.
