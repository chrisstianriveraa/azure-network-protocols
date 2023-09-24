<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />



- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04


<h2>Actions and Observations</h2>

<p>
In this tutorial we're going to be looking at the newtwork security groups and inspecting newtwork protocols. I created two VM's on Azure, one of the machines will be operating in Linux and the other machine will be running Windows 10. Both VM's would need to be on the same VNET. After doing that, you would need to get on the Windows machine and download wireshark. Once you download wireshark, open the application and filter it so that you only see ICMP traffic. ICMP is a netwokr layer protocol that replys messages about network connection issues. We can open the cmd prompt and ping the private IP address of our linux machine, you cam see the packets on wireshark below.
<p>
<img src="https://i.imgur.com/aJ21BzT.png"/>
</p>
<p>
The next part of the tutorial, we'll be continuously ping the Linux VM with command "ping -t". As the Windows VM is pinging the Linux VM, we'll go the Linux machine and block inbound ICMP traffic in the firewall. After that is done we will no longer receive replys from the Linux machine. We can block ICMP by creating a new network security group on the Linux machine. 
</p>
<p>
 <img src="https://i.imgur.com/0UMJrqn.png"/>

 <img src="https://i.imgur.com/7J2x2qa.png"/>
</p>
<br />

<p>
We will next use the Windows machine to SSH to the Linux VM. SSH doesnt have a GUI, it gives users access to the machine CLI. We can set a filter in wireshark to only capture SSH packets. When we use ssh into the Linux machine with the command prompt "ssh labuser@10.0.0.5, we can see wireshark starts to capture ssh packets. 
</p>
<p>
<img src="https://i.imgur.com/Nasop6s.png"/>
</p>
<br />

<p>
We can then use wireshark to filter for DHCP. DHCP is Dynamic Host Configuration Protocol. It is uesd to assign IP addresses to machines. We'll request a new ip address with the command prompt "ipconfig /renew". After we enter the prompt wireshark will capture DHCP traffic.
</p>
<p>
<img src="https://i.imgur.com/TM0bkiF.png"/>
</p>

<p>
 Now it's time to filter DNS traffic. We can initiate DNS traffic by typing in the prompt "nslookup wwww.google.com" this command asks the DNS serven what is google's IP address. 
</p>
<p>
<img src="https://i.imgur.com/mtTcALd.png"/>
</p>

<br />
