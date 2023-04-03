# azure-network-protocols
<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Step 1 Create a Resource Group & Two Virtual Machines
- Step 2 Observe ICMP traffic
- Step 3 Observe SSH  traffic
- Step 4 Observe DHCP traffic
- Step 5 Observe DNS  traffic
- Step 6 Observe RDP  traffic

<h2>Actions and Observations</h2>
<p>The first step is to create a Resource Group to organize my resources.</p>
<img src="https://i.imgur.com/oFsPcWz.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p>Next, create two Virtual Machines:</p>
<ol>
    <li>Create a Windows 10 VM and place it in the (NetworkRG_lab) Resource Group created.</li>
    <li>Create a Linux Ubuntu VM and also place it in (NetworkRG_lab) Resource Group & Virtual Network.</li>
</ol>
<img src="https://i.imgur.com/mOhQ7Dh.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p>Check your Virtual Network in Network Watcher to ensure it is set up correctly.</p>
<img src="https://i.imgur.com/MhQiy3r.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p>Next, we are going to observe some ICMP traffic. But first, we must use Remote Desktop to connect to our Windows 10 Virtual Machine and install Wireshark.</p>
<img src="https://i.imgur.com/9lJekFy.png" height="25%" width="25%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/arpa02s.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>
<p>After opening Wireshark and filtering for ICMP traffic, retrieve the private IP address (10.0.0.5) of the Ubuntu VM and attempt to ping it from within the Windows 10 VM using Powershell.</p>
<img src="https://i.imgur.com/HeLJFSi.png" height="80%" width="80%" alt="Disk Sanitization Steps"/><br />
<p>Next, go to Network Security Group for the Ubuntu VM in the Azure portal and disable incoming ICMP traffic.</p>
<img src="https://i.imgur.com/6fRJX9x.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p>Now go back to Wireshark and use Powershell to try and Ping the VM, and you will see that the "request timed out" on Powershell and you get a "no response" on Wireshark whereas before you would have gotten a "reply".</p>
<img src="https://i.imgur.com/oHlujo4.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p>Next, let's observe SSH traffic. To do so, filter for SSH traffic in Wireshark. Next, SSH into your Ubuntu VM from your Windows 10 VM using its private IP address (10.0.0.5), type in some commands, and observe the traffic on Wireshark.</p>
<br />
<img src="https://i.imgur.com/8IMPpBh.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/rTJpXRC.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p>Now, let's filter for DHCP traffic in Wireshark. Then, attempt to issue your VM a new IP address from the command line (using ipconfig /renew) on the Windows 10 VM and observe the resulting DHCP traffic in Wireshark.</p>
<img src="https://i.imgur.com/zQTh7De.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p>To observe DNS traffic, filter for DNS traffic in Wireshark. Then, on your Windows 10 VM command line, use nslookup to see the IP addresses of google.com. After that, observe the DNS traffic displayed in Wireshark.
<br />
<img src="https://i.imgur.com/K8Wa8tt.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

</p>
<p>
Finally, to observe RDP traffic, filter for RDP traffic in Wireshark using the tcp.port == 3389 filter. Observe the continuous stream of traffic being displayed. The reason for the non-stop spam of traffic is that the RDP protocol continuously streams data from one computer to another, meaning traffic is always being transmitted.
<img src="https://i.imgur.com/mSrHSKd.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
















