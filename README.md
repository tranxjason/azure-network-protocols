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

![rd2](https://github.com/user-attachments/assets/9bb3d9b4-e8cb-43e2-a141-19485ba5c69f)

Within the Azure portal, I opened the networking settings for the Ubuntu VM and added an inbound security rule to block ICMP traffic. I make sure to have the priority higher than SSH (300) to ensure the rule applies first.

![network setting](https://github.com/user-attachments/assets/06f6d67b-6a73-47fa-98d2-fdf7a25543bf)

Upon returning to the Windows VM, I notice that the ICMP traffic is blocked now that the inbound security rule is in place. After changing the rule to allow traffic again, the perpetual ping resolves without timing out.

![icmp](https://github.com/user-attachments/assets/5269ccd7-6792-412c-a61d-34480dc61bea)

Next, I chose to examine SSH traffic. I logged in to the Ubuntu server via PowerShell with the ssh command. With Wireshark, I filtered the traffic with tcp.port == 22. While logged into the Ubuntu server, my session is logged in Wireshark with each command I use.

![ssh](https://github.com/user-attachments/assets/5c7915ae-80cf-4825-8da4-71763865653e)

After examining SSH traffic, I exited the Ubuntu server in order to filter for DHCP traffic. To see it in action, I decided to attempt to issue a new IP address from my VM. The command ipconfig /renew will attempt to issue the new IP address and will temporarily disconnect me for a few seconds. After reconnecting, the resulting traffic is shown in Wireshark.

![dhcp](https://github.com/user-attachments/assets/ee17eb6b-8dea-4b53-81b7-0388554b7f88)

To observe DNS traffic, I used the filter udp.port == 53 and the command nslookup. I wanted to see the results that are from looking up google.com and disney.com, two very popular sites.

![udp port 53](https://github.com/user-attachments/assets/e16455a0-8ee6-4484-b49e-926c7d2085b2)

To finish my lab, I decided to observe RDP traffic. The filter for Wireshark is tcp.port == 3389. There is non-stop traffic because RDP is constantly showing me a live stream from one computer to another (in my case, my computer accessing the VM that is hosted on Azure) and thus traffic is always transmitted.

![tcp 3389](https://github.com/user-attachments/assets/dfd1d8ec-670f-4245-a12e-a3312f26a990)

<h2>Lessons Learned</h2>
This project strengthened my understanding of cloud networking and security by configuring Azure NSGs and analyzing real-time traffic with Wireshark. I gained hands-on experience with key protocols (ICMP, SSH, DNS, DHCP, RDP) and learned how security rules impact network communication. It also improved my troubleshooting skills through protocol filtering and traffic analysis.
