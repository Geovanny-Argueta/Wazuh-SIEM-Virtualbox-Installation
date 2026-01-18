# Wazuh-SIEM-Virtualbox-Installation

Step-by-step guide to deploy a Wazuh SIEM lab on VirtualBox using multiple virtual machines to simulate real-world enterprise cyberattacks and security incidents using Wazuh SIEM.

## 📑 Table of Contents

- [Step 1: Install the virtualization software](#step-1-install-the-virtualization-software)
- [Step 2: Ubuntu Server Installation](#step-2-ubuntu-server-installation)
- [Step 3: Additional configuration in VirtualBox](#step-3-additional-configuration-in-virtualbox)
- [Step 4: Creating the Ubuntu Server Virtual Machine](#step-4-creating-the-ubuntu-server-virtual-machine)

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
<br>

---


### Step 2: Ubuntu Server Installation

To deploy Wazuh, a Linux-based operating system is required, for this lab environment, Ubuntu Server is used due to its stability, low resource consumption, and official support.

You can download Ubuntu Server LTS from the official website:  
https://ubuntu.com/download/server

![Ubuntu Server Download](https://github.com/user-attachments/assets/a5a6f11f-3eab-42e4-bc4c-183429005ed0)

<br>

---

### Step 3: Additional configuration in VirtualBox

Before proceeding with the creation of the Linux virtual machine, it is recommended to apply the following changes in the VirtualBox software.

### 3.1 Install additional extensions

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

---

### 3.2 VirtualBox Network Configuration

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

---

### 3.3 Creating a NAT Network

1. At the top menu, click on the **NAT Networks** section.

![NAT Menu](https://github.com/user-attachments/assets/648876f9-6cf3-44c9-b764-e90d25316ab5)

2. Then, right-click on the page and select **Create**.
3. Select the newly created NAT Network and right-click, then click **Properties**.
4. Change the network address to `10.10.10.0/24`, enable DHCP, and optionally rename the NAT Network.

![NAT Properties](https://github.com/user-attachments/assets/44d76c37-2140-44cd-bc25-6a10971f71ac)

5. Finally, click **Apply** to save the changes.

---

## Step 4: Creating the Ubuntu Server Virtual Machine

1. From the Home screen in VirtualBox, click **New** to start creating a new virtual machine.
2. Give the virtual machine a name. In my case, I will call it **Wazuh**.
3. Choose where you want to store the virtual machine files.
4. Select the Ubuntu Server ISO file that you downloaded earlier.

![VM Creation](https://github.com/user-attachments/assets/cad9a3b6-8ed9-4b04-99c3-0357e9fece01)

5. Next, move on to the **Set up Unattended Guest OS Installation** section.
6. Enter a username and password.
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















