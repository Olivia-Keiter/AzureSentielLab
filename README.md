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

<b> Step 12: Connect to your VM using RDP</b> <br/>
In Azure go to the VM you created for this lab. Click "Connect">"RDP." Download the RDP file and connect using the username/password you created earlier. In the VM search for "Event Viewer." Expand "windows Logs" then "Security." <br/>
<img src="https://imgur.com/eRj6jjF.png" height="80%" width="80%" alt="Azure Sentinel Steps"/>
<br />
<br />

<b> Step 13: View Event Viewer</b> <br/>
In your VM view some of the logs. For this lab we will be focused on event ID 4625. At this point, you should not have any of those logs. To create one attempt to RDP into your VM from your home compute again, this time using an incorrect username or password. When you look at the event viewer after failing to logon you will find a log with event ID 4625 (Audit Failure.)  <br/>
<img src="https://imgur.com/pxyzIlq.png" height="80%" width="80%" alt="Azure Sentinel Steps"/>
<br />
<br />

<b> Step 14: Go to API site</b> <br/>
In your VM open Microsoft Edge and navigate to https://ipgeolocation.io and click "Get Free API Access." This API will provide the geolocation of our attackers. Keep this tab open, you will use it later. <br/>
<img src="https://imgur.com/BZoskOK.png" height="80%" width="80%" alt="Azure Sentinel Steps"/>
<img src="https://imgur.com/WOZDcwl.png" height="80%" width="80%" alt="Azure Sentinel Steps"/>
<br />
<br />

<b> Step 15: Open ISE</b> <br/>
In your VM open PowerShell ISE. Paste the PowerShell code into ISE. Go back to the API site and copy the API key. Back in ISE edit line 2, paste your copied API key here. Save the code to your desktop by clicking File>Save As. <br/>
<img src="https://imgur.com/pxyzIlq.png" height="80%" width="80%" alt="Azure Sentinel Steps"/>
<br />
<br />

<b> Step 16: Ping your VM </b> <br/>
On your local computer open the command line. Ping your VMs public IP using -t to run the ping until you tell it to stop, you should see "Request timed out." <br/>
<img src="https://imgur.com/x6bfV9J.png" height="80%" width="80%" alt="Azure Sentinel Steps"/>
<br />
<br />

<b> Step 17: Disable Windows Firewall </b> <br/>
On your VM search for Windows Defender Firewall and click "Turn Windows Defender Firewall on or off." <br/>
<img src="https://imgur.com/VAjp4SP.png" height="80%" width="80%" alt="Azure Sentinel Steps"/>
Click "Turn off Windows Defender Firewall(not recommended) for both Private and Public network settings. Click OK to apply your changes <br/>
<img src="https://imgur.com/mKQVZYA.png" height="80%" width="80%" alt="Azure Sentinel Steps"/>
<br />
<br />

<b> Step 18: Ping your VM </b> <br/>
On your local computer go back to the command line and view the ping request you left running. You will now see that you local computer and ping your VM. This will make it easier for attackers to find our VM. <br/>
<img src="https://imgur.com/V8EhaX4.png" height="80%" width="80%" alt="Azure Sentinel Steps"/>
<br />
<br />

<b> Step 19: Run the PowerShell Script </b> <br/>
On your VM open PowerShell ISE and run the command we pasted earlier. After a few seconds you will see the failed RDP attempt we did earlier in the lab. This script is pulling information from the Event Viewer, specific to event ID 4625 and storing it in a file for later use. <br/>
<img src="https://imgur.com/MONceva.png" height="80%" width="80%" alt="Azure Sentinel Steps"/>
On your VM open File Explorer and navigatte to C:\ProgramData\failed_rdp. (This file is hidden so you will need to view hidden items) <br/>
<img src="https://imgur.com/zdVCCVL.png" height="80%" width="80%" alt="Azure Sentinel Steps"/>
Open failed_rdp.txt and see the data being pulled from the event viewer. (Everything highlighed blue is sample data to use later in the lab.) The last entry being when you failed to RDP into the VM. <br/>
<img src="https://imgur.com/3WXDZPB.png" height="80%" width="80%" alt="Azure Sentinel Steps"/>
<br />
<br />

<b> Step 20: *OPTIONAL* Wait</b> <br/>
Wait until you start to recieve more outputs in PowerShell. Congratulations, your VM was found by attackers who are attempting to brute force into it. <br/>
<img src="https://imgur.com/94Qgzsc.png" height="80%" width="80%" alt="Azure Sentinel Steps"/>
<br />
<br />

<b> Step 21: Copy the data </b> <br/>
On your VM copy the data in the failed_rdp.txt file and save it to your local machine in a text file for use in the next step. <br/>
<img src="https://imgur.com/9GZBqlY.png" height="80%" width="80%" alt="Azure Sentinel Steps"/>
<img src="https://imgur.com/sjr5S3G.png" height="80%" width="80%" alt="Azure Sentinel Steps"/>
<br />
<br />

<b> Step 22: Create a Custom Log</b> <br/>
On your local computer, back in Azure go to Log Analytics Workspace>Logs and add a new custom log. Select the failed_rdp.txt file from the last setep as the sample log, click next. View the next page and ensure the record delimeter is set to "New line."<br/>
<img src="https://imgur.com/uoYuPSr.png" height="80%" width="80%" alt="Azure Sentinel Steps"/>
View the next page and ensure the record delimeter is set to "New line."<br/>
<img src="https://imgur.com/6wqAuLm.png" height="80%" width="80%" alt="Azure Sentinel Steps"/>
Select "windows" as the type and "C:\programData\failed_rdp.log" as the path. This is the path to the log on your VM. <br/>
<img src="https://imgur.com/mvjiAZy.png" height="80%" width="80%" alt="Azure Sentinel Steps"/>
Give the custom log a name. I chose "FAILED_RDP_w_GEO" see that "_CL" is added to the end of the log name and create the custom log. <br/>
<img src="https://imgur.com/dF8C6rg.png" height="80%" width="80%" alt="Azure Sentinel Steps"/>
<br />
<br />

<b> Step 23: View Custom Log </b> <br/>
Once the log is created the name will show in custom tables almost immedietly. However, it will take ~15 minutes for it to sync with Azure. Now is a good time to take a break as you cannot move on in the lab until the data has synced to azure.<br/>
<img src="https://imgur.com/nZLwUYq.png" height="80%" width="80%" alt="Azure Sentinel Steps"/>
<br />
<br />

<b> Step 24: Run the Custom Log </b> <br/>
Navigate to your workspace then select Logs. Run your new custom log. From here you can see each output listed under results. <br/>
<img src="https://imgur.com/LGoXNcu.png" height="80%" width="80%" alt="Azure Sentinel Steps"/>
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
