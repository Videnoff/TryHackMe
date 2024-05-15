**Mounting the Filesystem**

In this section, we will begin to review how to mount the file system. Note, if you are doing this with any other file system, not in the Little Endian format, you must convert it from Big Endian to Little Endian using a tool called jffs2dump. But here is a reasonably concise guide to mounting the filesystem:

Step 1. If /dev/mtdblock0 exists, remove the file/directory and re-create the block device

```
rm -rf /dev/mtdblock0
```

```
mknod /dev/mtdblock0 b 31 0
```

Step 2. Create a location for the jffs2 filesysystem to live  

```
mkdir /mnt/jffs2_file/
```

Step 3. Load required kernel modules

```
modprobe jffs2
```

```
modprobe mtdram
```

```
modprobe mtdblock
```

Step 4. Write image to /dev/mtdblock0  

```
dd if=/opt/Dumping-Router-Firmware-Image/_FW_WRT1900ACSV2_2.0.3.201002_prod.img.extracted/600000.jffs2 of=/dev/mtdblock0
```

![[Pasted image 20240512093556.png]]

Step 5. Mount file system to folder location

```
mount -t jffs2 /dev/mtdblock0 /mnt/jffs2_file/
```

Step 6. Lastly, move into the mounted filesystem.

```
cd /mnt/jffs2_file/
```

![[Pasted image 20240512101406.png]]

![[Pasted image 20240512101417.png]]


To explain a little bit of what the command does, we're creating a block device (mtdblock ([Memory Technology Device](https://en.wikipedia.org/wiki/Memory_Technology_Device))) that will allow us to dump the flash memory. We're first removing it if it exists, and then re-creating it.  

  

Next, we're creating a location for our [jffs2](https://en.wikipedia.org/wiki/JFFS2) file to be mounted to.

  

After that, we're loading some kernel modules that will allow us to interact with the jffs2 file system and dump the flash memory.

  

Next, we write the file system to the block device, and after that we mount the mtdblock device which now contains the flash memory of the file system. 

  

Lastly, executing

```
cd /mnt/jffs2_file/ 
```

we are now sitting inside the router's dumped firmware and can begin the investigation.

Answer the questions below

Running an ls -la reveals a lot of interesting information. First, we notice that many files are symbolically linked (similar to a shortcut). 

| Question                    | Answer      |
| --------------------------- | ----------- |
| Where does linuxrc link to? | bin/busybox |

![[Pasted image 20240512101718.png]]


| Question                                         | Answer |
| ------------------------------------------------ | ------ |
| What parent folder do mnt, opt, and var link to? | /tmp/  |

![[Pasted image 20240512101826.png]]


| Question                                          | Answer |
| ------------------------------------------------- | ------ |
| What folder would store the router's HTTP server? | /www/  |



Scanning through a lot of these folders, you may begin to notice that they are empty. This is extremely strange, but that is because the router is not up and running. Remember, we are merely looking at a template of the filesystem that will be flashed onto the router, not the firmware from a router that has been dumped. Other information about the router may be contained in the previous section within the 6870 block.

  

The first of the folders that aren't empty is /bin/; where do a majority of the files link to?

| Question                                                                                                                                                                       | Answer  |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------- |
| Why is that? Well, [busybox is more or less a tool suite of common executable commands within the Unix environment](https://ubuntuforums.org/archive/index.php/t-846852.html). | busybox |

![[Pasted image 20240513103034.png]]


| Question                                                                                      | Answer  |
| --------------------------------------------------------------------------------------------- | ------- |
| Interestingly, what database would be running within the bin folder if the router was online? | sqlite3 |

![[Pasted image 20240513103339.png]]


The following notable folder of interest is /etc/. This folder contains many configuration files for the router, such as Access Point power levels regulated by certain countries. One you might recognize is the FCC (Federal Communications Commission).

| Question                                                               | Answer           |
| ---------------------------------------------------------------------- | ---------------- |
| We can even see the build date of the device. What is the build date?  | 2020-04-22 11:44 |

![[Pasted image 20240513103630.png]]


![[Pasted image 20240513103711.png]]


| Question                                                                                            | Answer   |
| --------------------------------------------------------------------------------------------------- | -------- |
| There are even files related to the SSH server on the device. What SSH server does the machine run? | dropbear |

![[Pasted image 20240513104329.png]]


| Question                                                                                                                                                                     | Answer |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ |
| We can even see the file for the media server, which company developed it? This company use to own Linksys at one point in time, which is likely why it is still being used. | Cisco  |

![[Pasted image 20240513104750.png]]

![[Pasted image 20240513104819.png]]


| Question                                                                                                | Answer   |
| ------------------------------------------------------------------------------------------------------- | -------- |
| Which file within /etc/ contains a list of standard Network services and their associated port numbers? | services |

![[Pasted image 20240513105118.png]]

![[Pasted image 20240513105201.png]]


| Question                                         | Answer          |
| ------------------------------------------------ | --------------- |
| Which file contains the default system settings? | system_defaults |

![[Pasted image 20240513105333.png]]


![[Pasted image 20240513105429.png]]


| Question                                                       | Answer       |
| -------------------------------------------------------------- | ------------ |
| What is the specific firmware version within the /etc/ folder? | 2.0.3.201002 |

![[Pasted image 20240513105547.png]]


Backing out into the JNAP folder, the JNAP API (formerly known as HNAP, the Home Network Administration Protocol) has been a potential attack vector and vulnerability in the past, which this article highlights [here](https://routersecurity.org/hnap.php). Interestingly enough, reminisce of it is still here today on Linksys devices. Going to http://<Default_Gateway>/JNAP/ on a Linksys router reveals an interesting 404. Much different than the standard 404.  

**Accessing /JNAP/**

![](https://i.imgur.com/vYy5Usa.png)

**Accessing any other invalid URI**

![](https://i.imgur.com/ASkUsj5.png)

This makes you wonder if something is still really there. If you investigate within /JNAP/modules folder back on the dumped filesystem, you will see some contents related to the device and what services it offers, some of them are firewalls, http proxies, QoS, VPN servers, uPnP, SMB, MAC filtering, FTP, etc.

  

**Side note:** If you have a Linksys router and are interested in playing around further, I found this [Github Repository](https://github.com/jakekara/jnap) for tools to interact with JNAP, I chose not to include this within the room since not everyone has access to a Linksys router. I won't go much further than exploring the File System.   

  
| Question                                                | Answer            |
| ------------------------------------------------------- | ----------------- |
| What three networks have a folder within /JNAP/modules? | guest_lan,lan,wan |

![[Pasted image 20240513110630.png]]


After the JNAP folder, lib is the only other folder with any contents whatsoever, and what's in there is standard in terms of libraries. The rest of the file system is relatively bare, leading us to this room's end.

I hope I made you all more curious about what's happening in your device; most importantly, I hope you enjoyed it. I encourage all of you to go out on your own and get your own router's Firmware, do some firmware dumping, and look at what's happening inside your device.

A room about Cable Modems may come in the future. However, Cable Modems firmware images are relatively difficult to access since they are only distributed to CMOs (Cable Modem Operators, like Charter, Xfinity, Cox, etc.)