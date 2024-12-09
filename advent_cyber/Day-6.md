The purpose of this challenge was to understand how to use YARA rules to detect malware and how to bypass these rules.

### Detecting Sandboxes

The `C:\ProgramFiles` directory is often absent in sandboxes. We can check whether it's present by searching the registry path `HKLM\\Software\\Microsoft\CurrentVersion`.

### YARA

By specifying a certain string that a malware is likely to have in its rules, YARA is able to detect the malware. The example used in this challenge was a rule that checks for any command that tries to access the aforementioned registry and stores a positive in `C:\Tools\YaraMatches.txt`. By running this rule and executing a malicious software, we can see YARA in action. This gave me the first flag - `THM{GlitchWasHere}`.


An attempt can be made at evading YARA by encoding the program. However, this can still be detected by another tool named "Floss". By running the malware through floss and piping its results into some file `C:\tools\malstrings.txt`, we can see the scanned results in that file. This is where I found the second flag - `THM{HiddenClue}`. I first searched for the keyword "Mayor Malware" as mentioned in the challenge. However, since that didn't give me the flag, I looked up "THM" instead and found it.

### Event Viewer

Sysmon is responsible for monitoring and logging system activity. We can find the event ID for `YaraMatches.txt` and filter for that in the Operational events log. There, we can find some important details of the malware - where it was located, the PID and PPID, the privileges with which the malware was run, the command that was run and the time frame it was done in.
