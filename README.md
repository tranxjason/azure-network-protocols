<p align="center">
  <img src="https://github.com/tranxjason/Azure/blob/main/nsg%20azure.jpg"/>
</p>

<h1>Inspecting Network Protocols & Network Security Groups (NSGs)</h1>
In this lab, I observe various network traffics to and from Azure Virtual Machines with Wireshark as well as experiment with network security groups. 
<br />

<h2>Environment and Technologies Used</h2>

- <b>Microsoft Azure (Virtual Machines/Compute)</b> 
- <b>Remote Desktop Connection</b>
- <b>Command-Line Tools</b>
- <b>Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)</b>
- <b>Wireshark (Protocol Analyzer)</b>

<h2>Operating Systems Used</h2>

- <b>Windows 10 Pro</b> 
- <b>Ubuntu Server 20.04</b>

<h2>The Set-Up</h2>
Within Azure, I created two VMs within the same virtual network to ensure they are able to communicate with each other. One VM will have Windows 10 Pro while the other uses Ubuntu. The Windows VM will connect to the other via the command line/Powershell

<h2>Actions and Observations</h2>

Using Remote Desktop Connection, I connect to the Windows VM using its public IP address. From there, I installed Wireshark in order to begin inspecting traffic.

![rd1](https://github.com/user-attachments/assets/f095fc03-68ed-4765-8c24-40e0f98bea76)

Within Wireshark, I filtered for ICMP (Internet Control Message Protocol) traffic and opened PowerShell to execute a command called ping. Ping utilizes ICMP, which is used by devices in a network to communicate problems within data transmition. I used ping to see if I can communicate with the Ubuntu VM using its private IP address and with google.com. Afterwards, I used a perpetual ping to the Ubuntu VM in order to see how network security groups work. I executed the perpetual ping with the command: ping -t (ip address).

![image alt](https://github.com/tranxjason/Azure/blob/main/rd2.jpg)

Within the Azure portal, I opened the networking settings for the Ubuntu VM and added an inbound security rule to block ICMP traffic. I make sure to have the priority higher than SSH (300) to ensure the rule applies first.

![image alt](https://github.com/tranxjason/Azure/blob/main/network%20setting.jpg)

Upon returning to the Windows VM, I notice that the ICMP traffic is blocked now that the inbound security rule is in place. After changing the rule to allow traffic again, the perpetual ping resolves without timing out.

![image alt](https://github.com/tranxjason/Azure/blob/main/icmp.jpg)

Next, I chose to examine SSH traffic. I logged in to the Ubuntu server via PowerShell with the ssh command. With Wireshark, I filtered the traffic with tcp.port == 22. While logged into the Ubuntu server, my session is logged in Wireshark with each command I use.

![image alt](https://github.com/tranxjason/Azure/blob/main/ssh.jpg)

After examining SSH traffic, I exited the Ubuntu server in order to filter for DHCP traffic. To see it in action, I decided to attempt to issue a new IP address from my VM. The command ipconfig /renew will attempt to issue the new IP address and will temporarily disconnect me for a few seconds. After reconnecting, the resulting traffic is shown in Wireshark.

![dhcp](https://github.com/user-attachments/assets/ee17eb6b-8dea-4b53-81b7-0388554b7f88)
