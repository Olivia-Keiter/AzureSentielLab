<h1>Azure Sentinel Home Lab</h1>

<h2>Description</h2>
Project consists of using Azure Sentinel as a SIEM, connecting it to a unsecured virtual machine (honey pot) and using a custom PowerShell script to view live attacks (RDP brute force) from all over the world.
<br />


<h2>Languages and Utilities Used</h2>

- <b>PowerShell</b> 
- <b>API Site</b>

<h2>Environments Used </h2>

- <b>Windows 10</b> (21H2)
- <b>Azure Portal</b>

<h2>Progect walk-through:</h2>

<b> Step 1: Create a Resource Group</b> <br/>
In Azure create a Resource that you will use throughout this project. All resources you create will go in this resource group. <br/>
<img src="https://imgur.com/Ko8OPH7.png" height="80%" width="80%" alt="Azure Sentinel Steps"/>
<br />
<br />
                                                                                           
<b> Step 2: Create a VM</b> <br/>
In Azure create Virtual Machine using the resource group you created.<br/>
<img src="https://imgur.com/J9Q4FBp.png" height="80%" width="80%" alt="Azure Sentinel Steps"/>
<br />
<br />   
                                                                                            
<b> Step 3: Add a username and password</b> <br/>
In Azure create a username and password for your VM. Be sure to remember this as you will need it to RDP into your VM later. <b>*(TIP: Avoid common usernames like: Admin, Administrator, or User)*</b> <br/>
<img src="https://imgur.com/FtJVbm7.png" height="80%" width="80%" alt="Azure Sentinel Steps"/>
<br />
<br />     
<b> Step 4: Edit the Networking tab</b> <br/>
This VM is going to act as a "honeypot" so we want it to be unsecured so it is more easily discovered by attackers. In the Networking tab while creating the VM select "Advanced" for "NIC network security group" and click "Create new." <br/>
<img src="https://imgur.com/6JmPfBi.png" height="80%" width="80%" alt="Azure Sentinel Steps"/>
<br />
<br />
<b> Step 5: Edit the NIC NSG</b> <br/>
In Azure remove the default inbound rule and add a new inbound rule. Since we want this VM to be discoverable create the new rule to allow any/any inbound traffic and set the priority low (ex: 100) <br/>
<img src="https://imgur.com/syB8VS9.png" height="80%" width="80%" alt="Azure Sentinel Steps"/>
<br />
<br />
                                                                                              
<b> Step 6: Review and Create</b> <br/>
Accept the default settings for the VM and click "Review & Create." Once validation has passed click "Create" <br/>
<img src="https://imgur.com/FcjHeuW.png" height="80%" width="80%" alt="Azure Sentinel Steps"/>
<br />
<br />
Wait for process to complete (may take some time):  <br/>
<img src="https://i.imgur.com/JL945Ga.png" height="80%" width="80%" alt="Azure Sentinel Steps"/>
<br />
<br />
Sanitization complete:  <br/>
<img src="https://i.imgur.com/K71yaM2.png" height="80%" width="80%" alt="Azure Sentinel Steps"/>
<br />
<br />
Observe the wiped disk:  <br/>
<img src="https://i.imgur.com/AeZkvFQ.png" height="80%" width="80%" alt="Azure Sentinel Steps"/>
</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
