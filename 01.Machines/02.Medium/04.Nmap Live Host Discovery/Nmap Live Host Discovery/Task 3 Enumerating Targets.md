We mentioned the different _techniques_ we can use for scanning in Task 1. Before we explain each in detail and put it into use against a live target, we need to specify the targets we want to scan. Generally speaking, you can provide a list, a range, or a subnet. Examples of target specification are:

- list: `MACHINE_IP scanme.nmap.org example.com` will scan 3 IP addresses.
- range: `10.11.12.15-20` will scan 6 IP addresses: `10.11.12.15`, `10.11.12.16`,… and `10.11.12.20`.
- subnet: `MACHINE_IP/30` will scan 4 IP addresses.

You can also provide a file as input for your list of targets, `nmap -iL list_of_hosts.txt`.

If you want to check the list of hosts that Nmap will scan, you can use `nmap -sL TARGETS`. This option will give you a detailed list of the hosts that Nmap will scan without scanning them; however, Nmap will attempt a reverse-DNS resolution on all the targets to obtain their names. Names might reveal various information to the pentester. (If you don’t want Nmap to the DNS server, you can add `-n`.)

Launch the AttackBox using the Start AttackBox button, open the terminal when the AttackBox is ready, and use Nmap to answer the following.

Answer the questions below

| Question | Answer |
| ---- | ---- |
| What is the first IP address Nmap would scan if you provided `10.10.12.13/29` as your target? | 10.10.12.13/29 |

```
nmap -sL 10.10.12.13/29
```

![[Pasted image 20240217101229.png]]

| Question | Answer |
| -------- | ------ |
| How many IP addresses will Nmap scan if you provide the following range `10.10.0-255.101-125`?         | 6400       |
```
nmap 10.10.0-255.101-125
```

