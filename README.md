# Deploy Active Directory Lab  
This repository provides a step-by-step guide to deploying Active Directory in a lab environment. Follow the instructions to set up a Domain Controller, create users, and configure a client machine.

## 🚀 Overview  
This lab covers:  
- Installing **Active Directory Domain Services (AD DS)**  
- Promoting a server to a **Domain Controller (DC)**  
- Creating and managing **Organizational Units (OUs)**  
- Adding a **Domain Admin** user  
- Joining a **client machine** to the domain  
- Configuring **Remote Desktop access**  
- Creating additional users via **PowerShell scripting**  

---

## Part 1: Install Active Directory  

### 1️⃣ Install Active Directory Domain Services (AD DS)  
1. Log in to **DC-1** and install **Active Directory Domain Services (AD DS)**.  

![Screenshot 2025-03-20 115512](https://github.com/user-attachments/assets/7db84f52-9df6-4856-bd51-13a5d7d49f46)

![Screenshot 2025-03-20 115557](https://github.com/user-attachments/assets/dd759993-b65c-4cad-875f-56e2658afa91)

![Screenshot 2025-03-20 115624](https://github.com/user-attachments/assets/e6261c3d-2b77-4eb2-99a8-93ed4fc221d5)

![Screenshot 2025-03-20 120141](https://github.com/user-attachments/assets/0a5b9b62-cc31-456b-96de-0ada5fa37b73)


2. Promote the server as a **Domain Controller (DC)** and set up a new forest:  
   - Example: `mydomain.com` (can be any name, just remember it).  

![Screenshot 2025-03-20 125125](https://github.com/user-attachments/assets/683bb930-637a-4967-8005-5807653b987f)

![Screenshot 2025-03-20 125312](https://github.com/user-attachments/assets/e5fef6eb-df43-4fe2-809f-26a3b24f8175)


3. Restart the server and log in as:  
   ```  
   mydomain.com\labuser  
   ```  

![Screenshot 2025-03-20 131022](https://github.com/user-attachments/assets/88776657-af5d-4327-b5f7-037fbfce2f64)


### 2️⃣ Create a Domain Admin User  
1. Open **Active Directory Users and Computers (ADUC)**.  

![Screenshot 2025-03-20 131740](https://github.com/user-attachments/assets/3a83c656-f70e-4055-a051-ffe0da02d5a4)


2. Create an **Organizational Unit (OU)** named **`_EMPLOYEES`**.  

![Screenshot 2025-03-20 131856](https://github.com/user-attachments/assets/d4fb4ac7-3fa6-4fd1-9719-22085b6d97e2)

3. Create another OU named **`_ADMINS`**.  

![Screenshot 2025-03-20 131914](https://github.com/user-attachments/assets/4cb94776-00fc-47fb-876b-b768792b4e8d)

4. Add a new user:  
   - **Name:** Jane Doe  
   - **Username:** `jane_admin`  
   - **Password:** `Cyberlab123!`  

![Screenshot 2025-03-20 132432](https://github.com/user-attachments/assets/8eb020e2-a001-432b-8f65-626ac749a0e8)


5. Add `jane_admin` to the **Domain Admins** security group.  

![Screenshot 2025-03-20 133511](https://github.com/user-attachments/assets/bef9c91c-e661-4dd6-b993-2787e5a2f641)


6. Log out of **DC-1** and log back in as:  
   ```  
   mydomain.com\jane_admin  
   ```  

![Screenshot 2025-03-20 134236](https://github.com/user-attachments/assets/b2f61d0c-4e0d-4c2a-875f-a48d8c4078cf)


7. Use `jane_admin` as the **primary admin account** from now on.  

---

## Part 2: Join a Client Machine to the Domain  

### 3️⃣ Join Client-1 to the Domain  
1. Log into **Client-1** as the original local admin (`labuser`).  

![Screenshot 2025-03-20 135053](https://github.com/user-attachments/assets/40a575e7-c557-42c7-9706-d995dc68f473)


2. Join **Client-1** to the domain (`mydomain.com`).  

![Screenshot 2025-03-20 135448](https://github.com/user-attachments/assets/ef7440e2-f9a4-40f1-9fa1-49d6382f78c6)

![Screenshot 2025-03-20 135637](https://github.com/user-attachments/assets/bacd24f5-e3ad-4e9c-b774-4a532fd2f5b7)

![Screenshot 2025-03-20 140005](https://github.com/user-attachments/assets/917964d1-d13f-4c01-b1d4-6b8a5163c303)


3. Restart the machine.  

![Screenshot 2025-03-20 140025](https://github.com/user-attachments/assets/e6edaa9a-ad04-4526-b20b-2c88847ad509)


4. Log in to the **Domain Controller** and verify Client-1 appears in **ADUC**.  

![Screenshot 2025-03-20 140320](https://github.com/user-attachments/assets/96f7449e-9191-4791-b817-2fe4f0947e61)


5. Create an OU named **`_CLIENTS`** and move **Client-1** into it.  

![Screenshot 2025-03-20 140443](https://github.com/user-attachments/assets/ee3fd002-53eb-424c-a4b1-f9ca31d6c50b)

![Screenshot 2025-03-20 140640](https://github.com/user-attachments/assets/108f1aae-feec-4a21-9cb5-74282418afdc)

---

## Part 3: Configure Remote Desktop Access  

### 4️⃣ Enable Remote Desktop for Domain Users  

1. Log into **Client-1** as `mydomain.com\jane_admin`.  

![image](https://github.com/user-attachments/assets/728e2b80-7647-484c-a7dd-65430662a92d)

2. Open **System Properties**.  

![Screenshot 2025-03-20 154040](https://github.com/user-attachments/assets/7f446b12-2295-4c2f-b48c-4926f169c936)

3. Click **Remote Desktop** settings.  

4. Allow **Domain Users** access to Remote Desktop.  

![Screenshot 2025-03-20 154549](https://github.com/user-attachments/assets/d33a791e-860e-4e17-afe6-eeb1845a39c8)



🔹 **Note:** This setting can also be applied via **Group Policy (GPO)** to manage multiple systems at once.  

---

## Part 4: Create Multiple User Accounts  

### 5️⃣ Bulk Create Users via PowerShell  

1. Log into **DC-1** as `jane_admin`.  

2. Open **PowerShell ISE** as Administrator.  

![Screenshot 2025-03-20 154901](https://github.com/user-attachments/assets/37c2ea4b-7875-495b-8c7c-3dcf34133fed)

3. Create a new script file and paste the provided script.  

![image](https://github.com/user-attachments/assets/ac4e3d7d-204e-453d-81cd-29fa7c19d5f5)

4. Run the script and observe user accounts being created.  

![Screenshot 2025-03-20 155601](https://github.com/user-attachments/assets/210fdf0e-3b66-4b32-b00f-bbb79a708f12)

![Screenshot 2025-03-20 155610](https://github.com/user-attachments/assets/095c9ba2-9649-4f71-9b33-ad19d6283972)

5. Open **ADUC** and verify the users appear under **`_EMPLOYEES`**.  

![image](https://github.com/user-attachments/assets/5a601320-6328-4c26-a34c-e187ac2c13c6)

6. Attempt to log into **Client-1** using one of the newly created accounts.  

![Screenshot 2025-03-20 160257](https://github.com/user-attachments/assets/633b2b71-8da3-4c3e-8cd7-26ad72938426)

![image](https://github.com/user-attachments/assets/e1b81308-b2ee-4668-9360-f13c7a25648c)

![Screenshot 2025-03-20 160554](https://github.com/user-attachments/assets/e1cc6793-c979-4b94-a6f9-d55b4360b447)

---

## ✅ Final Steps & Verification  
- Confirm that **Client-1** is successfully joined to the domain.  
- Ensure **users can log in** to Client-1 with domain credentials.  
- Verify **Remote Desktop access** is functioning correctly.  
- Check that **all created users** are properly listed in **ADUC**.  

---

## 📝 Notes  
- This lab can be extended to include **Group Policy (GPO) configurations**, **File Sharing**, or **Advanced AD Security Settings**.  
- Future enhancements may include **automating user/group policies** and **additional administrative tasks**.  

---


### 🎯 Next Steps:  
- Explore **[Group Policy (GPO) configuration](https://github.com/tameya-w/azure-network-protocols)**.  
- Set up **File Sharing & Permissions**.  
- Implement **Basic AD Security Policies**.  
