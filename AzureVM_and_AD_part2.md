<h1>Azure Virtual Machine Creation used to host an Active Directory Domain Controller (part 2)</h1>

 ### YouTube Demonstration - Coming Soon!

<h2>Description</h2>
Welcome back to Deploying an Active Directory server using Microsoft Azure Virtual Machines (pt 2). In part 1 we setup two VMs (Server2019 and Windows10). We won’t be doing anything with the Windows10 VM but focusing on deploying Active Directory (AD) on Server2019. Let’s get to it!
<br />


<h2>Languages and Programs Used</h2>

- <b>PowerShell</b> 
- <b>Microsoft Azure</b>

<h2>Operating Systems Used </h2>

- <b>Windows Server 2019</b> (Domain Controller for Active Directory)
- <b>Windows 10</b> (A client machine to add to Active Directory)

<h2>Program walk-through:</h2>

<p>From the Azure Dashboard you can see our two VMs under Resources. Click on Server2019:</p>

<p align="center">
<br/>
<img src="https://i.imgur.com/OWJVtq5.png" height="80%" width="80%" alt="Microsoft Azure Virtual Machine"/>
<br /></p>
<br />
<br />
Start Server2019 (refresh screen for status checks. you might get a message across screen stating it’s not ready, but in the Notifications in top right it states it’s ready):
<br />
<p align="center">
<br/>
<img src="https://i.imgur.com/85HfkHx.png" height="80%" width="80%" alt="Microsoft Azure Virtual Machine"/>
<br /></p>
<br />
<br />
Connect to Server2019 via RDP (Connect button > Download RDP file > Open > etc):
<br />
<p align="center">
<br/>
<img src="https://i.imgur.com/WMLgPsN.png" height="80%" width="80%" alt="Microsoft Azure Virtual Machine"/>
<br /></p>
<br />
<br />
This brings us to the Server Manager > Dashboard:
<br />
<p align="center">
<br/>
<img src="https://i.imgur.com/WBnzWDq.png" height="80%" width="80%" alt="Microsoft Azure Virtual Machine"/>
<br /></p>
<br />
<br />
In part 1, we’ve already renamed the Domain Controller from Server2019 to Miami-01. Now we will add some roles and features to this domain controller. In the top right go to Manage > Add Roles and Features:
<br />
<p align="center">
<br/>
<img src="https://i.imgur.com/ekJDIPv.png" height="80%" width="80%" alt="Microsoft Azure Virtual Machine"/>
<br /></p>
<br />
<br />
Hit Next:
<br />
<p align="center">
<br/>
<img src="https://i.imgur.com/7ESMvqz.png" height="80%" width="80%" alt="Microsoft Azure Virtual Machine"/>
<br /></p>
<br />
<br />
Select Role-based or feature-based installation > Next:
<br />
<p align="center">
<br/>
<img src="https://i.imgur.com/OJ7EoX6.png" height="80%" width="80%" alt="Microsoft Azure Virtual Machine"/>
<br /></p>
<br />
<br />
Select Next:
<br />
<p align="center">
<br/>
<img src="https://i.imgur.com/eUkho4L.png" height="80%" width="80%" alt="Microsoft Azure Virtual Machine"/>
<br /></p>
<br />
<br />
Select Active Directory Domain Services:
<br />
<p align="center">
<br/>
<img src="https://i.imgur.com/iIVaZ6D.png" height="80%" width="80%" alt="Microsoft Azure Virtual Machine"/>
<br /></p>
<br />
<br />
When you add the role it will automatically add additional features. Just click Add Features:
<br />
<p align="center">
<br/>
<img src="https://i.imgur.com/VvHHJ57.png" height="80%" width="80%" alt="Microsoft Azure Virtual Machine"/>
<br /></p>
<br />
<br />
Select Next on Server Roles screen:
<br />
<p align="center">
<br/>
<img src="https://i.imgur.com/MzGtNfP.png" height="80%" width="80%" alt="Microsoft Azure Virtual Machine"/>
<br /></p>
<br />
<br />
Select Next on Features tab (notice the Group Policy Management feature has been added):
<br />
<p align="center">
<br/>
<img src="https://i.imgur.com/GvOOIlL.png" height="80%" width="80%" alt="Microsoft Azure Virtual Machine"/>
<br /></p>
<br />
<br />
Select Next on the AD DS screen:
<br />
<p align="center">
<br/>
<img src="https://i.imgur.com/02JaaZf.png" height="80%" width="80%" alt="Microsoft Azure Virtual Machine"/>
<br /></p>
<br />
<br />
Select Install:
<br />
<p align="center">
<br/>
<img src="https://i.imgur.com/vNIF3nA.png" height="80%" width="80%" alt="Microsoft Azure Virtual Machine"/>
<br /></p>
<br />
<br />
The install could take a couple of minutes:
<br />
<p align="center">
<br/>
<img src="https://i.imgur.com/0kflUm2.png" height="80%" width="80%" alt="Microsoft Azure Virtual Machine"/>
<br /></p>
<br />
<br />
When the installation is complete, click Promote this server to a domain controller:
<br />
<p align="center">
<br/>
<img src="https://i.imgur.com/ssnAg8a.png" height="80%" width="80%" alt="Microsoft Azure Virtual Machine"/>
<br /></p>
<br />
<br />
Select Add a new forest then give any name for the Root domain name (I called it infotechaaron.local). Followed by Next:
<br />
<p align="center">
<br/>
<img src="https://i.imgur.com/ghn7HTa.png" height="80%" width="80%" alt="Microsoft Azure Virtual Machine"/>
<br /></p>
<br />
<br />
Type any password you want for Directory Services Restore Mode (DSRM) and click Next:
 <br />
