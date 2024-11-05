### Challenge
For this challenge, I was given a checksum and had to find and decrypt the file containing the encrypted flag using the `./decrypt.sh files/<file>` command.

After logging into the picoctf user, I listed all the files present. I first confirmed whether `checksum.txt` was the same one provided in the challenge - it was. After that I catted `decrypt.sh` to understand how the shell script would decrypt the required file in the hope that it would provide me a clue in the process. Indeed it did, and the clue was to look inside the `files` directory. 

I cd'd to the `files` directory and listed all the files and piped it with grep to find any file that ends or starts with the characters that the checksum does since I read that a hash can be verified visually by looking at the first and last four characters of a string. That didn't work because the string was inside the files themselves and not in their names.

In hint 2 of the challenge, it was said that a sha checksum can be created using the `sha256sum <directory>/*` command for a directory. I created a sha checksum for the files directory and that gave me a list of all the checksums for each file in that directory. I ran that command again but this time grepping with the checksum provided to us in the challenge (in `checksum.txt`) with the following command: `sha256sum files/* | grep b09c99c555e2b39a7e97849181e8996bc6a62501f0149c32447d8e65e205d6d2`.

The output of this was `b09c99c555e2b39a7e97849181e8996bc6a62501f0149c32447d8e65e205d6d2  files/451fd69b`, meaning that `files/451fd69b` contained the encrypted flag.

I catted `files/451fd69b` to read the encrypted flag which instead launched a new user shell. In that I ran `./decrypt.sh files/451fd69b` which gave me the final decrypted flag - `picoCTF{trust_but_verify_451fd69b}`.
#
### References
I referred to [Hashing Functions](https://ctf101.org/cryptography/what-are-hashing-functions) for understanding SHA hash.