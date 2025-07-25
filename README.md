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
<h3> Step 1: Using Remote Desktop to connect to the VM & Installing Wireshark </h3>

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

</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/b22db5ba-86dc-444d-9b12-c2b945b3a39b" width=800/>
</p>
<p>

  - Within the VM, I installed a program called "Wireshark".
  - "Wireshark" is a free network packet analyzer that captures and inspects data packets traveling through a network.

</p>
<br />

<h3> Step 2: Observing ICMP Traffic </h3>

<p>
<img src="https://github.com/user-attachments/assets/2f7dc07e-78e4-418c-8286-a0419ceb98d7" width=800 />
</p>
<p>

  - Within Wireshark, I highlighted "Ethernet" and selected the blue shark fin in the top left corner to begin network inspection.

</p>
<br /

<p>
<img src="https://github.com/user-attachments/assets/68ef93ab-d493-4e5d-a4fa-5d7bb51575eb" width=800 />
</p>
<p>

  - After clicking the blue fin, Wireshark began to display all of the network traffic that is happening inside of the virtual machine.

 <p>
<img src="https://github.com/user-attachments/assets/a213acc4-0ef9-485f-a2ce-65ab1077f9d3" width=800 />
</p>
<p>

  - Next, I located the filter bar at the top of the screen and entered "icmp" to filter for icmp traffic only.
  - The icmp filter will be used to obeserve traffic betwen the Windows VM and the Linux VM I created in Azure.

</p>
<br /

<p>
<img src="https://github.com/user-attachments/assets/409926b8-fd7d-49cd-9881-8ffb82dd2d1c" width=800 />
</p>
<p>

  - Next, I went back into Azure to locate the Private IP address of the Linux VM.
  - The Private IP address is needed in order to ping the Linux VM within the Windows VM.

</p>
<br /

<p>
<img src="https://github.com/user-attachments/assets/1ddb4535-cbd1-4263-aab7-48eaf2109fbf" width=800 />
</p>
<p>

  - Next, I opened Windows Powershell inside of the virtual machine and entered the Private IP address of the Linux VM.

</p>
<br /

<p>
<img src="https://github.com/user-attachments/assets/fb2f79da-7ab0-45a0-878a-286aa108336a" width=800 />
</p>
<p>

  - After receiving a reply from Powershell, Wireshark is now only displaying icmp traffic over the network.
  - This means that the connection test between the two VMs was successful!

</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/0fc5cf87-4018-471c-bf79-babe451177ab" width=800 />
</p>
<p>

  - After that, I went back into Powershell and entered the command "ping 10.0.0.5 -t".
  - This command initiated a non-stop ping between the Windows VM and the Linux VM.

</p>
<br />

<h3> Step 3: Configuring a Firewall (Network Security Group) </h3>

<p>
<img src="https://github.com/user-attachments/assets/fa0ca6de-2dd2-498d-aa2c-f043d05d2890" width=800 />
</p>
<p>

  - Within the Azure portal, I selected the Linux VM and navigated to the network settings where I located the Network Security Group (NSG) for the VM.

</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/25005b8e-eb4e-4e44-8771-db4ff68d60dc" width=400 />
</p>
<p>

  - Next, I selected "Inbound Security Rules" and clicked "Add" to create a new rule for the Firewall.
  - I changed the source to "Any" and the protocol to "ICMPv4".
  - I set the action to "Deny" which will tell the Firewall to deny incoming traffic to the Linux VM.


</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/4114598d-5076-48ca-92c1-1309266ab96d" width=800 />
</p>
<p>

  - Due to the new rule that I created, any new Ping request in Powershell will time out becuase the Firewall is blocking them.

</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/f385915f-cffc-4228-8411-e49a213988c9" width=800 />
</p>
<p>

  - Next, I went back into Azure to delete the inbound security rule that I created.

</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/fa625f4e-e28d-4c05-9a4b-f4205553f8ed" width=800 />
</p>
<p>

  - After deleting the rule, Powershell and Wireshark were able to start the ping again.
  - Wireshark began to show requests and replies again while Powershell showed more replies from 10.0.0.5.





















    

