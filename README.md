<p align="center">
<img src="https://imgur.com/ocgeUoz.png" alt=" alt="osTicket logo"/>
</p>

<h1>DNS: Network File Shares and Permissions </h1>
This tutorial we will create and test some file shares and security group. This will create these file shares while logged on into a domain admin account. We will observe the file permissions that we were granted and denied access within a normal user account. The domain admin and normal user account is connected to each other through Active Directory.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop

<h2>Operating Systems Used </h2>

- Windows 10</b> (version 22H2)

<h2>List of Prerequisites</h2>

-Microsoft Active Directory
-Microsoft Azure
-Microsoft Powershell (ISE)
-A domain admin account setted up on a Remote Desktop VM.
-A client VM desktop connected to the domain VM through Active Directory.
-A file containing a list of employees downloaded into the domain accounts Active Directory.
-Remote Desktop

<h2>Installation Steps</h2>


<p>
<img src = "https://i.imgur.com/GFYFR0R.png" " height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
 <p>
1. Connect/log into DC-1 as your domain admin account (mydomain.com\jane_admin).

</p>                                                                                                    
                                                                                                     
<p>
<img src= "https://imgur.com/bPK5voU.png" " height="80%" width="80%" alt="Disk Sanitization Steps" />
</p>

<p>
                                                                                                 
                                                                                                 
                                                                                                 
2. Connect/log into Client-1 as a normal user (mydomain\<someuser>).
</p>
<br />

<p>
<img src="https://imgur.com/6ygCAOi.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
3. On DC-1, on the C:\ drive, create 4 folders: “read-access”, “write-access”, “no-access”, “accounting”.
</p>
<br />

<p>
<img src="https://imgur.com/Lq68YV5.png" width="80%" alt="Disk Sanitization Steps"/>
</p>
        
<p>
<img src="https://imgur.com/gAD99s9.png" width="80%" alt="Disk Sanitization Steps"/>
</p>
                                                                                       
                                                                                                                                                                    
<p>
4. Set the following permissions (share the folder) for the “Domain Users” group:
Folder: “read-access”, Group: “Domain Users”, Permission: “Read”.
Folder: “write-access”,  Group: “Domain Users”, Permissions: “Read/Write”
Folder: “no-access”, Group: “Domain Admins”, “Permissions: “Read/Write”
(Skip accounting for now)



</p>
<br />

<p>
<img src="https://imgur.com/oXede5t.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
5. On Client-1, navigate to the shared folder (start, run, \\dc-1)
</p>
<br />

<p>
<img src="https://imgur.com/cHX8FIE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
                                                                                               
<p>
<img src="https://imgur.com/mUGrs1e.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
                                                                                               
<p>
<img src=" https://imgur.com/QC6v5NY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>                                                                                               
                                                                                               
<p>
6.Try to access the folders you just created. Which folders can you access?

                                                                                               
                                                                                               
</p>
<br />

<p>
<img src="https://i.imgur.com/SbhSS6V.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
7. Go back to DC-1, in Active Directory, create a security group called “ACCOUNTANTS”



</p>
<br />

<p>
<img src="https://i.imgur.com/wVSvcC6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
8. On the “accounting” folder you created earlier, set the following permissions:
Folder: “accounting”, Group: “ACCOUNTANTS”, Permissions: “Read/Write”.

</p>
<br />

<p>
<img src="https://i.imgur.com/U0zZqC1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
9. On Client-1, as  <someuser>, try to access the accountants folder. It should fail. 


</p>
<br />

<p>
<img src="https://i.imgur.com/IdTzZWd.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
10. Log out of Client-1 as  <someuser>

</p>
<br />

<p>
<img src="https://i.imgur.com/0LOpcLJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
11. On DC-1, make <someuser> a member of the “ACCOUNTANTS”  Security Group.

</p>

<p>
Sign back into Client-1 as <someuser> and try to access the “accounting” share in \\DC-1\ - Does it work now?
</p>
<br />
