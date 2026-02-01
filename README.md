# Wazuh-SIEM-Virtualbox-Installation

Step-by-step guide to deploy a Wazuh SIEM lab on VirtualBox using multiple virtual machines to simulate real-world enterprise cyberattacks and security incidents using Wazuh SIEM.

## 📑 Table of Contents

- [Step 1: Install the virtualization software](#step-1-install-the-virtualization-software)
- [Step 2: Ubuntu Server Installation](#step-2-ubuntu-server-installation)
- [Step 3: Additional configuration in VirtualBox](#step-3-additional-configuration-in-virtualbox)
- [Step 4: Creating the Ubuntu Server Virtual Machine](#step-4-creating-the-ubuntu-server-virtual-machine)
- [Step 5: Ubuntu Linux Operating System Configuration](#step-5-ubuntu-linux-operating-system-configuration)
- [Step 6: Wazuh SIEM Installation on Ubuntu Linux](#step-6-wazuh-SIEM-installation-on-ubuntu-linux)

---

### Step 1: Install the virtualization software

The first step is to download the virtualization software that will be used to deploy **Wazuh** and the rest of the virtual machines, in my case, I will use **VirtualBox**, as it is a comfortable and widely used option for lab environments.

You can download VirtualBox from the official website:  
https://www.virtualbox.org/wiki/Downloads

Once on the VirtualBox website, select the **Download** option and choose the installer that matches your operating system, in my case, I am using **Windows hosts**, so I selected the corresponding option.

![VirtualBox Download](https://github.com/user-attachments/assets/28e3305f-e992-41e4-8307-ceb92f9a4683)

After downloading VirtualBox, completed the following steps:

1. Run the downloaded installer.
2. During the installation wizard:
   - Keep the **default settings**
   - Allow the installation of **network interfaces** when prompted
   - Accept any security warnings from the operating system
3. Complete the installation and click **Finish**.
4. After installation, open **VirtualBox** to verify that it was installed successfully.

⬆️ [Back to Table of Contents](#-table-of-contents)

<br>

---


### Step 2: Download Ubuntu Server

To deploy Wazuh, a Linux-based operating system is required, for this lab environment, Ubuntu Server is used due to its stability, low resource consumption, and official support.

You can download Ubuntu Server LTS from the official website:  
https://ubuntu.com/download/server

![Ubuntu Server Download](https://github.com/user-attachments/assets/a5a6f11f-3eab-42e4-bc4c-183429005ed0)

⬆️ [Back to Table of Contents](#-table-of-contents)

<br>

---

### Step 3: Additional configuration in VirtualBox

Before proceeding with the creation of the Linux virtual machine, it is recommended to apply the following changes in the VirtualBox software.

#### 3.1 Install additional extensions

You must go to the following link and download the VirtualBox package:  
https://www.virtualbox.org/wiki/Downloads

![Extension Pack Download](https://github.com/user-attachments/assets/e1525ede-b62d-41f0-b85d-07f59d4ccfb5)

1. Open VirtualBox.
2. Go to **File → Tools → Extension Pack Manager**  
   (in some versions: **File → Preferences → Extensions**).

![Extension Manager](https://github.com/user-attachments/assets/263ae5c2-eb5a-4084-b8a7-28770a6e0d1b)

3. Click **Install**.

![Install Button](https://github.com/user-attachments/assets/6dd72cfd-9094-47d4-8dc9-16175ce78512)

4. Select the previously downloaded package and load it.

![Select Package](https://github.com/user-attachments/assets/0852ed3f-7495-4b7d-8273-32b21934dde2)

5. Then, click on **Install**.

![Confirm Install](https://github.com/user-attachments/assets/dcea53d7-1335-4084-b2d7-81412572161f)

<br>

#### 3.2 VirtualBox Network Configuration

1. Click on **File → Tools → Network**.

![Network Menu](https://github.com/user-attachments/assets/0c47e825-6322-4cf5-ae69-46f9d31eca60)

2. Then, right-click and select **Properties**.
3. In the **Adapter** tab, change the IP address and set it to `192.168.100.1`.

This change is made in order to maintain a more structured and consistent network scheme and to avoid configuration mistakes in the network setup.

![Adapter IP](https://github.com/user-attachments/assets/f5cb0082-4e15-4e34-babd-ebb67fe7c110)

4. Next, select the **DHCP Server** tab.
5. In the **Server Address** field, set the IP address to `192.168.100.100` and leave the Server Mask unchanged.
6. Set `192.168.100.101` as the Lower Address Bound and `192.168.100.254` as the Upper Address Bound.

This configuration means that the DHCP server will assign IP addresses in the range from `192.168.100.101` to `192.168.100.254`.

![DHCP Config](https://github.com/user-attachments/assets/70aa7729-cda5-4d03-bd0d-322f8ef788e9)

7. Then, click **Apply** to save the changes.

<br>

#### 3.3 Creating a NAT Network

1. At the top menu, click on the **NAT Networks** section.

![NAT Menu](https://github.com/user-attachments/assets/648876f9-6cf3-44c9-b764-e90d25316ab5)

2. Then, right-click on the page and select **Create**.
3. Select the newly created NAT Network and right-click, then click **Properties**.
4. Change the network address to `10.10.10.0/24`, enable DHCP, and optionally rename the NAT Network.

![NAT Properties](https://github.com/user-attachments/assets/44d76c37-2140-44cd-bc25-6a10971f71ac)

5. Finally, click **Apply** to save the changes.

⬆️ [Back to Table of Contents](#-table-of-contents)

<br>

---

## Step 4: Creating the Ubuntu Server Virtual Machine

1. From the Home screen in VirtualBox, click **New** to start creating a new virtual machine.
2. Give the virtual machine a name. In my case, I will call it **Wazuh**.
3. Choose where you want to store the virtual machine files.
4. Select the Ubuntu Server ISO file that you downloaded earlier.

![VM Creation](https://github.com/user-attachments/assets/cad9a3b6-8ed9-4b04-99c3-0357e9fece01)

5. Next, move on to the **Set up Unattended Guest OS Installation** section.
6.  In this case, you can fill in the requested information using the username and password. It will not be important for now, since the Ubuntu system installation and configuration will be performed manually, So, the credentials entered here will not be important in the future.
7. Then, simply select the **Install Guest Additions** option.

![Unattended Setup](https://github.com/user-attachments/assets/d696a663-6660-4e48-94a1-84f6a9f2580e)

8. Next, go to the **Specify Virtual Hardware** section.
9. For this lab, the recommended configuration is **4 CPUs, 8 GB of RAM, and 60 GB of disk space**.

![Hardware Setup](https://github.com/user-attachments/assets/2a9e26b2-3da7-4f2c-9a79-884969056e9f)

10. Next, go to the **Specify Virtual Hard Disk** section.
11. Choose how much disk space you want to allocate to the virtual machine.

![Disk Size](https://github.com/user-attachments/assets/928b7220-f420-43b6-a96b-868fa807004f)

12. Finally, click **Finish** to complete the setup.
13. After clicking Finish, the virtual machine will start automatically. Shut it down.
14. Once powered off, right-click on the Wazuh VM and select **Settings**.
15. Go to **Network**:
    - Adapter 1: **Host-only Adapter**
    - Adapter 2: **NAT Network**

![Adapter 1](https://github.com/user-attachments/assets/ec07b54e-f614-4d90-8157-f5e38f563583)

![Adapter 2](https://github.com/user-attachments/assets/9f924ffe-8e59-4fe9-b9c4-80794c27b458)

⬆️ [Back to Table of Contents](#-table-of-contents)

<br>

---

## Step 5: Ubuntu Linux Operating System Configuration

Next, power on the Wazuh virtual machine. In some cases, after shutting it down post-configuration, you may encounter an ISO boot error. This can be quickly resolved by reattaching the previously downloaded Linux ISO. Once the VM starts, click inside the screen and use the arrow keys to select “Try or Install Ubuntu Server.”
<img width="749" height="529" alt="image" src="https://github.com/user-attachments/assets/b02e6acc-e49a-4cf5-a986-78513b779875" />

Proceed with the Ubuntu Server installation, which may take several minutes. When prompted, select your preferred language and press Enter. Next, choose the keyboard layout (English is recommended) and select Done. Finally, keep the default installation type and press Done to continue.
<img width="1273" height="851" alt="image" src="https://github.com/user-attachments/assets/033f117c-f0a4-41d2-8393-04a89d314519" />

Next, in the network configuration step, leave the settings as default. As shown, the internal network is assigned IP 192.168.100.102 and the NAT network receives 10.10.10.4, confirming the network is correctly configured. Then, press Done to continue.
<img width="1269" height="851" alt="image" src="https://github.com/user-attachments/assets/6162cd29-aaa2-4410-ba23-d1284800f55a" />

In the Proxy section, leave the field empty and select Done. Ubuntu will then verify the package repository and confirm internet connectivity, which may take a few minutes. Once you see the message “This mirror location has passed the test,” press Done to continue.
<img width="1277" height="845" alt="image" src="https://github.com/user-attachments/assets/0076763d-d8b4-4243-8271-ba24f1572c6d" />

Next, in the Guided Storage Configuration section, keep the default settings and select Done. On the following screen, select Done again. When prompted to confirm the changes, choose Continue to proceed with the installation.
<img width="1214" height="542" alt="image" src="https://github.com/user-attachments/assets/a5f40449-df07-4f79-9314-98a68622801b" />

Next, in the Profile Configuration section, enter the server name, your desired username, and password. These values are your choice, but make sure to note them down, as you will use these credentials to access your virtual machine.
#### Important Note: When entering the password and if you are typing numbers, it is recommended to use the number keys located on the top row of the keyboard (the number and symbol keys), rather than the numeric keypad.
<img width="1154" height="306" alt="image" src="https://github.com/user-attachments/assets/0bf2bc57-4063-47e2-938f-1727645b9637" />

<img width="1164" height="850" alt="image" src="https://github.com/user-attachments/assets/bad16c0f-c5a8-458e-a931-b2ffc9eb33fa" />
Once completed, select Done. Then, skip the Ubuntu Pro option and press Continue to proceed.

Next, in the SSH configuration step, you may enable it if desired. In this case, enable SSH and select Done. Then, in the Featured Server Snaps section, do not select any options and press Done. The installation will begin and may take several minutes to complete.
<img width="1266" height="849" alt="image" src="https://github.com/user-attachments/assets/4cecf977-de5d-4d93-a534-bd3a8b5c63a4" />

Once the process is complete, a message will appear at the top indicating that the installation has finished. Select Reboot Now and press Enter to restart the system.
<img width="1213" height="812" alt="image" src="https://github.com/user-attachments/assets/8c3076b8-e0b3-4273-815a-5ce8b91870bb" />

During the reboot, an error message may appear. Simply press Enter to continue. The VM will restart, and the login screen will be displayed. Press Enter again and sign in using the credentials you created earlier.
<img width="1285" height="293" alt="image" src="https://github.com/user-attachments/assets/9a17a3a7-e70e-4154-8175-be17e919af7a" />

Important Note: When entering your credentials, if you use numbers, make sure to type them using the number keys located on the top row of the keyboard (number and symbol keys). This helps prevent potential login issues.
<img width="1154" height="306" alt="image" src="https://github.com/user-attachments/assets/ed2a8962-27ef-45ef-80e4-9be7296c93d5" />

⬆️ [Back to Table of Contents](#-table-of-contents)

<br>

---

## Step 6: Wazuh SIEM Installation on Ubuntu Linux
What is Wazuh and what is it used for?

**Wazuh** is an open-source **SIEM and XDR platform** used to monitor endpoints and infrastructure for security threats, compliance, and operational issues.

It collects and analyzes logs, detects suspicious activity, monitors file integrity (FIM), checks system configuration, and helps security teams respond to incidents.

Wazuh can be deployed using different architectures depending on the environment size and performance requirements:

### **All-in-One Deployment**
- All Wazuh components (**Wazuh server, indexer, and dashboard**) are installed on a **single server**.
- Best suited for **labs, testing environments, and small infrastructures**.
- Easy to deploy and manage, with minimal resource requirements.

### **Single-Node Deployment**
- Each main component (**server, indexer, dashboard**) runs on a **separate server**.
- Recommended for **medium-sized environments** that need better performance and separation of services.

### **Multi-Node Deployment**
- Uses **clusters** for the Wazuh server and indexer, with one or more dashboard instances.
- Designed for **large environments** with high event volume.
- Provides **high availability, load balancing, and fault tolerance**.

## Architecture Used in This Lab: In this lab, we are using the **All-in-One deployment architecture**.
The **Wazuh server**, **Wazuh indexer**, and **Wazuh dashboard** are installed on the **same Ubuntu Linux server, t**his approach is ideal for learning, testing, and demonstrating Wazuh features without the complexity of a distributed environment.
