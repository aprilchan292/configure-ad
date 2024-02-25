<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Setup Resources in Azure
- Ensure Connection between Client and Domain Controller
- Install Active Directory and Admin Creation
- Create X-Amount of Client Users using PowerShell Script

<h2>Deployment and Configuration Steps</h2>


<p>
  <ul>
    <li>Setup Resources in Azure</li>
    <ul>
      <li>Create a Resource Group.</li>
      <li>Create a Virtual Machine, it will automatically generate a virtual network and subnet.</li>
    </ul>
  </ul>
<img src="https://i.imgur.com/sBKP3Bc.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
  <ul>
    <li>Create the Domain Controller VM (Windows Server 2022) named "DC-1":</li>
    <ul>
      <li>Take note of the Resource Group and VNet created.</li>
      <li>Set Domain Controller’s NIC Private IP address to be static.</li>
    </ul>
  </ul>
<img src="" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
  <ul>
    <li>Create the Client VM (Windows 10) named “Client-1”:</li>
    <ul>
      <li>Use the same Resource Group and VNet from Step 2.</li>
      <li>Ensure both VMs are in the same VNet.</li>
    </ul>
  </ul>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
  <ul>
    <li>Ensure Connectivity between the client and Domain Controller:</li>
    <ul>
      <li>Ping DC-1’s private IP address from Client-1 using perpetual ping.</li>
      <ul>
        <li>Copy Client-1's public IP address.</li>
        <li>Go to the Start menu, navigate to Remote Desktop, enter the IP address, and log in using the credentials we created in Azure.</li>
      </ul>
      <li>Enable ICMPv4 on the local Windows Firewall of DC-1.</li>
    </ul>
  </ul>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
  <ul>
    <li>Install Active Directory:</li>
    <ul>
      <li>Login to DC-1 and install Active Directory Domain Services.</li>
      <li>Promote DC-1 as a DC and set up a new forest with a specified domain name.</li>
      <li>Restart DC-1 and log back in as the designated user.</li>
    </ul>
  </ul>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
  <ul>
    <li>Create an Admin and Normal User Account in AD:</li>
    <ul>
      <li>Create OUs named "_EMPLOYEES" and "_ADMINS".</li>
      <li>Create a new employee named “Jane Doe” with the username “jane_admin” and add to "Domain Admins" Security Group.</li>
      <li>Log in as “mydomain.com\jane_admin”.</li>
    </ul>
  </ul>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
  <ul>
    <li>Join Client-1 to your domain (mydomain.com):</li>
    <ul>
      <li>Set Client-1’s DNS settings to DC’s Private IP address.</li>
      <li>Restart Client-1 from Azure Portal.</li>
      <li>Join Client-1 to the domain.</li>
      <li>Verify Client-1 in ADUC on the Domain Controller.</li>
    </ul>
  </ul>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
  <ul>
    <li>Setup Remote Desktop for non-administrative users on Client-1:</li>
    <ul>
      <li>Log into Client-1 as mydomain.com\jane_admin.</li>
      <li>Open system properties and allow "domain users" access to remote desktop.</li>
    </ul>
  </ul>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
  <ul>
    <li>Create additional users and attempt to log into Client-1 with one of the users:</li>
    <ul>
      <li>Login to DC-1 as jane_admin.</li>
      <li>Open PowerShell_ise as an administrator.</li>
      <li>Run the provided script to create new users.</li>
      <li>Observe the accounts in ADUC and attempt to log into Client-1 with one of the newly created accounts.</li>
    </ul>
  </ul>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />
