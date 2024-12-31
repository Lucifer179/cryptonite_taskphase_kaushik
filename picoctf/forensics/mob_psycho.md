## Challenge

Can you handle APKs? Download the android apk here. 

## Solve

When I couldn't make sense of the apk after catting it, I checked the strings in it and searched for "flag" and found a line relating to it - `res/color/flag.txtUT`. Clearly, the flag was in a folder `color` within another folder `res`. With this, I figured there were multiple folders embedded in the apk so I extracted it with binwalk and found `flag.txt` in the aforementioned location.

## Flag

`picoCTF{ax8mC0RU6ve_NX85l4ax8mCl_b112ae57}`