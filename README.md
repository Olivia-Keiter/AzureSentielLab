<h1>Azure Sentinel Home Lab</h1>

<h2>Description</h2>
Project consists of using Azure Sentinel as a SIEM, connecting it to a unsecured virtual machine (honey pot) and using a custom PowerShell script to view live attacks (RDP brute force) from all over the world.
<br />
<h2> Topology</h2><br/> 
<img src="https://imgur.com/AfrssEH.png" height="80%" width="80%" alt="Azure Sentinel Steps"/>


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
Accept the default settings for the VM and click "Review & Create." Once validation has passed click "Create." This deployment will take ~10 minutes, you can move onto the next step while the VM is deploying. <br/>
<img src="https://imgur.com/FcjHeuW.png" height="80%" width="80%" alt="Azure Sentinel Steps"/>
<br />
<br />

<b> Step 7: Create a Log Analytic Workspace</b> <br/>
In Azure create a log analytic workspace using the same resource group and region you used for your VM. <br/>
<img src="https://imgur.com/5gkVnue.png" height="80%" width="80%" alt="Azure Sentinel Steps"/>
<br />
<br />

<b> Step 8: Edit the Data collection</b> <br/>
In Azure go to Microsoft Defender for Cloud>Settings>Data collection and change it to store All Events. Be sure to save <br/>
<img src="https://imgur.com/Z2ydv4r.png" height="80%" width="80%" alt="Azure Sentinel Steps"/>
<br />
<br />

<b> Step 9: Edit the Defender Plan</b> <br/>
In Azure go to Microsoft Defender for Cloud>Settings>Defender plans. Esure Microsoft Defender Plans are turned on for Servers and off for SQL servers. Be sure to save <br/>
<img src="https://imgur.com/lLxvTje.png" height="80%" width="80%" alt="Azure Sentinel Steps"/>
<br />
<br />

<b> Step 10: Connect your VM to your Log Analytics Workspace</b> <br/>
In Azure go to Log Analytics Workspace and select the workspace you created for this lab. Go to the Virtual Machine tab and selec the VM you created for this lab. Click "Connect." The connection will show up immediently but it will take ~15 minutes for the data to sync to Azure. <br/>
<img src="https://imgur.com/of9myT7.png" height="80%" width="80%" alt="Azure Sentinel Steps"/>
<br />
<br />

<b> Step 11: Add Microsoft Sentinel to a workspace</b> <br/>
In Azure go to Microsoft Sentinel. Select your workspace and click "Add" <br/>
<img src="https://imgur.com/HaABVPo.png" height="80%" width="80%" alt="Azure Sentinel Steps"/>
<br />
<br />

<b> Step 1: Add Microsoft Sentinel to a workspace</b> <br/>
In Azure go to Microsoft Sentinel. Select your workspace and click "Add" <br/>
<img src="https://imgur.com/HaABVPo.png" height="80%" width="80%" alt="Azure Sentinel Steps"/>
<br />
<br />

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
