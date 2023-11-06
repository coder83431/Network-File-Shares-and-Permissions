<p align="center">
<img src="https://imgur.com/ocgeUoz.png" alt=" alt="osTicket logo"/>
</p>

<h1>Network File Shares and Permissions </h1>
In this tutorial, we will create and test some file shares and security groups. The file shares created will be set to Read, Write, or Deny access to individual users or groups.


<h2>Environments and Technologies Used</h2>

- Microsoft Azure 
- Remote Desktop

<h2>Operating Systems Used </h2>

- Windows 10</b> (version 22H2)
- Windows Server 2022                                                               

<h2>List of Prerequisites</h2>

- Microsoft Active Directory
- Microsoft Azure
- Microsoft Powershell (ISE)
- Remote Desktop                                                                 
- A domain admin account set up on a Remote Desktop VM.
- A client VM desktop connected to the domain VM through Active Directory.
- A file containing a list of employees downloaded into the domain account's Active Directory. We will be logging into the client's VMs under one of the employee's accounts.

<h2>Installation Steps</h2>

 <p>
1. Connect into DC-1 as your domain admin account (mydomain.com\jane_admin).

</p>                                                                                                    
                                                                                                     
<p>
<img src= "https://imgur.com/bPK5voU.png" " height="80%" width="80%" alt="Disk Sanitization Steps" />
</p>

<p>
                                                                                                 
                                                                                                 
                                                                                                 
2. Connect/log into Client-1 as a normal user (mydomain\<someuser>). For this demonstration, I will be logged into an account as a user named "bubo sud".
</p>
<br />

<p>
<img src="https://imgur.com/6ygCAOi.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
3. On DC-1, on the C:\ drive, create 4 folders: “read-access”, “write-access”, “no-access”, and “accounting”.
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
We will skip assigning any permissions to the "accounting" folder for now.
                                                                               



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
                                                                                                                                                                                          
 
                                                                                                
                                                                                                                                                                                        
                                                                                                
6. Try to access the folders you just created. Being the domain user "bubo sud", notice how you can access but can't write in the folder named "read-access". 

                                                                                               
                                                                                               
</p>
<br />

<p>
<img src="https://imgur.com/iUhcIO1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
                                                                                               
<p>
<img src="https://imgur.com/s5mFFkp.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
                                                                                                          
                                                                                               
7. Now we will focus on assigning permissions to the folder named "accounting". We will make the user "bubo sud" a member of a security group that will have the ability to perform actions on the "accounting" folder. Go back to DC-1, and in Active Directory, create a security group called “ACCOUNTANTS”. 



</p>
<br />

<p>
<img src="https://imgur.com/I2pvseV.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
8. On the “accounting” folder you created earlier, set the following permissions:
Folder: “accounting”, Group: “ACCOUNTANTS”, Permissions: “Read/Write”.

</p>
<br />

<p>
<img src="https://imgur.com/4Zp6BsM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
9. On Client-1, as  <someuser>, try to access the accountants folder. It should fail. This is because the users is currently given the permissions of "Domain Users" and thus don't have access to the "accounting" folder.


</p>
<br />


</p>
<br />

<p>
<img src="https://imgur.com/3u7W5FJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
10. Log out of Client-1 as  <someuser>. On DC-1, make <someuser> a member of the “ACCOUNTANTS”  Security Group.

</p>

<p>
<img src="https://imgur.com/tKQjZWm.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>                                                                                      
                                                                                               
<p>
11. Sign back into Client-1 as <someuser> and try to access the “accounting” share in \\DC-1\. Now the user should have access to the "accounting" folder.
</p>
 
 <p> 12. Don't forget to clean up and delete your resources (resource groups and VMs) after completing this lab in order to prevent draining all of your free Microsoft Azure credits.
 </p>
<br />
