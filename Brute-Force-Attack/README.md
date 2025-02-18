# Brute Force Attack - Active Directory Lab

##  Introduction
This section simulates a **brute-force attack** against an Active Directory domain using **Crowbar** from Kali Linux. The attack targets the **Remote Desktop Protocol (RDP)** service and demonstrates how brute-force activity appears in Splunk.

## Objectives
- Simulate a brute-force attack using **Crowbar**.
- Capture failed and successful login events in **Splunk**.
- Learn how to **detect and mitigate** brute-force attempts.



##  Setting Up the Attack

###  Enable Remote Desktop on Target Machine
Before running the attack, we must allow **RDP access** on our **Windows Target Machine**.

1. Open **System Properties** (`Win + R → sysdm.cpl`).
2. Go to the **Remote** tab.
3. Check **"Allow remote connections to this computer."**
4. Click **Select Users → Add**, and enter:
   - `jsmith`
   - `tsmith`
5. Click **OK → Apply**.

![Enable RDP](/Network_setup/Enable_Remote_Desktop_Users.jpg)

---

###  Configuring Crowbar in Kali Linux
1. Open a terminal in **Kali Linux** and install Crowbar:

    ```sh
    sudo apt install crowbar -y
    ```

2. Extract a small subset of passwords from the **rockyou** wordlist:

    ```sh
    head -n 20 /usr/share/wordlists/rockyou.txt > passwords.txt
    ```

3. Append the **target user’s password** to the list:

    ```sh
    echo "SuperSecurePass123!" >> passwords.txt
    ```

---

##  Executing the Attack

1. Run Crowbar to brute-force the **Terry Smith** (`tsmith`) RDP login:

    ```sh
    crowbar -b rdp -u tsmith -C passwords.txt -s 192.168.10.10/32
    ```

✔️ If successful, you will see an **RDP Success Message**.

![Brute Force Success](./Brute_Force_Success.jpg)

---

##  Analyzing the Attack in Splunk

After executing the attack, we can query **Splunk** to analyze the **failed login attempts** and **successful login event**.

###  Detecting Failed Logins (Event ID `4625`)
- Open **Splunk Search & Reporting**.
- Run the following query:

    ```splunk
    index=endpoint eventcode=4625
    ```

✔️ You should see multiple failed login attempts.

![Failed Logins](/Brute-Force-Attack/Brute_Force_Failed_Event4625.jpg)

---

###  Detecting Successful Login (Event ID `4624`)
- Run the following query:

    ```splunk
    index=endpoint eventcode=4624
    ```

✔️ A successful login from the **attacker’s IP (Kali Linux)** should appear.

![Successful Login](/Brute-Force-Attack/Brute_Force_Successful_Login_Event4624.jpg)


##  Mitigation Strategies

### **1. Implement Account Lockout Policies**
- Configure **Group Policy** to lock accounts after a certain number of failed attempts:
  Computer Configuration → Windows Settings → Security Settings → Account Policies → Account Lockout Policy
  - Set **Threshold** to `5` failed attempts.

### **2. Enable Multi-Factor Authentication (MFA)**
- Use **MFA** to require an additional authentication step beyond passwords.

### **3. Restrict RDP Access**
- Disable **RDP access** for users who don’t require it.
- Limit RDP to specific **trusted IP addresses**.

### **4. Monitor Logs in SIEM (e.g., Splunk)**
- Create alerts in **Splunk** for multiple **failed login attempts (4625)**.

### **5. Use Strong Password Policies**
- Enforce strong passwords to prevent brute-force success.
