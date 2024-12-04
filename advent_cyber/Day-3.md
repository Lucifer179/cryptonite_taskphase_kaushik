For this challenge, I was briefed on RCE (Remote Control Execution), what a web shell is, how to use a log analysis tool named Kibana and how to use an RCE. I had to use this knowledge to attack a random website and analyze the attack on Kibana.

### Red Team
First, I went onto the website given (frostypines.thm) and tried looking for places I could upload a file to put in my script `shell.php` which contained the RCE. I logged in and out multiple times and searched around for the option to upload a profile picture. Since there wasn't one and there weren't any other places I could upload a file, I was trying to log in through admin. 

After trying a few times, I realized I can simply go to the admin page as they had demonstrated so I directly went to `frostypines.thm/admin` which worked. From there, I had the option to edit and add rooms. 

I added a room with the room's picture being the `shell.php` file. I then went on to the regular user and looked at the rooms. I went into the inspect tool and found where the file was located - `/media/images/rooms/shell.php`. I executed this file by going to the url `http://frostypines.thm/media/images/rooms/shell.php` following it with `?command=pwd`. This successfully excecuted the RCE and launched a web shell for me to execute commands from. 

I catted `flag.txt` and got the flag - `THM{Gl1tch_Was_H3r3}`.

### Blue Team

I went to Kibana, set the required date and time range and analyzed the logs. Initially, I tried searching through the logs with the method mentioned in the challenge where I analyze the time period with the most traffic from the IP with the most logs. I tried that IP in the answer anyway and it was wrong so I excluded it in search using `clientip` and started looking again. 

I knew that I was looking for a "GET" request with some parameters following it. In this case I knew to look for `shell.php` as a keyword directly but I didn't want to do that as that sort of defeats the point. Eventually, I did find the script I had uploaded and therefore the IP from which I did so - 10.11.83.34.