# Active Directory - Splunk & Sysmon Setup

## Configuring Windows Target Machine

### Renaming the Target Machine
1. Open **Settings** and navigate to **System > About**.
2. Click **Rename this PC** and enter `Target-PC`.
3. Click **Next** and restart the computer.
4. After reboot, verify the change by searching for **PC Info**.

### Setting a Static IP
1. Open **Control Panel > Network and Sharing Center**.
2. Click on **Change adapter settings**.
3. Right-click the active network adapter and select **Properties**.
4. Select **Internet Protocol Version 4 (TCP/IPv4)** and click **Properties**.
5. Set the following details:
   - **IP Address:** `192.168.1.100`
   - **Subnet Mask:** `255.255.255.0`
   - **Default Gateway:** `192.168.1.1`
   - **Preferred DNS Server:** `8.8.8.8`
6. Click **OK** and restart the network adapter.

### Verifying Connectivity
1. Open **Command Prompt** and type:
   ```sh
   ipconfig
   ```
2. Ensure the correct IP is set (`192.168.1.100`).
3. Test connectivity to the Splunk server:
   ```sh
   ping 192.168.10.10
   ```
4. Open a web browser and navigate to:
   ```
   http://192.168.10.10:8000
   ```
   Ensure the Splunk login page appears.

---

## Installing Splunk Universal Forwarder
1. Download **Splunk Universal Forwarder** from [Splunk's website](https://www.splunk.com).
2. Select **Windows (64-bit)** and install using the `.msi` file.
3. Follow the installation wizard:
   - **Accept License Agreement**.
   - **Select "On-premise Splunk Enterprise instance"**.
   - **Username:** `admin`
   - **Generate random password** (optional).
   - **Receiving Indexer:** `192.168.10.10`
   - **Port:** `9997`
   - **Skip Deployment Server**.
4. Complete the installation and verify the service is running.

---

## Installing Sysmon
1. Download **Sysmon** from [Microsoft Sysinternals](https://docs.microsoft.com/en-us/sysinternals/downloads/sysmon).
2. Extract `Sysmon.zip` to a known location.
3. Download the **Sysmon configuration file** from Olaf's GitHub repository.
4. Open **PowerShell as Administrator**.
5. Change directory to the extracted Sysmon location:
   ```sh
   cd C:\Path\To\Sysmon
   ```
6. Install Sysmon with the config file:
   ```sh
   .\sysmon64.exe -i C:\Path\To\sysmonconfig.xml
   ```
7. Accept the agreement and verify installation:
   ```sh
   Get-Service Sysmon
   ```

---

## Configuring Splunk Forwarder (`inputs.conf`)
1. Open **Notepad as Administrator**.
2. Create a new file under:
   ```
   C:\Program Files\SplunkUniversalForwarder\etc\system\local\inputs.conf
   ```
3. Add the following:
   ```ini
   [default]
   host = Target-PC

   [monitor://C:\Windows\System32\winevt\Logs\Security.evtx]
   disabled = 0
   index = endpoint
   sourcetype = WinEventLog:Security

   [monitor://C:\Windows\System32\winevt\Logs\System.evtx]
   disabled = 0
   index = endpoint
   sourcetype = WinEventLog:System

   [monitor://C:\Windows\System32\winevt\Logs\Application.evtx]
   disabled = 0
   index = endpoint
   sourcetype = WinEventLog:Application

   [monitor://C:\Program Files\Sysmon\Sysmon.log]
   disabled = 0
   index = endpoint
   sourcetype = xmlwineventlog
   ```
4. Save and close the file.
5. Restart the Splunk Forwarder service:
   ```sh
   net stop splunkforwarder
   net start splunkforwarder
   ```

---

## Configuring Splunk to Receive Data
1. Log into **Splunk Web** (`http://192.168.10.10:8000`).
2. Navigate to **Settings > Indexes**.
3. Click **New Index**, name it `endpoint`, and save.
4. Go to **Settings > Forwarding and Receiving**.
5. Click **Configure Receiving > New Receiving Port**.
6. Enter `9997` and save.

---

## Verifying Log Ingestion
1. In **Splunk Web**, go to **Apps > Search & Reporting**.
2. Run the following search query:
   ```sh
   index=endpoint
   ```
3. Verify that logs from `Target-PC` appear.
4. Check logs for **Security**, **System**, **Application**, and **Sysmon** events.

---

## Summary
- The **Target-PC** is now renamed and has a static IP.
- **Splunk Universal Forwarder** is installed and configured to send logs.
- **Sysmon** is installed for advanced telemetry.
- **Splunk is configured to receive logs** on port `9997`.
- **Logs are verified** in the `endpoint` index.

---

