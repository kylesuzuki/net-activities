<p align="center">
<img src="https://i.imgur.com/FRRLw01.png" alt="Azure logo"/>
</p>

<h1>Performing Networking Activities within Azure VMs</h1>
This beginner-friendly tutorial provides hands-on experience with Azure networking. Learn how to create a resource group with Windows 10 and Linux virtual machines, and use Wireshark to observe ICMP, SSH, DHCP, DNS, and RDP traffic. Discover network communication, disable and re-enable ICMP traffic, and explore essential networking concepts and technologies. Practice proper resource management by deleting the resource group and verifying its successful removal.<br />

<h2>List Summary</h2>

- Create a Resource Group.
- Create a Windows 10 Virtual Machine (VM).
- Create a Linux (Ubuntu) VM.
- Install Wireshark within your Windows 10 VM.
- Observe ICMP Traffic.
- Observe SSH Traffic.
- Observe DHCP Traffic.
- Observe DNS Traffic.
- Observe RDP Traffic.
- Delete the Resource Group to avoid incurring costs.
- Verify the successful deletion of the Resource Group.

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (ICMP, SSH, DHCP, DNS, RDP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>List of Prerequisites</h2>

- Active <a href="https://azure.microsoft.com/en-us/free/">Azure account (Tenant) and Subscription</a>
- Completion of <a href="https://github.com/kylesuzuki/azure-prereq">Azure Account and Storage Lab</a> (highly recommended)

<h2>Installation Steps</h2>

<h3>Create a Resource Group.</h3>
<p>
<img src="https://i.imgur.com/3Qafc6P.png" height="80%" width="80%" alt="RG Creation"/>
</p>
<p>
To create a research group in Azure, follow these steps: search for "Resource Group", click on 'Create', choose the desired subscription (e.g., Azure subscription 1), provide a name for the resource group (e.g., RG-Lab-2), select a region for its creation (e.g., West US 3), wait for validation on the "Review + create" page, click 'Create'.
</p>


<h3>Create a Windows 10 Virtual Machine (VM).</h3>
<p>
<img src="https://i.imgur.com/pbYsW8q.png" height="80%" width="80%" alt="Window VM Creation"/>
</p>
<p>
To create a Windows 10 Virtual Machine (VM) in Azure, follow these steps: search for "Virtual Machine", click on 'Create', choose "Azure virtual machine", select the desired subscription (e.g., Azure subscription 1), specify the resource group (e.g., RG-Lab-2), provide a name for the virtual machine (e.g., VM1), and select a region for its creation (e.g., West US 3).

Next, click on 'Image' and choose "Windows 10 Pro, version 21H2 - Gen2 (free services eligible)". Then, click on 'Size' and choose "Standard_E2s_v3 - 2 vcpus, 16 GiB memory ($91.98/month)". Set the desired username (e.g., labuser) and password (e.g., Password1).

Ensure the box under Licensing stating "I confirm I have an eligible Windows 10/11 license with multi-tenant hosting rights" is checked. Click 'Next' and leave the disk options as they are.

For the subnet configuration, make sure it is set to "(new) default (10.0.0.0/24)". Wait for validation on the "Review + create" page, click 'Create'.
</p>


<h3>Create a Linux (Ubuntu) VM.</h3>
<p>
<img src="https://i.imgur.com/GVWotlE.png" height="80%" width="80%" alt="Linux VM Creation"/>
</p>
<p>
To create a Linux (Ubuntu) VM in Azure, follow these steps: search for "Virtual Machine", click on 'Create', choose "Azure virtual machine", select the desired subscription (e.g., Azure subscription 1), specify the resource group (e.g., RG-Lab-2), provide a name for the virtual machine (e.g., VM2), and pick the same region as the previously created virtual machine ((US) West US 3).

Next, click on 'Image' and choose "Ubuntu Server 20.04 LTS - Gen2 (free services eligible)". Click on 'Size' and choose "Standard_E2s_v3 - 2 vcpus, 16 GiB memory ($91.98/month)". Set the authentication type to "Password" and specify the username (e.g., labuser) and password (e.g., Password1).

Click 'Next', leave the disk options as they are, and proceed to the next step. Ensure that the virtual network is set to 'RG-Lab-2-vnet' and the subnet is set to "default (10.0.0.0/24)". Wait for validation on the "Review + create" page, click 'Create'
</p>

<h3>Install Wireshark within your Windows 10 VM.</h3>
<p>
<img src="https://i.imgur.com/MTRGtSR.png" height="80%" width="80%" alt="Install Wireshark"/>
</p>
<p>
To install Wireshark on your Windows 10 VM, follow these steps: search for "Virtual Machine", click on 'VM1' and copy the Public IP address. Then, open the Remote Desktop Connection application on your computer and paste the Public IP address. Click connect and enter the credentials (username and password) you created for your Windows 10 VM earlier. If a warning message appears stating that it's not trustworthy, simply click 'Yes'. Additionally, a "Choose privacy settings for your device" message may pop up. Just set all options to "No" and click 'Accept'. 

Open Microsoft Edge, click 'Start without your data' if it appears, then <a href="https://www.wireshark.org/download.html">download Wireshark</a> (Windows Installer (64-bit)). Open the downloaded file and follow the setup instructions to install Wireshark.
</p>

<h3>Observe ICMP Traffic.</h3>
<p>
<img src="https://i.imgur.com/GT0gM6d.png" height="80%" width="80%" alt="ICMP Traffic"/>
</p>
<p>
To observe ICMP traffic, follow these steps: launch the Wireshark application, type "icmp", and press enter to filter just the ICMP traffic.

Back in Azure, search "Virtual Machine", click on 'VM2' and copy the Private IP address.

Back in your Windows 10 VM, open PowerShell and type "ping" followed by the copied Private IP address. Press enter to initiate the ping command. Observe the ping requests and replies within the Wireshark application.

Still in your Windows 10 VM's PowerShell, now type "ping" followed by a public website's URL (e.g., www.google.com). Press enter to execute the command. Observe the ping requests and replies within the Wireshark application.

Still in your Windows 10 VM's PowerShell, type "ping" followed by the copied Private IP address again, this time appending "-t" to the Private IP address. This will create a perpetual ping loop, allowing you to continuously monitor the connectivity.

Back in Azure, search "Network Security Groups", click 'VM2-nsg', click 'Inbound security rules', and click '+ Add' to create a new inbound security rule. Configure the rule as follows: set Source to "Any", Source port ranges to *, Destination to "Any", and Service to "Custom". Protocol to "ICMP", Action to "Deny", Priority to 200, and assign a name to the rule (e.g., "DENY_ICMP_PING_FROM_ANYWHERE"). Click 'Add'.

Back in your Windows 10 VM, notice the ping requests initiated from PowerShell start to time out both in PowerShell and Wireshark. This is because the ICMP traffic is now being blocked by the NSG associated with VM2, preventing VM2 from responding to the pings.

To re-enable ICMP traffic, go back in Azure, search "Network Security Groups", click 'VM2-nsg', click 'Inbound security rules', and click the inbound security rule you just created (e.g., "DENY_ICMP_PING_FROM_ANYWHERE"). Either change the Action to "Allow" or delete the inbound security rule.

Back in your Windows 10 VM, notice the ping requests initiated from PowerShell start to resume again in both PowerShell and Wireshark. This indicates that the ICMP traffic is no longer blocked by the NSG associated with VM2.

To stop the perpetual ping in PowerShell, press 'CTRL + C'.
</p>

<h3>Observe SSH Traffic.</h3>
<p>
<img src="https://i.imgur.com/saQJeGN.png" height="80%" width="80%" alt="SSH Traffic"/>
</p>
<p>
To observe SSH traffic, follow these steps: type either "ssh" or "tcp.port == 22" in Wireshark on your Windows 10 VM and press enter to filter just the SSH traffic.
  
Still in your Windows 10 VM, type "ssh [VM2 username]@[VM2 private IP address]" into Powershell. Replace [username] with the username you created earlier for VM2 and [VM2 private IP address] with the actual private IP address of VM2. Press enter. A prompt will appear asking, "Are you sure you want to continue connecting (yes/no/[fingerprint])?" Type "yes" and press enter. Type the password you created earlier for VM2 (you will not be able to see the characters as you type) and press enter.

Within the Linux SSH connection, you can enter various commands and observe the corresponding SSH traffic in Wireshark:
  <ul>
  <li>Type "uname -a" and press enter. This command displays the operating system running on VM2.</li>
  <li>Type "pwd" and press enter. This command prints the current working directory.</li>
  <li>Type "ls -lasth" and press enter. This command lists the folders and files in the current directory, displaying them in a detailed format.</li>
  <li>Type "touch hi.txt" and press enter. This command creates a new file named "hi.txt".</li>
  <li>Press the up button on your keyboard until you retrieve the previous "ls -lasth" command, and press enter. Notice that the newly created "hi.txt" file is now listed.</li>
  <li>Type "exit" and press enter. This command exists the SSH connection.</li>
  </ul>
</p>

<h3>Observe DHCP Traffic.</h3>
<p>
<img src="https://i.imgur.com/GK8tuBs.png" height="80%" width="80%" alt="DHCP Traffic"/>
</p>
<p>
To observe DHCP traffic, follow these steps: type "dhcp" in Wireshark on your Windows 10 VM and press enter to filter just the DHCP traffic.

Still in your Windows 10 VM, type "ipconfig /renew" into Powershell and press enter. This command triggers a DHCP renewal process where VM1 broadcasts a request for a new IP address on the virtual network. Azure's DHCP server then responds by re-issuing an IP address to VM1. While running this command, you can observe the DHCP traffic in Wireshark, confirming the exchange of DHCP messages over the network and indicating that the IP address has been successfully re-issued to VM1.
</p>

<h3>Observe DNS Traffic.</h3>
<p>
<img src="https://i.imgur.com/8r7blHa.png" height="80%" width="80%" alt="DNS Traffic"/>
</p>
<p>
To observe DNS traffic, follow these steps: type either "dns" or "udp.port == 53" in Wireshark on your Windows 10 VM and press enter to filter just the DNS traffic.

Still in your Windows 10 VM, type "nslookup www.google.com" into Powershell and press enter. You will receive a response from the DNS server in PowerShell, providing the IPv4 address of www.google.com. Additionally, you will notice a series of DNS traffic in Wireshark, indicating that the DNS server performed various lookups to retrieve information about www.google.com and return its IP address.

As an optional step, you can repeat the previous instructions to determine the IP addresses associated with the domain disney.com. 
</p>

<h3>Observe RDP Traffic.</h3>
<p>
<img src="https://i.imgur.com/5XVzhIV.png" height="80%" width="80%" alt="RDP Traffic"/>
</p>
<p>
To observe RDP traffic, follow these steps: type either "rdp" or "tcp.port == 3389" in Wireshark on your Windows 10 VM and press enter to filter just the RDP traffic.

As you observe the captured traffic, you will notice a continuous stream of data. The source and destination addresses will correspond to the IP address of VM1 (the virtual machine) and your local computer's IP address, respectively.

The reason for the continuous spam of traffic is because we are currently using RDP to establish a remote connection and interact with the virtual machine. As a result, there is a constant flow of RDP traffic being exchanged between your local computer and VM1. This non-stop traffic occurs even when you are not actively performing any specific activity, as the RDP connection remains active.
</p>

<h3>Delete the Resource Group created earlier to avoid incurring costs.</h3>
<p>
<img src="https://i.imgur.com/wNlmze9.png" height="80%" width="80%" alt="Delete RG"/>
</p>
<p>
To delete the Resource Group, follow these steps: search "Resource Group", click on the resource group (e.g., RG-Lab-2), click 'Delete resource group', then type or copy and paste the name of your resource group (e.g., RG-Lab-2) to confirm the deletion. Click 'Delete'.

Repeat these steps for the NetworkWatcherRG resource group that was automatically created earlier as well.
</p>

<h3>Verify the successful deletion of the Resource Groups.</h3>
<p>
<img src="https://i.imgur.com/vfekx03.png" height="80%" width="80%" alt="Delete Verified"/>
</p>
<p>
To verify the successful deletion of the Resource Groups, search "Resource Group" and confirm that your specified resource groups (e.g., RG-Lab-2 and NetworkWatcherRG) are no longer listed.
</p>
