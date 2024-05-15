**One Inch Deep Analysis**

In this section we will be taking a look at the firmware, checking for strings and, dump the file system from the image. The next section will cover mounting and exploring the file system.

Answer the questions below


While running strings on the file, there is a lot of notable clear text. This is due to certain aspects of the firmware image not being encrypted. This likely means that with Binwalk, we can dump the firmware from the image.

  
| Question                                                                  | Answer                    |
| ------------------------------------------------------------------------- | ------------------------- |
| What does the first clear text line say when running strings on the file? | Linksys WRT1900ACS Router |
![[Pasted image 20240511225427.png]]


| Question                                                          | Answer |
| ----------------------------------------------------------------- | ------ |
| Also, using strings, what operating system is the device running? | Linux  |


Scrolling through with strings, you may notice some other interesting lines like 

/bin/busybox

and various other lua files. It really makes you wonder what's going on inside there.

Next, we will be dumping the filesystem from the image file. To do so, we will be using a tool called binwalk.

Binwalk is a tool that checks for well-known file signatures within a given file. This can be useful for many things; it even has its uses in Steganography. A file could be hidden within the photo, and Binwalk would reveal that and help us extract it. We will be using it to extract the filesystem of the router in this instance.

| Question                                                                           | Answer |
| ---------------------------------------------------------------------------------- | ------ |
| What option within Binwalk will allow us to extract files from the firmware image? | -e     |

![[Pasted image 20240511225905.png]]


| Question                                                                                               | Answer        |
| ------------------------------------------------------------------------------------------------------ | ------------- |
| Now that we know how to extract the contents of the firmware image, what was the first item extracted? | uImage header |

![[Pasted image 20240512085545.png]]


```
sudo binwalk -e FW_WRT1900ACSV2_2.0.3.201002_prod.img --run-as=root
```


| Question                    | Answer              |
| --------------------------- | ------------------- |
| What was the creation date? | 2020-04-22 11:07:26 |

![[Pasted image 20240512085545.png]]


The Cyclical Redundancy Check is used similarly to file hashing to ensure that the file contents were not corrupted and/or modified in transit.

  
| Question                          | Answer     |
| --------------------------------- | ---------- |
| What is the CRC of the **image**? | 0xABEBC439 |



| Question                | Answer        |
| ----------------------- | ------------- |
| What is the image size? | 4229755 bytes |

| Question                               | Answer |
| -------------------------------------- | ------ |
| What architecture does the device run? |        |

| Question                                              | Answer |
| ----------------------------------------------------- | ------ |
| Researching the results to question 10, is that true? | Yes    |


You will notice two files got extracted, one being the jffs2 file system and another that Binwalk believes in gzipping compressed data.

![[Pasted image 20240512085920.png]]

![[Pasted image 20240512085931.png]]

![[Pasted image 20240512085942.png]]

You can attempt to extract the data, but you won't get anywhere. Binwalk misinterpreted the data. However, we can still do some analysis of it.

  
| Question                                                                                                                                                                                                                                    | Answer |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ |
| Running strings on 6870, we notice a large chunk of clear text. We can actually rerun binwalk on this file to receive even more files to investigate. Interestingly enough, a copy of the Linux kernel is included. What version is it for? |        |
```
sudo binwalk -e 6870 --run-as=root
```

![[Pasted image 20240512090515.png]]



| Question                                                                                                                                                                                                                                                                                                                                                                              | Answer           |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- |
| Suppose you extract the contents of 6870 with Binwalk and run strings on 799E38.cpio, you may see a lot of hex towards the bottom of the file. Some of it can be translated into human-readable text. Some of it is interesting and makes you wonder about its purpose. Some additional investigation may reveal its purpose. I will leave you to explore that on your own, though :) | No answer needed |


| Question                                                                                                                                                 | Answer           |
| -------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- |
| Continuing with the analysis, we have a jffs2 file system that we can examine the contents of. First, we must mount it, bringing us to the next section. | No answer needed |
