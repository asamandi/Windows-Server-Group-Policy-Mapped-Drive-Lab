## Windows Server Group Policy Mapped Drive Lab

### Overview
- This lab demonstrates how to configure and troubleshoot Group Policy in a Windows Server Active Directory domain environment.
- The goal of this lab was to automatically map a network drive for IT users and apply a basic user restriction through Group Policy.

----------------------------------------------------------------
### Lab Environment
- Server Name: DC1
- Server OS: Windows Server 2022
- Client Name: PC1
- Client OS: Windows 11
- Domain: amir.local
- Network: VirtualBox Internal Network - AD-Lab  

----------------------------------------------------------------
### Existing Resources
- Domain Controller: DC1
- Domain: amir.local
- User: ali.it
- Security Group: IT-Group
- Shared Folder: \\DC1\IT  

----------------------------------------------------------------
### Group Policy Object
- GPO Name: IT-Mapped-Drive-Policy
- Linked OU: IT  

----------------------------------------------------------------
### Configured Settings

Mapped Drive:
- Drive Letter: I:
- Drive Path: \\DC1\IT
- Drive Label: IT Share
- Action: Update  

User Restriction:
- Prohibit access to Control Panel and PC settings: Enabled  

----------------------------------------------------------------
### Skills Demonstrated
- Group Policy Management
- OU-based GPO linking
- Mapped network drive deployment
- User Configuration settings
- Control Panel restriction
- Group Policy update
- Group Policy verification
- Mapped drive troubleshooting
- DNS and domain troubleshooting  

----------------------------------------------------------------
### Verification Commands
- gpupdate /force
- gpresult /r
- net use
- dir I:
- dir \\DC1\IT
- whoami
- whoami /groups
- ipconfig /all
- nslookup amir.local
- ping DC1  

----------------------------------------------------------------
### Troubleshooting Notes

### Issue:
- Mapped drive does not appear.

Most Likely Cause:
- The GPO is linked to the wrong OU, the user is in the wrong OU, DNS is misconfigured, or the user has not logged out and logged back in.

Fix:
- Verify that the GPO is linked to the IT OU, confirm that ali.it is inside the IT OU, make sure PC1 uses DC1 as DNS, run gpupdate /force, then log out and log back in.

### Issue:
- The user cannot access the mapped drive.

Most Likely Cause:
- The shared folder path is wrong or the user does not have the correct share and NTFS permissions.

Fix:
- Verify that \\DC1\IT is accessible manually. Confirm the user is a member of IT-Group and that IT-Group has access to the IT shared folder.

----------------------------------------------------------------

### Screenshots

[001-gpmc-open.png](https://github.com/asamandi/Windows-Server-Group-Policy-Mapped-Drive-Lab/blob/main/Screenshots/001-gpmc-open.png)
- Shows Group Policy Management Console opened on DC1.

[002-gpo-created.png](https://github.com/asamandi/Windows-Server-Group-Policy-Mapped-Drive-Lab/blob/main/Screenshots/002-gpo-created.png)
- Shows the new Group Policy Object created for the mapped drive and workstation settings.

[003-gpo-linked-to-it-ou.png](https://github.com/asamandi/Windows-Server-Group-Policy-Mapped-Drive-Lab/blob/main/Screenshots/003-gpo-linked-to-it-ou.png)
- Shows the GPO linked to the IT OU so the policy applies to IT users.

[004-gpo-edit.png](https://github.com/asamandi/Windows-Server-Group-Policy-Mapped-Drive-Lab/blob/main/Screenshots/004-gpo-edit.png)
- Shows the GPO being edited in Group Policy Management Editor.

[005-mapped-drive-policy-created-01.png](https://github.com/asamandi/Windows-Server-Group-Policy-Mapped-Drive-Lab/blob/main/Screenshots/005-mapped-drive-policy-created-01.png)
- Shows the mapped drive policy configuration process.

[005-mapped-drive-policy-created-02.png](https://github.com/asamandi/Windows-Server-Group-Policy-Mapped-Drive-Lab/blob/main/Screenshots/005-mapped-drive-policy-created-02.png)
- Shows the mapped drive location and drive letter settings.

[005-mapped-drive-policy-created-03.png](https://github.com/asamandi/Windows-Server-Group-Policy-Mapped-Drive-Lab/blob/main/Screenshots/005-mapped-drive-policy-created-03.png)
- Shows the completed mapped drive Group Policy Preference configuration.

[006-control-panel-restriction-01.png](https://github.com/asamandi/Windows-Server-Group-Policy-Mapped-Drive-Lab/blob/main/Screenshots/006-control-panel-restriction-01.png)
- Shows the Control Panel restriction policy configuration.

[006-control-panel-restriction-02.png](https://github.com/asamandi/Windows-Server-Group-Policy-Mapped-Drive-Lab/blob/main/Screenshots/006-control-panel-restriction-02.png)
- Shows the Control Panel restriction policy configuration.

[007-gpupdate-success.png](https://github.com/asamandi/Windows-Server-Group-Policy-Mapped-Drive-Lab/blob/main/Screenshots/007-gpupdate-success.png)
- Shows Group Policy successfully refreshed on PC1 using gpupdate /force.

[008-gpresult-policy-applied.png](https://github.com/asamandi/Windows-Server-Group-Policy-Mapped-Drive-Lab/blob/main/Screenshots/008-gpresult-policy-applied.png)
- Shows the mapped drive and restriction policy applied to the domain user using gpresult /r.

[009-mapped-drive-visible.png](https://github.com/asamandi/Windows-Server-Group-Policy-Mapped-Drive-Lab/blob/main/Screenshots/009-mapped-drive-visible.png)
- Shows the mapped network drive visible in File Explorer on PC1.

[010-it-share-access-through-drive.png](https://github.com/asamandi/Windows-Server-Group-Policy-Mapped-Drive-Lab/blob/main/Screenshots/010-it-share-access-through-drive.png)
- Shows successful access to the IT shared folder through the mapped drive.

----------------------------------------------------------------

### Final Result

- The IT-Mapped-Drive-Policy was successfully applied to the IT user.
- When ali.it logged in to PC1, the IT shared folder was automatically mapped as drive I:.
- The user was able to access and create files through the mapped drive.
- Group Policy application was verified using gpupdate, gpresult, net use, and File Explorer.