<p align="center">
<br/>
<img src="https://i.imgur.com/3rs57Sk.png" height="80%" width="80%" alt="Microsoft Azure Virtual Machine"/>
<br /></p>
<br />
<br />
Select Next on DNS Options:
<br />
<p align="center">
<br/>
<img src="https://i.imgur.com/pF2W3Uf.png" height="80%" width="80%" alt="Microsoft Azure Virtual Machine"/>
<br /></p>
<br />
<br />
By default the NetBIOS domain name will autofill. Select Next:
<br />
<p align="center">
<br/>
<img src="https://i.imgur.com/kgFnIsu.png" height="80%" width="80%" alt="Microsoft Azure Virtual Machine"/>
<br /></p>
<br />
<br />
Select Next on the Paths screen:
<br />
<p align="center">
<br/>
<img src="https://i.imgur.com/Hkn2Drg.png" height="80%" width="80%" alt="Microsoft Azure Virtual Machine"/>
<br /></p>
<br />
<br />
On the Review Options screen you have two options for installing AD. You can continue in the wizard by selecting Next, or you can View Script and run that script in PowerShell. If you choose to run the script in PowerShell:
<br />
<p align="center">
<br/>
<img src="https://i.imgur.com/adp7fTJ.png" height="80%" width="80%" alt="Microsoft Azure Virtual Machine"/>
<br /></p>
<br />
<br />
Copy the script:
<br />
<p align="center">
<br/>
<img src="https://i.imgur.com/0lEt1gS.png" height="80%" width="80%" alt="Microsoft Azure Virtual Machine"/>
<br /></p>
<br />
<br />
Open PowerShell under admin mode and paste the script in PowerShell’s CLI and press enter to install.
<br />
<p align="center">
<br/>
<img src="https://i.imgur.com/VXD8QLv.png" height="80%" width="80%" alt="Microsoft Azure Virtual Machine"/>
<br /></p>
<br />
<br />
<p align="center">
<br/>
<img src="https://i.imgur.com/jPftcK3.png" height="80%" width="80%" alt="Microsoft Azure Virtual Machine"/>
<br /></p>
<br />
<br />
It will then sign you out. Go and RDP connect in again after a couple minutes:
<br />
<p align="center">
<br/>
<img src="https://i.imgur.com/mXj6pQq.png" height="80%" width="80%" alt="Microsoft Azure Virtual Machine"/>
<br /></p>
<br />
<br />
For some reason when I reconnected to the Server2019, it was spending a lot of time on the “Group Policy Client”, so be patient as it sets this up:
<br />
<p align="center">
<br/>
<img src="https://i.imgur.com/CPanqqB.png" height="80%" width="80%" alt="Microsoft Azure Virtual Machine"/>
<br /></p>
<br />
FYI: It took about 5 minutes for me to be able to connect to the VM again. Your patience is required lol.
<br />
<br />
<br />
<br />
Ok, I’m back into Server2019 and Active Directory has been installed:
<br />
<p align="center">
<br/>
<img src="https://i.imgur.com/HC7V0VY.png" height="80%" width="80%" alt="Microsoft Azure Virtual Machine"/>
<br /></p>
<br />
<br />
Now go to: Start > Windows Administrative Tools > Active Directory Administrative Center:
<br />
<p align="center">
<br/>
<img src="https://i.imgur.com/Zj6x3kq.png" height="80%" width="80%" alt="Microsoft Azure Virtual Machine"/>
<br /></p>
<br />
<br />
When AD Admin Center opens go to the infotechaaron (local) tab:
<br />
<p align="center">
<br/>
<img src="https://i.imgur.com/lpVyDyK.png" height="80%" width="80%" alt="Microsoft Azure Virtual Machine"/>
<br /></p>
<br />
<br />
From you (local) tab, a best practice is to click on Enable Recycle Bin (highlighted in blue on the right). What this does is creates a Recycle Bin which an admin can use if they accidentally delete a user. If that happens, just go into your Recycle Bin and re-enable that user (which will place the deleted user back into the same place it was deleted from. All permissions and groups remain intact).
<br />
<p align="center">
<br/>
<img src="https://i.imgur.com/rVPZ7yk.png" height="80%" width="80%" alt="Microsoft Azure Virtual Machine"/>
<br /></p>
<br />
<br />
Click OK:
<br />
<p align="center">
<br/>
<img src="https://i.imgur.com/GIaC1tB.png" height="80%" width="80%" alt="Microsoft Azure Virtual Machine"/>
<br /></p>
<br />
<br />
Click OK again:
<br />
<p align="center">
<br/>
<img src="https://i.imgur.com/XDfhbTy.png" height="80%" width="80%" alt="Microsoft Azure Virtual Machine"/>
<br /></p>
<br />
<br />
Refresh the AD Admin Center a couple of times (when Enable Recycle Bin is greyed out, it’s enabled):
<br />
<p align="center">
<br/>
<img src="https://i.imgur.com/VWzkrjm.png" height="80%" width="80%" alt="Microsoft Azure Virtual Machine"/>
<br /></p>
<br />
<br />
Go to Tools > Active Directory Users and Computers:
<br />
<p align="center">
<br/>
<img src="https://i.imgur.com/TND5RNm.png" height="80%" width="80%" alt="Microsoft Azure Virtual Machine"/>
<br /></p>
<br />
<br />
In Active Directory Users and Computers go to infotechaaron.local > Users and notice we have a helpdesk user account already created (there is also several Security Groups that have been created):
<br />
<p align="center">
<br/>
<img src="https://i.imgur.com/xjs8g9s.png" height="80%" width="80%" alt="Microsoft Azure Virtual Machine"/>
<br /></p>
<br />
<br />
Next, open PowerShell again under admin mode and we need to import the active directory module by issuing the following command:

