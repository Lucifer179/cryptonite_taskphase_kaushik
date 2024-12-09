## The source code

The length of the password was 32 characters. The code consisted 4 loops that were meant to be compared to a string and inputted into a buffer depending on the conditions given in each loop.

The string provided to us was `jU5t_a_sna_3lpm18g947_u_4_m9r54f`

## 1st loop

```
for (i=0; i<8; i++) {
            buffer[i] = password.charAt(i);
```
From i=0 to i=7 buffer positions i.e., the first 8 characters are to be directly inputted from the string.

Therefore, the first 8 characters of our required password are `jU5t_a_s`.

## 2nd loop

```
for (; i<16; i++) {
            buffer[i] = password.charAt(23-i);
```
From i=8 to i=15 i.e., the next 8 characters are taken from the (23-i) positions in the string. For i=8, 23-i=15. Therefore, the 16th position of the string is to be inputted as the next character and so on.

The following 8 characters is `1mpl3_an`.

I made a mistake in this part because I read the small L as a 1 which made me keep going back to the code to figure out what I did wrong. I had also inputted the positions incorrectly as I didn't take 23-i = 15 as the 16th position but rather the 15th in the string. These two mistakes put together cost me a lot of time. 

## 3rd loop

```
for (; i<32; i+=2) {
            buffer[i] = password.charAt(46-i);
```

From i=16 to i=30 in increments of 2 (so i=16, i=18,..., i=30) buffer positions, the `(46-i)+1`th positions are to be taken. The characters for each buffer position i = 16, 18,...,30 are `4, r, m, 4, u, 7, 9, 8`.

I made the mistake of inputting each entry one after the other (as in 16, 17 and so on) instead of the increments of two for the actual buffer position as well here. Figured that out later and fixed it.

## 4th loop

```
for (i=31; i>=17; i-=2) {
            buffer[i] = password.charAt(i);
```

From i=31 to i=17 in decrements of 2 (i=31, i=29,..., i=17) buffer positions, the `i+1`th positions are to be taken. So for i=31, the 32nd character would be inputted and so on. The characters for i = 17, 19,...,31 are `g, 4, _, _, _, 9, 5, f`.

## Final flag

Compiling all of these, the final password is `jU5t_a_s1mpl3_an4gr4m_4_u_79958f`. Therefore, the flag is `picoCTF{jU5t_a_s1mpl3_an4gr4m_4_u_79958f}`.
