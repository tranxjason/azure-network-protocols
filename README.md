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

![image alt](https://github.com/tranxjason/Azure/blob/main/rd1.jpg)
Using Remote Desktop Connection, I connect to the Windows VM using its public IP address. From there, I installed Wireshark in order to begin inspecting traffic.

![image alt](https://github.com/tranxjason/Azure/blob/main/rd2.jpg)
Within Wireshark, I filtered for ICMP (Internet Control Message Protocol) traffic and opened PowerShell to execute a command called ping. Ping utilizes ICMP, which is used by devices in a network to communicate problems within data transmition. I used ping to see if I can communicate with the Ubuntu VM using its private IP address and with google.com. Afterwards, I used a perpetual ping to the Ubuntu VM in order to see how network security groups work. I executed the perpetual ping with the command: ping -t (ip address).
