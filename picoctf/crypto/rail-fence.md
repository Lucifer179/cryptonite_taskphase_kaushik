## Challenge

"A type of transposition cipher is the rail fence cipher, which is described here. Here is one such cipher encrypted using the rail fence with 4 rails. Can you decrypt it?"

The encoded message was
```
Ta _7N6D49hlg:W3D_H3C31N__A97ef sHR053F38N43D7B i33___N6
```

Since this is a rail cipher with 4 rails, I put it in a rail cipher decoder with the zero offset + 4 rails parameters and got the decoded message - 
```
The flag is: WH3R3_D035_7H3_F3NC3_8361N_4ND_3ND_4A76B997
```

I initially put an initial offset of 1 which didn't work so after putting in the zero offset, the message came out correctly.

## Flag

`picoCTF{WH3R3_D035_7H3_F3NC3_8361N_4ND_3ND_4A76B997}`