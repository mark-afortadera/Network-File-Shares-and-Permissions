<p align="center">
<img src="https://imgur.com/PNiJftC.png height="80% width="80%" alt="Disk Sanitization Steps"/>
</p>

<h1>Managing Network File Shares and Permissions using Active Directory in Microsoft Azure</h1>
In this Demonstration, we will understand how to create and manage Network File Shares and permissions in a Windows Domain Environment. 
<br />


<h2>Environments and Technologies Used</h2>

- Active Directory running in Microsoft Azure using Virtual Machines (DC-1 and Client-1)
- Remote Desktop

<h2>Operating Systems Used </h2>

- Windows 10 Pro (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Sharing out resources over the network
- Creating File Shares to allow Read, Write, or Deny access to individual users or groups
- Setting Up and Testing File Shares
- Using Active Directory Security Groups for Access Control

<h2>Setting Up Network File Shares</h2>
<br />

<h2>Create Shared Folders on "DC-1"</h2>
<br />

<h3>Objective:</h3>
<p>Create and manage file shares with various permissions in a Windows domain environment.</p>
<br />

<h3>1. Log into Domain Controller and "Client-1"</h3>
<br />

![Screenshot 2025-02-21 190805](https://github.com/user-attachments/assets/672d4eae-ff22-4a7b-9dec-12636622e016)

<p>- Log into "DC-1" as a domain admin: Use credentials: mydomain.com\jane_admin</p>
<br />

<h3>2. Open File Explorer</h3>
<br />

![Screenshot 2025-02-21 191200](https://github.com/user-attachments/assets/99570b01-7494-4794-9064-00441f128787)

<h3>3. Create some sample File Shares</h3>
<br />

![Screenshot 2025-02-21 191341](https://github.com/user-attachments/assets/b78b74e9-6a3c-4d3d-8928-088416b9bc65)

<p>- On DC-1, navigate to the C:\ drive and create the following folders:</p>
<p><li>read-access</li></p>
<p><li>write-access</li></p>
<p><li>no-access</li></p>
<p><li>accounting</li></p>
<br />

<h3>4. Set Permissions and Share the Folders:</h3>
<br />

![Screenshot 2025-02-21 191728](https://github.com/user-attachments/assets/c5e54207-c51b-4e9a-a63a-aa1205bdb4da)
![Screenshot 2025-02-21 191933](https://github.com/user-attachments/assets/f8a07882-5668-47d1-8dc3-84a7a89eec5a)
![Screenshot 2025-02-21 192037](https://github.com/user-attachments/assets/755bfd9d-beb8-449d-a456-cf087456554d)

<p><li>"read-access": Assign Domain Users group "Read" permission.</li></p>
<p><li>"write-access": Assign Domain Users group "Read/Write" permissions.</li></p>
<p><li>"no-access": Assign Domain Admins group "Read/Write" permissions.</li></p>
<p><li>(Skip configuring permissions for "accounting" for now.)</li></p>
<br />

<h2> Attempt to access File Shares as a Normal User</h2>
<br />

<h3>Objective:</h3>
<p>Test access to shared folders based on user roles.</p>
<p>- Which folders can be access?</p>
<p>- Which folders can be created files in?</p>
<br />

<h3>1. Test Access from "Client-1"</h3>
<br />

<p>- Log into Client-1 as a normal user:</p>
<p><li>Use credentials: "mydomain\menu.suq" or any user that has been created in "DC-1".</li></p>
<br />

<h3>2. On Client-1, navigate to the shared folders:</h3>
<br />

![Screenshot 2025-02-21 192230](https://github.com/user-attachments/assets/cb8b4858-b542-45c3-90f6-0bf672ab23bf)

<p>- Open File Explorer then type \\DC-1, and press Enter.</p>
<br />

<h3>3. Try accessing each folder:</h3>
<br />

![Screenshot 2025-02-21 192433](https://github.com/user-attachments/assets/a321bcd2-d13e-4008-a111-30a5f897ff7a)
![Screenshot 2025-02-21 192441](https://github.com/user-attachments/assets/fbc7bcc0-ff9b-47f5-81b6-027eaef7c80d)

<p><li>In "read-access" folder, the user is allowed to open folders but no permission to create files.</li></p>
<br/ >

![Screenshot 2025-02-21 192512](https://github.com/user-attachments/assets/105c3546-bf92-4762-8df8-e39ab8f121eb)
![Screenshot 2025-02-21 192520](https://github.com/user-attachments/assets/f4b05e8f-a482-49f7-bc25-05a49fa29ee7)

<p><li>In "write-access" folder, the user is allowed to open and create files or folders.</li></p>
<br/ >

![Screenshot 2025-02-21 192602](https://github.com/user-attachments/assets/e5a7ca80-f4c8-4679-9477-0c7cab5b18d3)
![Screenshot 2025-02-21 192624](https://github.com/user-attachments/assets/09b97435-c88b-4507-9c0f-e0a27f727170)

<p><li>In "no-access" folder, the user's access is denied.</li></p>
<br/ >

<h2> Create a Security Group and assign permissions.</h2>
<br />

<h3>Objective:</h3>
<p>Configured and validated Active Directory security group permissions.</p>
<br />

<h3>1. Configure Group-Based Permissions</h3>
<br />

![Screenshot 2025-02-21 193834](https://github.com/user-attachments/assets/5af506c5-d191-4a1c-9d83-6f48c0827bf6)
![Screenshot 2025-02-21 193933](https://github.com/user-attachments/assets/6875f7be-c31d-4a44-bfe8-15bc2a266de9)

<p>- In Active Directory, create a OU folder "_GROUPS".</p>
<br />

![Screenshot 2025-02-21 194006](https://github.com/user-attachments/assets/a51a7dcc-424b-45fa-96a6-80ab9a77dc2b)
![Screenshot 2025-02-21 194028](https://github.com/user-attachments/assets/f7d14d32-c031-4aca-85b4-b134d3079f1e)

<p>- Within the OU "_GROUPS" folder, create a security group named "ACCOUNTANTS".</p>
<br />

<h3>2. Set permissions for the accounting folder:</h3>
<br />

![Screenshot 2025-02-21 194229](https://github.com/user-attachments/assets/c6a94b7e-7402-4d41-9d6c-176be55b5f71)

<p>- Onthe “accounting” folder you created earlier, set the following permissions:</p>
<p><li>Folder: “accounting”, Group: “ACCOUNTANTS”, Permissions: “Read/Write”</li></p>

<h3>3. Test Access Before Adding User to Group</h3>
<br />

![Screenshot 2025-02-21 194326](https://github.com/user-attachments/assets/44c2a8da-4899-4920-854b-57509e0eb010)

<p>- On "Client-1", log in as "menu.suq" and attempt to access the accounting folder:</p>
<p><li>The access attempt should fail.</li></p>
<p>- Log out of "Client-1" as "menu.suq".</p>
<br />

<h3>4. Add User to Security Group and Re-test</h3>
<br />

![Screenshot 2025-02-21 194458](https://github.com/user-attachments/assets/2eac3a77-2619-4d5c-a643-e35516fb2490)
![Screenshot 2025-02-21 194512](https://github.com/user-attachments/assets/8d544417-0ad1-4a53-9be3-1ef1c20ea942)

<p>- On "DC-1", add "menu.suq" to the ACCOUNTANTS security group.</p>
<br />

![Screenshot 2025-02-21 194626](https://github.com/user-attachments/assets/47e488be-273d-4740-9371-8c95066ab054)

<p>- Log back into "Client-1" as "menu.suq".</p>
<br />

![Screenshot 2025-02-21 195244](https://github.com/user-attachments/assets/abb49445-4f4f-4383-916c-8571d9c5decc)

<p>- Try to access the "accounting" folder share in "\\DC-1\accounting".</p>
<p><li>Access should now be granted.</li></p>
