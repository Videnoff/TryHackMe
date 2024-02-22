Let’s revisit the TCP/IP layers shown in the figure next. We will leverage the protocols to discover the live hosts. Starting from bottom to top, we can use:

- ARP from Link Layer
- ICMP from Network Layer
- TCP from Transport Layer
- UDP from Transport Layer

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/745e0412b319d324352c7b29863b74f4.png)

Before we discuss how scanners can use each in detail, we will briefly review these four protocols. ARP has one purpose: sending a frame to the broadcast address on the network segment and asking the computer with a specific IP address to respond by providing its MAC (hardware) address.

ICMP has [many types](https://www.iana.org/assignments/icmp-parameters/icmp-parameters.xhtml). ICMP ping uses Type 8 (Echo) and Type 0 (Echo Reply).

If you want to ping a system on the same subnet, an ARP query should precede the ICMP Echo.

Although TCP and UDP are transport layers, for network scanning purposes, a scanner can send a specially-crafted packet to common TCP or UDP ports to check whether the target will respond. This method is efficient, especially when ICMP Echo is blocked.

If you have closed the network simulator, click on the “View Site” button in Task 2 to display it again.

Answer the questions below

Send a packet with the following:

- From computer1
- To computer3
- Packet Type: “Ping Request”

![[Pasted image 20240217121325.png]]
![[Pasted image 20240217121817.png]]


| Question                                                                               | Answer       |
| -------------------------------------------------------------------------------------- | ------------ |
| What is the type of packet that computer1 sent before the ping?                        | ARP Request  |
| What is the type of packet that computer1 received before being able to send the ping? | ARP Response |
| How many computers responded to the ping request?                                                                                         | 1             |

Send a packet with the following:

- From computer2
- To computer5
- Packet Type: “Ping Request”

![[Pasted image 20240217122001.png]]
![[Pasted image 20240217122043.png]]

| Question                                                                       | Answer    |
| ------------------------------------------------------------------------------ | --------- |
| What is the name of the first device that responded to the first ARP Request?  | router    |
| What is the name of the first device that responded to the second ARP Request? | computer5 |
| Send another Ping Request. Did it require new ARP Requests? (Y/N)                                                                               | N          |
