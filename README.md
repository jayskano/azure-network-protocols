<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
This project demonstrates how I observed various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (22H2)
- Ubuntu Server 24.04


<h2>Walkthrough</h2>
<h3> Step 1: Using Remote Desktop to connect to the Windows 10 Virtual Machine (VM) </h3>

<p>
<img src="https://github.com/user-attachments/assets/47a94f6d-db64-4d09-87b2-31a15fcc72de" width=800 />
</p>
<p>

  - In order to connect to the Windows VM, I needed to locate the Public IP address within Azure first.

</p>
<br /

<p>
<img src="https://github.com/user-attachments/assets/c8fc584f-3302-452b-b357-2ce18b141902" width=400/>
</p>
<p>

  - Next, I entered the Public IP address into Remote Desktop and clicked "Connect".

</p>
<br /

<p>
<img src="https://github.com/user-attachments/assets/f23f4b50-b708-4689-8534-d73fb328ce68" />
</p>
<p>

  - After clcking "Connect", I was prompted to enter both the Username and Password that I had previously created in Azure for the VM.

</p>
<br /

<p>
<img src="https://github.com/user-attachments/assets/94430cd5-3923-4445-b686-f8b55fe60c10" width=800 />
</p>
<p>

  - I have successfully connected to the Windows 10 Virtual Machine (VM)!
    