import-module activedirectory
<br />
<p align="center">
<br/>
<img src="https://i.imgur.com/XiDfBqw.png" height="80%" width="80%" alt="Microsoft Azure Virtual Machine"/>
<br /></p>
<br />
<br />
Now issue the get-command new-aduser -syntax to see all the commands we can use to manage AD (notice the first one to add a new AD user). I’ll use that command to create a new AD user named Joe by issuing the new-aduser Joe command:
<br />
<p align="center">
<br/>
<img src="https://i.imgur.com/inY7O4Y.png" height="80%" width="80%" alt="Microsoft Azure Virtual Machine"/>
<br /></p>
<br />
<br />
Then go back into Active Directory Users and Computers > Refresh:
<br />
<p align="center">
<br/>
<img src="https://i.imgur.com/DF6c0Go.png" height="80%" width="80%" alt="Microsoft Azure Virtual Machine"/>
<br /></p>
<br />
<br />
Now we can see the new AD user Joe has been created:
<br />
<p align="center">
<br/>
<img src="https://i.imgur.com/m5WvLWy.png" height="80%" width="80%" alt="Microsoft Azure Virtual Machine"/>
<br /></p>
<br />
<br />
So that was a brief tutorial on creating AD user via PowerShell. You just need to make sure to import the active directory module first.

<h3>Other useful PowerShell commands are:</h3>h3>

whoami
PS C:\Users\helpdesk> whoami
infotechaaron\helpdesk

whoami tells us that we are logged into the user helpdesk on the infotechaaron domain.

whoami /fqdn
PS C:\Users\helpdesk> whoami /fqdn
CN=helpdesk,CN=Users,DC=infotechaaron,DC=local

whoami /fqdn tells us a little more such as the Domain Controller is infotechaaron.local

Finally, let’s enable the new AD user Joe’s account by right-clicking on his name > Enable Account:
