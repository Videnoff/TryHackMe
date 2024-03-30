Can you complete the level 1 tasks by cracking the hashes?

Answer the questions below

| Question                         | Answer | SS                                   |
| -------------------------------- | ------ | ------------------------------------ |
| 48bb6e862e54f2a795ffc4e541caed4d | easy   | ![[Pasted image 20240318193110.png]] |
```
hashcat -a 0 -m 0 1.txt /usr/share/wordlists/rockyou.txt
```


| Question                                 | Answer      | SS                                   |
| ---------------------------------------- | ----------- | ------------------------------------ |
| CBFDAC6008F9CAB4083784CBD1874F76618D2A97 | password123 | ![[Pasted image 20240318193856.png]] |
*Save the hash to file*
```
echo 'CBFDAC6008F9CAB4083784CBD1874F76618D2A97' > 2.txt
```

*Check the hash type*
```
hashid 2.txt
```
![[Pasted image 20240318193700.png]]

*Crack the hash*
```
hashcat -a 0 -m 100 2.txt /usr/share/wordlists/rockyou.txt
```

| Command | Description  |
| ------- | ------------ |
| -a      | 0 (Straight) |
| -m      | 100 (SHA1)   |


| Question                                                         | Answer  | SS                                   |
| ---------------------------------------------------------------- | ------- | ------------------------------------ |
| 1C8BFE8F801D79745C4631D09FFF36C82AA37FC4CCE4FC946683D7B336B63032 | letmein | ![[Pasted image 20240318195040.png]] |
*Save the hash to file*
```
echo '1C8BFE8F801D79745C4631D09FFF36C82AA37FC4CCE4FC946683D7B336B63032' > 3.txt
```  

*Check the hash type*
```
hashid 3.txt
```
![[Pasted image 20240318194913.png]]

*Crack the hash*
```
hashcat -a 0 -m 1400 3.txt /usr/share/wordlists/rockyou.txt
```


| Question                                                     | Answer | SS                                   |
| ------------------------------------------------------------ | ------ | ------------------------------------ |
| $2y$12$Dwt1BZj6pcyc3Dy1FWZ5ieeUznr71EeNkJkUlypTsgbX1H68wsRom | bleh   | ![[Pasted image 20240318201519.png]] |
*Filter only 4-letter words from rockyou.txt:*
```
grep -E '^.{4}$' /usr/share/wordlists/rockyou.txt | hashcat -m 3200 4.txt
```


| Question                         | Answer     | SS  |
| -------------------------------- | ---------- | --- |
| 279412f945939ba78ce0758d3fd83daa | Eternity22 |     |
```
hashcat -m 900 5.txt /usr/share/wordlists/rockyou.txt
```
