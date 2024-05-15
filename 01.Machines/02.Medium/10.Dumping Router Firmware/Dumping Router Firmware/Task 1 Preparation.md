**Installing the Required Software**

Each year millions of home routers are sold to consumers; a large majority of them don't even know what's running on them. Today we're going to take a look. Before proceeding, we will need a few tools:  

- Access to a Linux distribution (Or WSL) with strings and binwalk on it.
- Linksys WRT1900ACS v2 Firmware found here: [https://github.com/Sq00ky/Dumping-Router-Firmware-Image/](https://github.com/Sq00ky/Dumping-Router-Firmware-Image/)[](https://www.linksys.com/us/support-article?articleNum=165487)
- Lastly, [ensure binwalk has JFFS2 support with the following command](https://github.com/ReFirmLabs/binwalk/blob/master/INSTALL.md):

```
sudo pip install cstruct; 
```

```
git clone https://github.com/sviehb/jefferson;
```

```
cd jefferson && sudo python setup.py install
```

After you've got the tools, you're ready to set up your workspace!  

**Rebuilding the Firmware**

First, we're going to clone the repository that holds the firmware:

```
git clone https://github.com/Sq00ky/Dumping-Router-Firmware-Image/ /opt/Dumping-Router-Firmware && cd /opt/Dumping-Router-Firmware/
```

Next, we're going to unzip the **multipart zip file**:

```
7z x ./FW_WRT1900ACSV2_2.0.3.201002_prod.zip
```

running `ls` you should see the firmware image:

```
FW_WRT1900ACSV2_2.0.3.201002_prod.img
```

 Lastly, running a `sha256sum`  on the firmware image you should be left with the value **dbbc9e8673149e79b7fd39482ea95db78bdb585c3fa3613e4f84ca0abcea68a4**

![](http://puu.sh/HqCnb/5679ac9da1.png)  

Answer the questions below

Download the firmware and get your work space setup!
