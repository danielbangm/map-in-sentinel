<p align="center">
<img src="https://shorturl.at/kBILY" />
</p>

<h1>SIEM: Azure Sentinel - Prerequisites and Installation</h1>

I setup Azure Sentinel (SIEM) and connect it to a live virtual machine acting as a honey pot. We will observe live attacks (RDP Brute Force) from all around the world. We will use a custom PowerShell script to look up the attackers Geolocation information and plot it on the Azure Sentinel Map! 

<h2>Objectives</h2>

-  More Experience with Azure (I will Create the environment here)
-  Understanding the creation of VM, log analytic workspace, and Sentinel Azure.
-  Gain a better understanding of all parts of Active Directory such resetting passwords and setting up users.

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Virtual Machine(Honeypot-vm)
- log analytical workspaces(Lawhoneypot1)
- Azure Sentinel
- Remote Desktop

<h2>Operating Systems Used</h2>

-  Windows 10 pro

<h2>List of Prerequisites</h2>

-  All you need for this lab is the free Azure Tenant and Subscription

<h2>Installation steps</h2>

-  Step 1: Observe Event Viewer Logs in VM

I Log in VM using RDP. Type on the menu "Event viewer". Click on windows log, and then security. From there you can see all the event success and failure. That's where we going to get the IP addresses from all the attackers to plug into Sentinel to have their geolocation.
![image](https://github.com/danielbangm/map-in-sentinel/assets/22795502/dc3b3572-e09f-4f30-b5a4-bf36bd321744)

-  Step 2: Turn off windows Firewall on VM

Log in VM and search for wf.msc on the menu. Click on Windows Defender Firewall Properties. Go to Domain profile, Private profile, Public profile and turn them off. I tried to ping my VM from my actual computer and we can see that the echo is now accepted by the VM because we turned the firewall off.
![image](https://github.com/danielbangm/map-in-sentinel/assets/22795502/8123275d-9d3c-4385-84e6-4f4bf37fd394)
![image](https://github.com/danielbangm/map-in-sentinel/assets/22795502/d2ad11fb-16cc-473d-8e63-b04820f558bd)

-  Step 3: Download the powershell script and sign up for ipgeolocalisation.io

I downloaded this <a href="https://github.com/joshmadakor1/Sentinel-Lab/blob/main/Custom_Security_Log_Exporter.ps1">Powershell Script</a> which is essentially a github repository. Click on the custom securitylog exporter, either download or just copy it and then open powershell ISE on the VM. Create new file and paste it, save it on the desktop as "log exporter.The only thing to modify on that scrip is the API key. In order to get that, we have to sign up for ipgeolocalisation.io and get our API key replaced in the powershell script
![image](https://github.com/danielbangm/map-in-sentinel/assets/22795502/ea1fef18-f0c0-49df-8258-0c24be6300bb)

-  Step 4: Run the script

After getting your own API key, launch powershell ISE and run the script in Vm. The API keyy allows us to get the geolocalisation and longitute, latitude of the attackers. Essentially what it does, it looks through the event logs, security logs, then grabs all the events of people who failed to log in and grabs their IP address, and geolocalisation data to create a new log file
![image](https://github.com/danielbangm/map-in-sentinel/assets/22795502/10569e1e-3b84-41c7-8610-99d53730836a)



