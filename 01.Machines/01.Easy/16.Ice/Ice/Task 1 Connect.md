Connect to the TryHackMe network! Please note that this machine does not respond to ping (ICMP) and may take a few minutes to boot up.

  

-----------------------------------------

  

The virtual machine used in this room (Ice) can be downloaded for offline usage from [https://darkstar7471.com/resources.html](https://darkstar7471.com/resources.html). The sequel to this room, Blaster, can be found [here](https://tryhackme.com/room/blaster).

Answer the questions below

Connect to our network using OpenVPN. Here is a mini walkthrough of connecting:

Go to your [access](http://tryhackme.com/access) page and download your configuration file.

![](https://i.gyazo.com/c86eba5538466dc1d948e09b6f14b53b.png)

Use an OpenVPN client to connect. In my example I am on Linux, on the access page we have a windows tutorial.

![](https://i.gyazo.com/42083cc1831acad79e5a6fa2b235792f.png)(change "ben.ovpn" to your config file)

When you run this you see lots of text, at the end it will say Initialization Sequence Completed

You can verify you are connected by looking on your access page. Refresh the page

You should see a green tick next to Connected. It will also show you your internal IP address.

![](https://i.gyazo.com/fad648871fd0e51d1d5590d005329f1c.png)

You are now ready to use our machines on our network!

Now when you deploy material, you will see an internal IP address of your Virtual Machine.