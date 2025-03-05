## ✅ **What is it?**

Remote Desktop Protocol (**RDP**) allows users to **remotely connect to Windows machines**. Windows **stores forensic artifacts** related to RDP connections, including:

- **IP addresses of previously connected remote systems.**
- **Connection timestamps and authentication attempts.**
- **Cached screen images of remote sessions.**
- **Clipboard and file transfer history (copy-pasted content).**

Forensically, **RDP artifacts are valuable** because:

- They help track **unauthorized remote access** attempts.
- They reveal **which systems a user connected to**.
- Cached images may **contain sensitive data from the remote session**.

> **⚠️ Limitations:**
> 
> - If **RDP caching is disabled**, some artifacts may not be available.
> - Cached session images are **overwritten over time**.
> - **Network-level authentication (NLA)** may prevent full user details from being stored.

---

## **📍 Where to Find RDP Artifacts?**

Windows stores RDP artifacts in multiple locations:

### **1️⃣ RDP Connection History (Registry)**

|**Artifact**|**Registry Path**|**Purpose**|
|---|---|---|
|Recent RDP Connections|`HKCU\Software\Microsoft\Terminal Server Client\Default`|Stores last-used IPs/hostnames.|
|MRU (Most Recently Used) Servers|`HKCU\Software\Microsoft\Terminal Server Client\Servers`|Contains connection history per host.|
|Credentials Used (Encrypted)|`HKCU\Software\Microsoft\Terminal Server Client\UsernameHint`|Stores last-used usernames for RDP.|

### **2️⃣ RDP Log Files (Event Logs)**

|**Log Name**|**Location**|**Purpose**|
|---|---|---|
|RDP Connection Events|`Microsoft-Windows-TerminalServices-LocalSessionManager/Operational.evtx`|Logs session starts and terminations.|
|RDP Authentication Attempts|`Microsoft-Windows-Security-Auditing/Security.evtx`|Logs failed/successful login attempts (Event ID 4624, 4625).|

### **3️⃣ RDP Bitmap Cache (Cached Screenshots)**

|**Artifact**|**Location**|**Purpose**|
|---|---|---|
|RDP Bitmap Cache|`C:\Users\%USERNAME%\AppData\Local\Microsoft\Terminal Server Client\Cache\`|Stores images of previous RDP sessions.|

---

## **🛠️ How to Extract RDP Artifacts (Step by Step)**

We will use **RegRipper** for extracting registry artifacts, **EvtxECmd** for event logs, and **RDP Cache Viewer** for analyzing cached session images.

### **Method 1: Extracting RDP Connection History (Registry)**

1. **Open Registry Editor (`regedit`)**.
2. **Navigate to:**
    
    ```
    HKCU\Software\Microsoft\Terminal Server Client\Default
    ```
    
3. **Export RDP Connection Entries**:
    - Look for entries like `MRU0`, `MRU1`, etc.
    - These contain **previously connected RDP hostnames/IPs**.

#### **Automated Extraction with RegRipper**

Save the **NTUSER.DAT** registry hive:

```cmd
reg save HKCU\Software\Microsoft\Terminal Server Client C:\Temp\RDP_History.hive
```

Then run RegRipper:

```cmd
rip.exe -r C:\Temp\RDP_History.hive -p rdp
```

- This extracts **all RDP connection history**.

---

### **Method 2: Extracting RDP Logins (Event Logs)**

#### **1️⃣ Open Event Viewer**

- Navigate to:
    
    ```
    Applications and Services Logs > Microsoft > Windows > TerminalServices-LocalSessionManager > Operational
    ```
    
- Look for **Event ID 21** (Successful RDP Login).

#### **2️⃣ Export RDP Event Logs**

Save the logs for offline analysis:

```cmd
wevtutil epl Microsoft-Windows-TerminalServices-LocalSessionManager/Operational C:\Temp\RDP_Events.evtx
```

#### **3️⃣ Parse Logs with EvtxECmd**

Run:

```cmd
EvtxECmd.exe -f C:\Temp\RDP_Events.evtx -o C:\ExtractedResults
```

- This extracts **timestamps, usernames, and remote IPs**.

---

### **Method 3: Extracting RDP Bitmap Cache (Session Screenshots)**

#### **1️⃣ Locate the Cache Directory**

Navigate to:

```
C:\Users\%USERNAME%\AppData\Local\Microsoft\Terminal Server Client\Cache\
```

#### **2️⃣ Open Cached Images with RDP Cache Viewer**

- Download **[RDP Cache Viewer](https://github.com/DFIRKuiper/RDP-Cache-Viewer)**.
- Extract the tool and run:
    
    ```cmd
    rdp_cache_viewer.exe -i C:\Users\%USERNAME%\AppData\Local\Microsoft\Terminal Server Client\Cache\
    ```
    
- This will reconstruct **screenshots of past RDP sessions**.

---

## **📊 How to Analyze RDP Artifacts (Step by Step)**

|**Step**|**Action**|**Details**|
|---|---|---|
|**1. Extract RDP Connection History**|Use `RegRipper` on NTUSER.DAT|Shows previous RDP hostnames/IPs.|
|**2. Analyze Login Events**|Check Event ID 21, 4624, 4625|Identifies who logged in remotely.|
|**3. Review Bitmap Cache**|Use `RDP Cache Viewer`|Recovers images from past RDP sessions.|
|**4. Identify Failed Logins**|Check Security Log for Event ID 4625|Detects brute-force attempts.|
|**5. Correlate with Other Artifacts**|Compare with Prefetch, Shellbags, and Network Logs|Verifies unauthorized access attempts.|

---

## **🚨 Real-World Use Cases**

### **📌 Incident Response**

- Identify **unauthorized RDP access attempts**.
- Detect **brute-force login attempts** on RDP.

### **📌 Malware Analysis**

- Check if malware **established RDP-based persistence**.
- Track **connections to command-and-control (C2) servers** via RDP.

### **📌 Insider Threat Investigations**

- Verify if an **employee accessed a remote system without authorization**.
- Analyze **cached RDP images for leaked confidential data**.

---

## **🔎 Summary**

|**Category**|**Details**|
|---|---|
|**Location**|`Registry, Event Logs, Bitmap Cache`|
|**File Type**|`.evtx`, `.dat`, `.bin`|
|**Extraction Tool**|`RegRipper`, `EvtxECmd`, `RDP Cache Viewer`|
|**Key Information**|Previous RDP hosts, login attempts, cached session screenshots|
|**Forensic Value**|Tracks remote access, unauthorized logins, and session activity|

---
