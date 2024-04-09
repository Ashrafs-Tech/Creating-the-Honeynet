# Creating the environment

![Template](https://github.com/Ashrafs-Tech/Creating-the-Honeynet/assets/166546026/ecd86868-3a72-4cf2-b426-21ea4fe448a2)


## Introduction

For this project, I constructed a honeynet within the Azure platform and gathered log data from multiple sources into a Log Analytics workspace. This workspace serves as the foundation for Microsoft Sentinel, enabling the creation of attack maps, alert triggers, and incident reports. I conducted security metric assessments in the vulnerable environment for 24 hours, implemented security measures to fortify the environment, and subsequently reevaluated the metrics for another 24-hour period. Below, I will present the measured security metrics, which include:

- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityEvent (Windows Event Logs)
- SecurityIncident (Incidents created by Sentinel)
- Syslog (Linux Event Logs)

The first thing I have to do is to create an Azure subcription.  

![image](https://github.com/Ashrafs-Tech/Creating-the-Honeynet/assets/166546026/bb2a4fe0-bc54-414f-a293-026e7604d478)

Then I will create a Resource Group.  Think of it like a folder in our desktop.  But instead of files, it will be filled with resources. The "Resources" are the following: 

- Two Network Security Groups
- Two virtual machines
  * A Linux virtual machine
  * A Windows virtual machine
- Two Public IP addresses
- The virtual network that the virtual machines will be on

All of the above are part of our Honeynet.

To create a Resource Group and a virtual machine, I will go to the Azure portal and type in "virtual machine" and then click "Create"

![image](https://github.com/Ashrafs-Tech/Creating-the-Honeynet/assets/166546026/49650660-0afe-499c-b59a-62233c42b841)

Then I named the Resource group "RG-Cyber-Lab" and the first virtual machine "windows-vm"
I also created a username and password for the virtual machine.

![image](https://github.com/Ashrafs-Tech/Creating-the-Honeynet/assets/166546026/6c87b9b1-6a81-431c-8f97-925ad46d64d5)


Also made sure to put the virtual network in the same resource group as the virtual machine.

![image](https://github.com/Ashrafs-Tech/Creating-the-Honeynet/assets/166546026/bcf7bebd-901b-4cf8-9b01-b74990d5c0da)


Now I will create the Linux virtual machine for my environment. I put it in the same Resource Group, named the virtual machine "linux-vm", place it in the same zone as the other virtual machine, and gave it the Ubuntu Server Image. And I placed it in the same virtual network.

![image](https://github.com/Ashrafs-Tech/Creating-the-Honeynet/assets/166546026/c5fc51f8-c89e-487e-8e67-f5b063f4d60f)


Now that both virutal machines have been created, I will need to do some configuration.  I will open up both Network Security Groups so that both virtual machines can be discovered by people around the internet. Network Security Groups act as firewalls for the virtul machines. 

I went to the Windows virtual machine in the Resource Group.  There is a list of Inbound Security Rules.  I will delete the RDP rule.  The RDP rule is the "Remote Desktop Protocol" which monitors inbound traffic.

![image](https://github.com/Ashrafs-Tech/Creating-the-Honeynet/assets/166546026/978ebaee-f309-40bf-9336-6e2d13ca3066)

Now I will create my own rule that will allow all inbound traffic. I set the source port range and the destination port range to "*" which allows any. 

![image](https://github.com/Ashrafs-Tech/Creating-the-Honeynet/assets/166546026/c34ee132-3d2a-4882-beff-647523c1ee11)


Then I moved to the Linux virtual machine.  I deleted the SSH rule.

![image](https://github.com/Ashrafs-Tech/Creating-the-Honeynet/assets/166546026/b02e2150-7889-4a02-a0bb-9769b38f9ef9)

There will be warnings that appear when making these configurations but that's fine for the purposes of this project. 

![image](https://github.com/Ashrafs-Tech/Creating-the-Honeynet/assets/166546026/88718b22-ca6f-466a-9471-033bfffe8af9)



## Step 1 is done. I have created:

- My Azure subscription
- My Resource Group
- My Linux virutal machine
- My Windows virutal machine
- The Virtual Network
- Configure the Network Security Groups for both virtual machines.

![image](https://github.com/Ashrafs-Tech/Creating-the-Honeynet/assets/166546026/7c768727-89f2-448b-a826-3e3c817e5259)




