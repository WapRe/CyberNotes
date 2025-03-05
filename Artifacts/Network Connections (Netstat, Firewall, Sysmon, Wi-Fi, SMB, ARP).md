## ✅ **What is it?**

Windows records **network activity and device interactions**, tracking:

- **Active and past TCP/UDP connections** (`netstat`, firewall logs).
- **Inbound/outbound blocked connections** (`pfirewall.log`, Event ID 5157).
- **Process-based network connections** (`Sysmon Event ID 3`).
- **Wi-Fi networks the device has connected to** (`WLAN profiles`).
- **Past devices seen on the local network** (`arp -a`).
- **Remote SMB/Network Shares accessed** (lateral movement detection).

Forensically, **these artifacts are essential** for:

- Identifying **exfiltration channels** (malware, insider threats).
- Tracking **unauthorized RDP, VPN, or SMB access**.
- Correlating **network activity with process execution**.

> **⚠️ Limitations:**
> 
> - **Most data is volatile**, meaning it's lost upon reboot.
> - **If logging is disabled**, some artifacts may be missing.
> - **Encrypted traffic (VPN, HTTPS, Tor)** makes deeper inspection difficult.

---

## **📍 Where to Find Network Artifacts?**

### **1️⃣ Active Network Connections**

|**Command**|**Purpose**|
|---|---|
|`netstat -ano`|Shows active network connections (IP, PID, state).|
|`arp -a`|Displays MAC addresses of past network devices.|

### **2️⃣ Network Logs (Persistent Data)**

|**Log Name**|**Location**|**Purpose**|
|---|---|---|
|Windows Firewall Log|`C:\Windows\System32\LogFiles\Firewall\pfirewall.log`|Logs allowed/blocked traffic.|
|Security Event Log|`Microsoft-Windows-Security-Auditing/Security.evtx`|Tracks inbound/outbound network events.|
|Sysmon Log (Event ID 3)|`Microsoft-Windows-Sysmon/Operational.evtx`|Records process-based network connections.|

### **3️⃣ Wi-Fi & Adapter History**

|**Artifact**|**Location**|**Purpose**|
|---|---|---|
|Wi-Fi Connection History|`C:\ProgramData\Microsoft\Wlansvc\Profiles\Interfaces\`|Stores past Wi-Fi SSIDs.|
|SMB & Remote Access Logs|`Microsoft-Windows-SMBClient/Operational.evtx`|Detects access to shared network folders.|

---

## **🛠️ How to Extract Network Artifacts (Step by Step)**

We will use **command-line tools**, **Event Viewer**, and **Sysmon logs**.

### **Method 1: Extracting Active Network Connections**

1. **List Current Network Connections**
    
    ```cmd
    netstat -ano > C:\Temp\netstat_connections.txt
    ```
    
    - Captures:
        - **Remote IPs**.
        - **Process IDs (PIDs) using connections**.
        - **Connection states (LISTENING, ESTABLISHED, etc.).**
2. **List Past Connected Devices (ARP Table)**
    
    ```cmd
    arp -a > C:\Temp\arp_cache.txt
    ```
    
    - Provides **past device MAC addresses** on the network.

---

### **Method 2: Extracting Network Logs (Firewall, Security Events)**

#### **1️⃣ Open Windows Firewall Log**

- Navigate to:
    
    ```
    C:\Windows\System32\LogFiles\Firewall\pfirewall.log
    ```
    
- Open and search for **blocked or allowed connections**.

#### **2️⃣ Extract Network Event Logs**

Save Security Event Logs for forensic analysis:

```cmd
wevtutil epl Microsoft-Windows-Security-Auditing/Security C:\Temp\NetworkSecurity.evtx
```

#### **3️⃣ Parse Logs with EvtxECmd**

Run:

```cmd
EvtxECmd.exe -f C:\Temp\NetworkSecurity.evtx -o C:\ExtractedResults
```

- Look for:
    - **Event ID 5156** → Allowed network connections.
    - **Event ID 5157** → Blocked network connections.

---

### **Method 3: Extracting Sysmon Network Logs**

#### **1️⃣ Open Event Viewer**

- Navigate to:
    
    ```
    Applications and Services Logs > Microsoft > Windows > Sysmon > Operational
    ```
    
- Look for:
    - **Event ID 3** → Logs network connections per process.

#### **2️⃣ Export Sysmon Logs**

```cmd
wevtutil epl Microsoft-Windows-Sysmon/Operational C:\Temp\SysmonLogs.evtx
```

#### **3️⃣ Parse Logs with EvtxECmd**

Run:

```cmd
EvtxECmd.exe -f C:\Temp\SysmonLogs.evtx -o C:\ExtractedResults
```

- This maps **which process initiated network connections**.

---

### **Method 4: Extracting Wi-Fi & SMB History**

#### **1️⃣ Extract Wi-Fi Profiles**

```cmd
netsh wlan show profiles > C:\Temp\wifi_profiles.txt
```

- This lists **all Wi-Fi networks the machine has connected to**.

#### **2️⃣ Extract SMB Remote Access Logs**

- Open Event Viewer and navigate to:
    
    ```
    Applications and Services Logs > Microsoft > Windows > SMBClient > Operational
    ```
    
- Look for:
    - **Event ID 1020** → Connection to a shared folder.
    - **Event ID 1058** → Access denied to a network share.

---

## **📊 How to Analyze Network Artifacts (Step by Step)**

|**Step**|**Action**|**Details**|
|---|---|---|
|**1. Extract Active Network Connections**|Use `netstat -ano`|Displays real-time connections and PIDs.|
|**2. Investigate ARP Cache**|Use `arp -a`|Identifies past network devices.|
|**3. Review Firewall Logs**|Check `pfirewall.log`|Shows blocked/allowed traffic.|
|**4. Analyze Sysmon Logs**|Look at `Event ID 3`|Maps process-level network activity.|
|**5. Investigate Wi-Fi History**|Examine WLAN profile files|Tracks past Wi-Fi connections.|
|**6. Analyze SMB/Network Share Logs**|Look at `Event ID 1020`|Detects unauthorized lateral movement.|

---

## **🚨 Real-World Use Cases**

### **📌 Incident Response**

- Detect **malware communicating with C2 servers**.
- Identify **unauthorized RDP, VPN, or SMB access**.

### **📌 Malware Analysis**

- Track **malware exfiltrating data** via HTTP, FTP, or SMB.
- Identify **malware persistence mechanisms via network connections**.

### **📌 Insider Threat Investigations**

- Check if **an employee accessed restricted network shares**.
- Verify **Wi-Fi connections to unauthorized networks**.

---

## **🔎 Summary**

|**Category**|**Details**|
|---|---|
|**Location**|`Netstat, Firewall Logs, Sysmon, ARP, Wi-Fi History, SMB Logs`|
|**File Type**|`.evtx`, `.log`, `.txt`|
|**Extraction Tool**|`Netstat`, `EvtxECmd`, `Sysmon`, `wevtutil`, `netsh`|
|**Key Information**|Open connections, firewall activity, Wi-Fi history, SMB access|
|**Forensic Value**|Tracks past and present network activity, detects malware C2 traffic|

---
