Why crack a password hash when you can authenticate using the hash?

Use the full admin hash with pth-winexe to spawn a shell running as admin without needing to crack their password. Remember the full hash includes both the LM and NTLM hash, separated by a colon:

```
pth-winexe -U 'admin%hash' //10.10.212.141 cmd.exe
```

Answer the questions below

Read and follow along with the above.
