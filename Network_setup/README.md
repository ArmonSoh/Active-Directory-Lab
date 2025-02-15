# Network Setup

This section documents the network configuration required for the Active Directory Lab environment. The configurations ensure proper communication between virtual machines, enable Remote Desktop access, and set up static IP addresses for key services.

## Enabling Remote Desktop for Users
To allow users to connect remotely to specific machines in the domain, Remote Desktop must be enabled and configured with appropriate permissions.

### Steps:
1. Open **System Properties** (`sysdm.cpl`).
2. Navigate to the **Remote** tab.
3. Enable **Allow remote connections to this computer**.
4. Configure **Remote Desktop Users** to specify which accounts can connect.

**Screenshot:**
![Enable Remote Desktop](Enable_Remote_Desktop_Users.jpg)

---

## Configuring a Static IP for Splunk
Splunk requires a static IP to ensure log forwarding and monitoring stability. This setup assigns a fixed IP address to the Splunk server.

### Steps:
1. Open **Control Panel > Network and Internet > Network and Sharing Center**.
2. Click **Change adapter settings**.
3. Right-click the active network adapter and select **Properties**.
4. Select **Internet Protocol Version 4 (TCP/IPv4)** and click **Properties**.
5. Choose **Use the following IP address** and enter:
   - **IP Address**: `192.168.10.50`
   - **Subnet Mask**: `255.255.255.0`
   - **Default Gateway**: `192.168.10.1`
6. Click **OK** and restart the network adapter.

**Screenshot:**
![Splunk Static IP Config](Splunk_Static_IP_Config.jpg)

---

### **Windows 10 Network Configuration**
The Windows 10 machine in the environment needs proper DNS settings to allow domain communication.

### **Steps:**
1. Open **Network and Sharing Center**.
2. Click on **Ethernet** (or Wi-Fi if applicable).
3. Select **Properties** and open **Internet Protocol Version 4 (TCP/IPv4)**.
4. Configure the following IP settings:
   - **IP Address:** `192.168.10.100`
   - **Subnet Mask:** `255.255.255.0`
   - **Default Gateway:** `192.168.10.1`
5. Configure the DNS settings:
   - **Preferred DNS Server:** `8.8.8.8` (Google Public DNS)
   - **Alternate DNS Server:** *(Leave blank, as seen in the screenshot)*
6. Click **OK** and **Apply** the settings, then restart the network connection.

**Screenshot:**
![Windows 10 Network Config](ip_setup_windows10_target.jpg)

---

### Summary
- Remote Desktop is enabled to allow administrative access.
- A static IP is assigned to the Splunk server for consistent log forwarding.
- The Windows 10 workstation is configured with proper DNS settings for domain resolution.

These configurations ensure smooth operation of the Active Directory Lab environment.

