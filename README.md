# Wazuh-SIEM-Virtualbox-Installation
Step-by-step guide to deploy a Wazuh SIEM lab on VirtualBox using multiple virtual machines to simulate real-world enterprise cyberattacks and security incidents using Wazuh SIEM.

### Step 1: Install the virtualization software
The first step is to download the virtualization software that will be used to deploy **Wazuh** and the rest of the virtual machines.
In my case, I will use **VirtualBox**, as it is a comfortable and widely used option for lab environments.
You can download VirtualBox from the official website:
https://www.virtualbox.org/wiki/Downloads

Once on the VirtualBox website, select the **Download** option and choose the installer that matches your operating system.
In my case, I am using **Windows hosts**, so I selected the corresponding option.
<img width="1237" height="864" alt="image" src="https://github.com/user-attachments/assets/28e3305f-e992-41e4-8307-ceb92f9a4683" />
After downloading VirtualBox, completed the following steps:
1. Run the downloaded installer.
2. During the installation wizard:
    - Keep the **default settings**
    - Allow the installation of **network interfaces** when prompted
    - Accept any security warnings from the operating system
3. Complete the installation and click **Finish**.
4. After installation, open **VirtualBox** to verify that it was installed successfully.

---

### Step 2: Ubuntu Server Installation
To deploy Wazuh, a Linux-based operating system is required.
For this lab environment, Ubuntu Server is used due to its stability, low resource consumption, and official support.
You can download Ubuntu Server LTS from the official website:
https://ubuntu.com/download/server
<img width="1040" height="671" alt="image" src="https://github.com/user-attachments/assets/a5a6f11f-3eab-42e4-bc4c-183429005ed0" />


---

### Step 3: Additional configuration in VirtualBox
Before proceeding with the creation of the Linux virtual machine, it is recommended to apply the following changes in the VirtualBox software.
#### 1. Install additional extensions:
1. Installing VirtualBox packages
You must go to the following link and download the VirtualBox package:
https://www.virtualbox.org/wiki/Downloads
<p>
<img width="938" height="581" alt="image" src="https://github.com/user-attachments/assets/e1525ede-b62d-41f0-b85d-07f59d4ccfb5" />
</p>
3. On your PC
1. Open VirtualBox.
2. Go to File → Tools → Extension Pack Manager (in some versions: File → Preferences → Extensions).
<p>
<img width="605" height="439" alt="image" src="https://github.com/user-attachments/assets/263ae5c2-eb5a-4084-b8a7-28770a6e0d1b" />
</p>
3. Clic Install
<p>
<img width="475" height="346" alt="image" src="https://github.com/user-attachments/assets/6dd72cfd-9094-47d4-8dc9-16175ce78512" />
</p>
4. Select the previously downloaded package and load it.
<p>
<img width="1060" height="653" alt="image" src="https://github.com/user-attachments/assets/0852ed3f-7495-4b7d-8273-32b21934dde2" />
</p>
5. Then, click on Install.
<p>
<img width="432" height="283" alt="image" src="https://github.com/user-attachments/assets/dcea53d7-1335-4084-b2d7-81412572161f" />
</p>

#### 2. VirtualBox Network Configuration:

Click on File → Tools → Network:
You muct be clic
#### 1. Install additional extensions:
1. Installing VirtualBox packages
You must go to the following link and download the VirtualBox package:
<p>
<img width="446" height="339" alt="image" src="https://github.com/user-attachments/assets/0c47e825-6322-4cf5-ae69-46f9d31eca60" />
</p>

2. Then, right-click and select Properties.
3. In the Adapter tab, change the IP address and set it to 192.168.100.1. This change is made in order to maintain a more structured and consistent network scheme and to avoid configuration mistakes in the network setup.

<p>
    <img width="1796" height="272" alt="image" src="https://github.com/user-attachments/assets/f5cb0082-4e15-4e34-babd-ebb67fe7c110" />
</p>

4. Next, select the DHCP Server tab.

5. In the Server Address field, set the IP address to 192.168.100.100 and leave the Server Mask unchanged. Then, set 192.168.100.101 as the Lower Address Bound and 192.168.100.254 as the Upper Address Bound.
This configuration means that the DHCP server will assign IP addresses in the range from 192.168.100.101 to 192.168.100.254.

<p>
    <img width="1796" height="233" alt="image" src="https://github.com/user-attachments/assets/70aa7729-cda5-4d03-bd0d-322f8ef788e9" />
</p>

6. Then, click Apply to save the changes.






