## Challenge

"Our data got corrupted on the way here. Luckily, nothing got replaced, but every block of 3 got scrambled around! The first word seems to be three letters long, maybe you can use that to recover the rest of the message."

## Solve

Transposition cipher rearranges the characters of a message into a specific order that the _transposition key_ decides.

Since every third block was scrambled, I just had to notice a pattern in which it was being scrambled. The message was `heTfl g as iicpCTo{7F4NRP051N5_16_35P3X51N3_V091B0AE}2`. The first few words would obviously have to be "The flag is picoCTF{" so based off that logic and cutting it into blocks of 3, I could figure out that it was scrambled in a `2, 3, 1` pattern so to unscramble it I would simply have to write it in a `3, 1, 2` pattern. 

## Flag

Following that for the entire message, I was able to find the flag - `picoCTF{7R4N5P051N6_15_3XP3N51V3_109AB02E}`