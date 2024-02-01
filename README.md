<p align="center">
<img src=https://github.com/ClayWunder/File-Share-Permissions/assets/157168474/3c024d8e-ee73-4fa8-85c7-115947491897)
</p>

<h1>Configuring File Sharing and Permissions in Active Directory.</h1>

This tutorial outlines the configuration and assignment of File Sharing and Permissions in Active Directory. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Microsoft Active Directory
- Remote Desktop
- File Explorer

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Windows Server 2022

<h2>High-Level Deployment and Configuration Steps</h2>

- Step 1 - Create Sample File Shares with Various Permissions.
- Step 2 - Attempt to Access File Shares as Normal User.
- Step 3 - Create "ACCOUNTANTS" Security Group, Assign Permissions and Test.
- Cleanup

<h2>Create Sample File Shares with Various Permissions</h2>

- Log into DC-1 as domain admin account. (mydomain.com/jane_admin)
- Log into Client-1 as normal user.

![Screenshot 2024-02-01 at 2 47 44 PM](https://github.com/ClayWunder/File-Share-Permissions/assets/157168474/f9824749-43f9-4813-87ba-dc0d7648e14d)

On DC-1, on C: create 4 folders. 
- "read-access" "write_access" "no-access" "accounting"

![Screenshot 2024-02-01 at 2 50 35 PM](https://github.com/ClayWunder/File-Share-Permissions/assets/157168474/f3c89d60-6421-4185-ae49-f0a5ba1258ed)
![Screenshot 2024-02-01 at 2 51 01 PM](https://github.com/ClayWunder/File-Share-Permissions/assets/157168474/01096795-8b87-48da-8948-2f6d9fa3dbd6)
![Screenshot 2024-02-01 at 2 51 22 PM](https://github.com/ClayWunder/File-Share-Permissions/assets/157168474/d2c22321-7151-4a08-bbdc-9a8b9b8cb362)

Set the following permissions (share the older) for the "Domain Users" group:
- Folder: "read-access", Group: "Domain users", Permission: "read"
- Folder: "write-access", Group: "Domain Users", Permission: "read/write"
- Folder: "no-access", Group: "Domain Admins", Permission: "read/write"

<h2>Attempt to Accss File Shares as Normal User</h2>

![Screenshot 2024-02-01 at 2 53 39 PM](https://github.com/ClayWunder/File-Share-Permissions/assets/157168474/e65123aa-1020-4050-befe-11321b56c6d9)

On Client-1, navigate to shared folder. (start, run, \\dc-1)

Try to access the newly created folders. 

<h2>Create "ACCOUNTANTS" Security Group, Assign Permissions and Test</h2>

![Screenshot 2024-02-01 at 2 57 57 PM](https://github.com/ClayWunder/File-Share-Permissions/assets/157168474/7e722b9a-79df-4803-b313-d6cb5019a6db)

Login to DC-1, in Active Directory, create security group called "ACCOUNTANTS"

![Screenshot 2024-02-01 at 3 02 13 PM](https://github.com/ClayWunder/File-Share-Permissions/assets/157168474/7eb654fc-7ef1-41e6-88ef-958c08a54198)

Set permissions for "accounting" folder as follows:
- Folder: "accounting", Group: "ACCOUNTANTS", Permission: "read/write"

![Screenshot 2024-02-01 at 3 03 33 PM](https://github.com/ClayWunder/File-Share-Permissions/assets/157168474/7a3f5ecf-2859-4d7b-88fe-9f322f0b194f)

On Client-1, normal user should not be able to access the accountants folder in DC-1.

Logout of Client-1.

![Screenshot 2024-02-01 at 3 05 01 PM](https://github.com/ClayWunder/File-Share-Permissions/assets/157168474/a0f7254f-97c4-4284-b88d-80a3d5ca9a03)

Login to DC-1 and make user a member of ACCOUNTANTS security group.

![Screenshot 2024-02-01 at 3 12 30 PM](https://github.com/ClayWunder/File-Share-Permissions/assets/157168474/47576f10-ac47-44e1-84fd-1fa3c1d3d561)

Login to Client-1 as user and attempt to access "accounting" folder on DC-1.



