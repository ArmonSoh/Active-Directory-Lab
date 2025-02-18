# Atomic Red Team - Active Directory Lab

## Introduction
**Atomic Red Team (ART)** is an **adversary simulation framework** that allows us to **test detection capabilities** in Splunk by generating real-world attack telemetry.

In this section, we will:
- Install and configure **Atomic Red Team**.
- Run tests that simulate real-world **MITRE ATT&CK** techniques.
- Verify log generation in **Splunk**.

---

## Installing Atomic Red Team

### **Step 1: Disable Windows Defender Exclusions**
Since ART simulates attack behaviors, **Windows Defender may flag and block** certain actions. We will **exclude the C:\ drive** to prevent interference.

1. Open **Windows Security**.
2. Click on **Virus & threat protection** → **Manage settings**.
3. Scroll down to **Exclusions** and select **Add or remove exclusions**.
4. Click **Add an exclusion → Folder**, then select **C:\**.
5. Click **OK** to confirm.



---

### **Step 2: Change Execution Policy in PowerShell**
PowerShell **restricts execution of certain scripts** by default. We need to **bypass these restrictions**.

1. Open **PowerShell as Administrator**.
2. Run the following command:

    ```powershell
    Set-ExecutionPolicy Bypass -Scope CurrentUser
    ```

3. When prompted, type **Y** and press **Enter**.

---

### **Step 3: Install Atomic Red Team**
Now, let’s install ART using the PowerShell script.

1. Run the following command:

    ```powershell
    IEX (New-Object System.Net.WebClient).DownloadString('https://raw.githubusercontent.com/redcanaryco/invoke-atomicredteam/master/install-atomicredteam.ps1')
    ```

2. Press **Y** when prompted to install dependencies.
3. Once completed, navigate to **C:\AtomicRedTeam**.
4. Open the **Atomics** folder—this contains all the **MITRE ATT&CK technique scripts**.

---

##  Running Atomic Red Team Tests

### **Step 1: Selecting a Test**
Each test is mapped to a **MITRE ATT&CK Technique ID**. We will simulate the **Creation of a Local Account (T1136.001)**.

1. Open PowerShell **as Administrator**.
2. Run the following command:

    ```powershell
    Invoke-AtomicTest T1136.001
    ```

3. If executed successfully, **a new local account will be created**.


---

##  Verifying Results in Splunk

After executing the attack, we can query **Splunk** to analyze the event logs.

### **Step 1: Search for Local Account Creation**
- Open **Splunk Search & Reporting**.
- Run the following query:

    ```splunk
    index=endpoint New-LocalUser
    ```

✔️ **Expected Result:** If logs are captured correctly, we should see **a newly created local user account**.


---

##  Mitigation Strategies

 
### **Enable Logging & SIEM Integration**

- Ensure PowerShell logging is enabled:
    - Computer Configuration → Administrative Templates → Windows Components → PowerShell → Enable Logging

- Integrate logs into Splunk or another SIEM for real-time monitoring.

###  **Implement Least Privilege & Group Policies**
- Restrict the ability for standard users to create new local accounts.
- Apply Application Control to limit execution of unauthorized scripts.
### **Monitor for Suspicious Events**
- Create SIEM alerts to flag suspicious events, such as:
    - Multiple account creations within a short time.
    - Unusual PowerShell execution.
    - High number of failed logins before a successful one.
