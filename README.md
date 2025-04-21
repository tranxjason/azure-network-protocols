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
