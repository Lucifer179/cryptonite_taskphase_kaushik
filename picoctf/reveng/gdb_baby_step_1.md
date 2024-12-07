For this challenge, I had to just debug the file given and check what eax contained at the end of it. 

I used `objdump -d -Mintel debugger0_a > file` in the terminal to debug it directly and just looked at the debugged assembly code in "file" to find what eax contained which was `0x86342`. 

The flag was the decimal code of that so my final flag was `picoCTF{549698}`.

I thought the challenge was more complicated than it was so I spent a little more time on analyzing the code before I realized it's just asking me to say what eax has directly instead of figuring out what contents 0x86342 may have had.
