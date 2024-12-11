## JQ
Tool used for turning info from machine-readable to more digestable for humans to extract meaningful data from it.

How we can use it - A single event can have a lot of info. We can put it in a preferred format and filter for the required parameters.

## The challenge

We filter for events in the S3 bucket and start analyzing from there. Most logs are from the user "glitch" who uploaded a new png on 28th November which is when the transactions stopped going to the right account. 

McSkidy is the one who is shown to have created this user. However, we can analyze the login details of each user and see that McSkidy uses a Windows machine whereas this one used a Mac, and the IPs of all the logs from earlier don't match McSkidy's. The conclusion is that someone hacked into McSkidy's user and created the user "glitch" and gave it admin access after which the account for donations was changed to Mayor Malware's.

## Answers for the questions

What is the other activity made by the user glitch aside from the ListObject action? - PutObject

What is the source IP related to the S3 bucket activities of the user glitch? - 53.94.201.69

Based on the eventSource field, what AWS service generates the ConsoleLogin event? - signin.amazonaws.com

When did the anomalous user trigger the ConsoleLogin event? - 2024-11-28T15:21:54Z

What was the name of the user that was created by the mcskidy user? - glitch

What type of access was assigned to the anomalous user? - AdministratorAccess

Which IP does Mayor Malware typically use to log into AWS? - 53.94.201.69

What is McSkidy's actual IP address? - 31.210.15.79

What is the bank account number owned by Mayor Malware? - 2394 6912 7723 1294