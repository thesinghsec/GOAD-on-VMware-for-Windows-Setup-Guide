# Troubleshooting
## Network Collide Error:
- OPS, got an network error:
  
  ![image](https://github.com/user-attachments/assets/17fb91f5-7295-4f6a-a287-0e406f14909a)

- Open **VagrantFile** and edit Machines IP as per VMWare **Host-Only** network.
  ```"<path-to-OS>\OS\GOAD-main\GOAD-main\ad\GOAD\providers\vmware\Vagrantfile”```
  
![image](https://github.com/user-attachments/assets/825419ea-6bb3-4195-a3bd-5a5a4af8e624)

- I have changed 56 to 124, and keeps remaining address same.
  
  ![image](https://github.com/user-attachments/assets/31e36e5b-79ff-42b6-b18f-41ebf375638a)

- - Again run the cmd and boom it works:

  ```bash
  vagrant up
  ````

  ---
  ## NuGet Error:
  - The first error got is on DC02, which states missing `NuGet`.
    
    ![image](https://github.com/user-attachments/assets/ab500d04-322e-4b3a-934f-23a885f5f299)

- So, let’s manually install it, navigate to **DC02** and open **PowerShell as Administrator** and run the following cmd:
  ```powershell
  [Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
  Install-PackageProvider -Name NuGet -Force
  ```
  
  ![image](https://github.com/user-attachments/assets/14fef9c6-7b9a-4fdd-a865-2388bc1369db)

- Error resolved!

  ---
## Error Joining Domain:
- Oh, now second error displays, looks like error with joining domain, hummmmmm, let’s solve it.
  
    ![image](https://github.com/user-attachments/assets/56a9b4b3-fd62-4f13-8269-5703b17c25b4)

- Simply I just reboot the machine and re-run the script, error resolved.

---
## SQL Server Error:
- Next error we have faced with SQL server.
  
  ![image](https://github.com/user-attachments/assets/b3383484-125b-4acd-984c-e803bfacdc60)

- Try to reboot all VMs and retry with the cmd below (Specific for setting up servers):
  ```bash
  ansible-playbook -i ../ad/GOAD/data/inventory -i ../ad/GOAD/providers/vmware/inventory  servers.yml
  ```
- On running again, if we get the error like below. It means SQL server is already exists on VM. Try uninstalling the SQL Server entirely from machine this error is coming, in this case SRV03 has error with SQL.
  
  ![image](https://github.com/user-attachments/assets/67c1ff80-1c71-415e-a23c-faf4049b950f)

- I Noticed that on SRV02, SQL Server(SQLEXPRESS) service keeps running while in SRV03 it frequently stops even after turning it on. I messed with SQL Configuration Manager also but everything seems correctly configured.

  ![image](https://github.com/user-attachments/assets/d9315539-1c4e-4d6b-adbb-dd9addca79db)
  ![image](https://github.com/user-attachments/assets/bb689075-cce4-45db-b633-90cf10960cae)

- Let’s navigate to **SRV03** machine > Open **Control Panel** _(Control Panel\Programs\Programs and Features)_ > **Uninstall** all software related to **SQL Serve**r. Example: Highlighted below.
  
  ![image](https://github.com/user-attachments/assets/27c9401e-e2ae-496a-b7bb-d7cc2598eb36)

- Next, move to **C:\ drive and Delete “Setup” folder** (If still present).
  
  ![image](https://github.com/user-attachments/assets/b448cb23-b7f0-4a59-b1e2-b7e1c9510a7d)

- Move to **C:\Program Files and Delete Microsoft SQL Server folder** (If present).
  
  ![image](https://github.com/user-attachments/assets/7a3d6963-7701-4770-9218-85783ab4cf85)

-  Reboot the machine.
- Run the cmd again on main windows host:
  ```bash
  ansible-playbook -i ../ad/GOAD/data/inventory -i ../ad/GOAD/providers/vmware/inventory  servers.yml
  ``` 

- This will install fresh SQL Server and configure it automatically. Error resolved.

---
## Active Directory Error:
- Next error relates to specifically Active Directory computer object.
  
  ![image](https://github.com/user-attachments/assets/9b396a41-0526-4ee5-b2e6-5d76327965b8)

- First try with **rebooting** the machine, see if resolves the problem.
- If to navigate to **DC02 >** Search **Active Directory Domains and Trusts.**
  
  ![image](https://github.com/user-attachments/assets/1cfe5003-a35f-4a44-9c60-d336fc61ca63)

- You will get interface like below:
  
  ![image](https://github.com/user-attachments/assets/3c8eed66-5762-4c44-8341-e1d4aeff6d02)

- Right click on** Domain > Select Properties**.

  ![image](https://github.com/user-attachments/assets/94e57247-db3b-4487-91d4-47ce90cab916)

- Select **essos.local > Remove** from both incoming and outgoing trusts** > Apply > OK.**
  
  ![image](https://github.com/user-attachments/assets/ec2f037f-9ec3-47c8-97e6-d66aaa0c34a1)

- Reboot the machine, and re-run the script:
  ```bash
  ansible-playbook -i ../ad/GOAD/data/inventory -i ../ad/GOAD/providers/vmware/inventory  main.yml
  ```
- This will recreate trusts and it’s objects, error resolved.

---
  
