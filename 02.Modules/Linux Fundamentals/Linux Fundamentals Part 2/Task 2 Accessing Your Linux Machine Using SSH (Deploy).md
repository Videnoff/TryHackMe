The in-browser functionality was used in [Linux Fundamentals Part 1](https://tryhackme.com/room/linuxfundamentalspart1) to get you directly connected to your first ever Linux machine without any hassle.

In fact, the in-browser functionality uses the exact same protocol that we are going to be using today. This protocol is called **S**ecure **S**hell or **SSH** for short and is the common means of connecting to and interacting with the command line of a remote Linux machine.

We will be deploying two machines in this room:

- Your Linux machine
- The TryHackMe AttackBox

**What is SSH & how Does it Work?**

Secure Shell or SSH simply is a protocol between devices in an encrypted form. Using cryptography, any input we send in a human-readable format is encrypted for travelling over a network -- where it is then unencrypted once it reaches the remote machine, such as in the diagram below.

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5c549500924ec576f953d9fc/room-content/154f110d35efe47d493df29cdb773109.svg)  

You can learn about the various types of encryption on a TryHackMe room. But for now, we only need to understand that:  

- SSH allows us to remotely execute commands on another device remotely.
- Any data sent between the devices is encrypted when it is sent over a network such as the Internet

**Deploying Your Linux Machine  
**

Press the green "Start Machine" button on the top-right of this task and then scroll to the top of the page to see the deployment information like so:

![](https://assets.tryhackme.com/additional/linux-fundamentals/part2/deploy1.png)

The IP address displayed is the address of your Linux machine that you will be logging into using SSH. Take note of this for now.

  

Deploying the TryHackMe AttackBox

Looking at the top of the page, press the "Start AttackBox" button to deploy the TryHackMe AttackBox that we will be interacting with. The TryHackMe AttackBox is a Ubuntu Linux machine that is hosted online in the cloud and can be interacted with via your browser. You will be using this to interact with the machine that you deploy in this task.  

  

![](https://assets.tryhackme.com/additional/linux-fundamentals/part2/ab1.png)

  

  

**Using SSH to Login to Your Linux Machine**

The syntax to use SSH is very simple. We only need to provide two things:

1. The IP address of the remote machine

2. Correct credentials to a valid account to login with on the remote machine

  

For this room, we will be logging in as "tryhackme", whose password is "tryhackme" without the quotation ("") marks. Let's use the IP address of the machine displayed in the card at the top of the room as the IP address and this user, to construct a command to log in to the remote machine using SSH. The command to do so is `ssh` and then the username of the account, `@` the IP address of the machine.

But first, we need to open a terminal on the TryHackMe AttackBox. There is an icon placed on the desktop named "Terminal". And now, we can proceed to input commands.

For example: `ssh tryhackme@MACHINE_IP`  . Replacing the IP address with the IP address for your Linux target machine. Once executed, we will then be asked to trust the host and then provide a password for the "**tryhackme**" account, which is also "**tryhackme**".  

![](https://assets.tryhackme.com/additional/linux-fundamentals/part2/ab2.png)

Now that we are connected, any commands that we execute will now execute on the remote machine -- not our own.

_**Note:** When you type a password into an ssh login prompt there is no visible feedback -- you will not be able to see any text or symbols appear as you type the password. It is still working, however, so just type the password and press enter to login.  
_

Answer the questions below

I've logged into the Linux Fundamentals Part 2 machine using SSH!