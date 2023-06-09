<p align="center">
<img src="https://i.imgur.com/FRRLw01.png" alt="Azure logo"/>
</p>

<h1>Performing Networking Activities within Azure VMs</h1>
This beginner-friendly tutorial provides hands-on experience with Azure networking. Learn how to create a resource group with Windows 10 and Linux virtual machines, and use Wireshark to observe ICMP, SSH, DHCP, DNS, and RDP traffic. Discover network communication, disable and re-enable ICMP traffic, and explore essential networking concepts and technologies. Practice proper resource management by deleting the resource group and verifying its successful removal.<br />

<h2>List Summary</h2>

- Create a Resource Group.
- Create a Windows 10 Virtual Machine (VM).
- Create a Linux (Ubuntu) VM.
- Observe Your Virtual Network within Network Watcher.
- Observe ICMP Traffic.
- Observe SSH Traffic.
- Observe DHCP Traffic.
- Observe DNS Traffic.
- Observe RDP Traffic.
- Observe DNS Traffic.
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

<h2>Installation Steps</h2>

<h3>Create your Azure account (Tenant) and Subscription.</h3>
<p>
<img src="https://i.imgur.com/YmqCvWZ.png" height="80%" width="80%" alt="Account Creation"/>
</p>
<ul>
  <li>
    <a href="https://azure.microsoft.com/en-us/free/">Create an Azure account</a> (Tenant) and Subscription if you haven't done so already.
  </li>
</ul>


<h3>Within the Azure Portal, create a Resource Group.</h3>
<p>
<img src="https://i.imgur.com/D4LlhJ3.png" height="80%" width="80%" alt="RG creation"/>
</p>
<p>
<ul>
  <li>Search for Resource Group
    <ul>
      <li>Note: A Resource Group is essentially a folder</li>
    </ul>
  </li>
  <li>Click 'Create'</li>
  <li>Choose your Subscription (i.e., 'Azure subscription 1')
    <ul>
      <li>Note: A Subscription provides access to Azure services while enabling the separatation and management of resources, usage, and billing. </li>
    </ul>
  </li>
  <li>Write a name for your resource group (i.e., RG-Lab-1)</li>
  <li>Pick a Region where the resource group is being created (i.e., '(US) West US 2')</li>
  <li>For now, skip creating a tag since not necessary
    <ul>
      <li>Note: A tag is used to effectively track data and metadata within your organization</li>
    </ul>
  </li>
  <li>Wait for validation on "Review + create", then click 'Create'</li>
</ul>
</p>


<h3>Create a Storage Account within the previously created Resource Group.</h3>
<p>
<img src="https://i.imgur.com/Vesiv6r.png" height="80%" width="80%" alt="Storage Group creation"/>
</p>
<p>
<ul>
  <li>Search for Storage Account
    <ul>
      <li>Note: A Storage Account is one of the many resource types available in Azure, offering functionality akin to a very powerful Dropbox or Google Drive.</li>
    </ul>
  </li>
  <li>Click 'Create'</li>
  <li>Choose your Subscription (i.e., 'Azure subscription 1')</li>
  <li>Choose your resource group (i.e., 'RG-Lab-1')</li>
  <li>Write a name for your storage account (i.e., joshcoursecareerslab01)</li>
  <li>Pick a Region where the storage account is being created (i.e., '(US) West US 2')</li>
  <li>Choose your Performance (i.e., 'Standard')</li>
  <li>Choose your Redundancy (i.e., 'Geo-redundant storage (GRS)')</li>
  <li>Wait for validation on "Review + create" then click 'Create'</li>
</ul>
</p>

<h3>Upload a file from your local desktop into the Storage Account.</h3>
<p>
<img src="https://i.imgur.com/vvNXCvY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<ul>
  <li>Open the storage account you just created (i.e., 'joshcoursecareerslab01')</li>
  <li>Click 'Containers'
    <ul>
      <li>Note: a Container is like an individual folder inside of our Storage Account</li>
    </ul>
  </li>
  <li>Click '+ Container' to create a Container</li>
  <li>Write a name for your container (i.e., cclab01)</li>
  <li>Choose Public access level (i.e., 'Private (no anonymous access)')</li>
  <li>Click 'Create', then open the container</li>
  <li>Open the Notepad application on your computer, write something (i.e., Hello World), and save the file</li>
  <li>Click '+ Upload' and select the notepad file to upload</li>
</ul>
</p>

<h3>Edit the file within the Storage Account in the Azure Portal.</h3>
<p>
<img src="https://i.imgur.com/Mt2AoZa.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<ul>
  <li>Click on the "three dots" next to your uploaded Notepad file</li>
  <li>Click 'View/edit'</li>
  <li>Edit the file directly from inside the storage account container (make some changes to the text as you wish)</li>
  <li>Click 'Save'</li>
</ul>
</p>

<h3>Download the file to observe the changes.</h3>
<p>
<img src="https://i.imgur.com/UXkpAM1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<ul>
  <li>Click 'Download'</li>
  <li>Open the downloaded file on your computer and observe the edits</li>
</ul>
</p>

<h3>Download the file to observe the changes.</h3>
<p>
<img src="https://i.imgur.com/UXkpAM1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<ul>
  <li>Click 'Download'</li>
  <li>Open the downloaded file on your computer and observe the edits</li>
</ul>
</p>

<h3>Download the file to observe the changes.</h3>
<p>
<img src="https://i.imgur.com/UXkpAM1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<ul>
  <li>Click 'Download'</li>
  <li>Open the downloaded file on your computer and observe the edits</li>
</ul>
</p>

<h3>Download the file to observe the changes.</h3>
<p>
<img src="https://i.imgur.com/UXkpAM1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<ul>
  <li>Click 'Download'</li>
  <li>Open the downloaded file on your computer and observe the edits</li>
</ul>
</p>

<h3>Download the file to observe the changes.</h3>
<p>
<img src="https://i.imgur.com/UXkpAM1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<ul>
  <li>Click 'Download'</li>
  <li>Open the downloaded file on your computer and observe the edits</li>
</ul>
</p>

<h3>Delete the Resource Group created earlier to avoid incurring costs.</h3>
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<ul>
  <li>Search for Resource Group</li>
  <li>Click on your resource group (i.e., ‘RG-Lab-1’)</li>
  <li>Click 'Delete resource group'</li>
  <li>Type or copy and paste the name of your resource group (i.e., RG-Lab-1) to confirm the deletion</li>
  <li>Click ‘Delete’</li>
</ul>
</p>

<h3>Verify the successful deletion of the Resource Group.</h3>
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<ul>
  <li>Search for Resource Group</li>
  <li>Confirm that your resource group has been deleted</li>
</ul>
</p>
