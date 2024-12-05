For this challenge, I had to run a test on a mimic ransomware for the purpose of understanding how to mitigate it by understanding what it does. By analyzing the results of the test, we can know the keywords to look for with this type of attack.

### The Att&ck Technique

I first had to figure out which MITRE Att&ck technique to apply in this case. They mentioned it requires a test that takes advantage of a command and scripting interpreter which would've directly given me the answer but I instead looked around for tests that relate to ransomware and found the same one anyway - Command and Scripting Interpreter (T1059). Under that we needed the Windows Powershell subtechnique (T1059.003).

### Test Number to be stimulated

Had I not overthought it, I would have recognized that they are simply asking us to run a single test, which is test number 4 that mimics BlackByte ransomware, and not all of the tests under that subtechnique. I ran the first couple of them based off what I read in the challenge prior to the practical application and tried to find the flag and the required flag. I didn't (because that wasn't what I was supposed to do anyway) then I started running all of the tests. I went through the logs after running all of them and realized that I only have to look into test number 4 anyway as I wasn't finding any files by use of the Events Viewer that I could simply cat to get the flag and test number 4 downloads a pdf file.

After opening the pdf, I got the flag - `THM{R2xpdGNoIGlzIG5vdCB0aGUgZW5lbXk=}`.

I also had to determine the name of the file used in the test. I knew from the logs in the Events Viewer that it has to be `Wareville_Ransomware.txt`. However, it came as the wrong answer when I put it in. The format of the answer didn't reflect the file type I was getting anyway so I tried multiple other files I found in the logs after running only the 4th test to hone down on which files to look at. After a _very_ long time, I figured it _has_ to be `Wareville_Ransomware.txt` so I tried it again and it worked this time. Turns out all that time was wasted over a typo I must have made while inputting the answer earlier.