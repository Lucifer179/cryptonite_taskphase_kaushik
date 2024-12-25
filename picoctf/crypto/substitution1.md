## Challenge
"A second message has come in the mail, and it seems almost identical to the first one. Maybe the same thing will work again."

I knew that this was would be another substitution cipher so I got cracking at it. 

## Solve

I tried it with the same key as `substitution0` at first since it was said that it's identical but it didn't give me the correct deciphered text. But, I could make out some words to be a certain way so I began replacing the texts in the key using common sense.

The more I put in the letters I knew, the closer I was getting to the actual text. I was getting outputs like these -
```
CTFS (SHORT FOR CAPTNRE THE FLAG) ARE A TYPE OF COMPNTER SECNRITY COMPETITIOC. COCTESTACTS ARE PRESECTEQ GITH A SET OF
CHALLECGES GHICH TEST THEIR CREATIWITY, TECHCICAL (ACQ GOOGLICG) SVILLS, ACQ PROBLEM-SOLWICG ABILITY. CHALLECGES NSNALLY COWER
A CNMBER OF CATEGORIES, ACQ GHEC SOLWEQ, EACH YIELQS A STRICG (CALLEQ A FLAG) GHICH IS SNBMITTEQ TO AC OCLICE SCORICG SERWICE.
CTFS ARE A GREAT GAY TO LEARC A GIQE ARRAY OF COMPNTER SECNRITY SVILLS IC A SAFE, LEGAL ECWIROCMECT, ACQ ARE HOSTEQ ACQ PLAYEQ
BY MACY SECNRITY GRONPS ARONCQ THE GORLQ FOR FNC ACQ PRACTICE.

FOR THIS PROBLEM, THE FLAG IS: PICOCTF{FR3UN3CCY_4774CV5_4R3_C001_7AA384BC}
```
that indicated that I was close. So I kept substituting further with the intention to get the sample text completely correct. Finally I got this result - 

```
CTFS (SHORT FOR CAPTURE THE FLAG) ARE A TYPE OF COMPUTER SECURITY COMPETITION. CONTESTANTS ARE PRESENTED WITH A SET OF
CHALLENGES WHICH TEST THEIR CREATIVITY, TECHNICAL (AND GOOGLING) SKILLS, AND PROBLEM-SOLVING ABILITY. CHALLENGES USUALLY COVER
A NUMBER OF CATEGORIES, AND WHEN SOLVED, EACH YIELDS A STRING (CALLED A FLAG) WHICH IS SUBMITTED TO AN ONLINE SCORING SERVICE.
CTFS ARE A GREAT WAY TO LEARN A WIDE ARRAY OF COMPUTER SECURITY SKILLS IN A SAFE, LEGAL ENVIRONMENT, AND ARE HOSTED AND PLAYED
BY MANY SECURITY GROUPS AROUND THE WORLD FOR FUN AND PRACTICE.

FOR THIS PROBLEM, THE FLAG IS: PICOCTF{FR3UU3NCY_4774CK5_4R3_C001_7AA384BC}
```

However, even after I got this, I was getting the wrong flag - so I began troubleshooting. Whichever plain text to code text unit repeated, I removed them and checked whether any letter had two codes (which would obviously be wrong) and to check that every letter was accounted for. 

Based off that analysis, I found that there were 4 letters unaccounted for from the sample text - `j, q, x and z`. The potential letters were `f, i, p and u`. There were 24 combinations. I could brute force these but the flag I got had only one of these coded letters - u. I just had to try out 4 values and therefore 4 flags to see which one would be correct. With trial and error, I got the flag which was - `PICOCTF{FR3QU3NCY_4774CK5_4R3_C001_7AA384BC}`.