## ✅ **What is it?**

SRUM (System Resource Usage Monitor) is a **Windows database that logs application and network activity over the past 30 days**. It tracks:

- **Which applications were running and when**.
- **Network usage per app** (sent/received bytes).
- **Power consumption of applications** (useful for detecting stealthy malware).
- **User sessions** and **logon details**.

Forensically, **SRUM is invaluable** because:

- It provides a **historical view of system activity**, even if logs were deleted.
- It can help **track exfiltration of data** based on network usage.
- It is difficult to disable without administrator privileges.

> **⚠️ Limitations:**
> 
> - SRUM only retains **30 days of data**.
> - Some network connections **may not be recorded** if SRUM was disabled or corrupted.

- - Data is stored in an **ESE (Extensible Storage Engine) database**, requiring specialized tools to parse.

---

## **📍 Where to Find It?**

SRUM data is stored in an **ESE database file**:

```
C:\Windows\System32\sru\SRUDB.dat
```

This file logs data across multiple tables related to **app usage, network connections, and energy consumption**.

---

## **🛠️ How to Extract It (Step by Step)**

We will use **srumecmd**, a forensic tool for extracting SRUM data.

### **Method 1: Manual Collection**

1. **Copy the SRUM Database**
    
    - Open **Command Prompt as Administrator**.
    - Copy the database to a working location:
        
        ```cmd
        copy C:\Windows\System32\sru\SRUDB.dat C:\Temp\SRUDB.dat
        ```
        
2. **Convert the Database**
    
    - Since SRUM uses an **ESE database format**, you’ll need a **database viewer** (like ESEDatabaseView) to open it manually.

---

### **Method 2: Automated Extraction with srumecmd**

#### **1️⃣ Download srumecmd**

- Get it from **[Eric Zimmerman's GitHub](https://ericzimmerman.github.io/)**.
- Extract to a working directory.

#### **2️⃣ Run srumecmd on the SRUM Database**

Navigate to the tool’s folder and run:

```cmd
srumecmd.exe -d C:\Temp\SRUDB.dat -o C:\ExtractedResults
```

- `-d` specifies the input SRUM database file.
- `-o` defines the output folder for extracted CSV files.

#### **3️⃣ Review Extracted Data**

- Open the CSV files in **Excel**.
- Look for:
    - **Application Names** (which programs were running).
    - **Sent/Received Bytes** (potential data exfiltration).
    - **Execution Timestamps** (when an app was active).

---

## **📊 How to Analyze It (Step by Step)**

|**Step**|**Action**|**Details**|
|---|---|---|
|**1. Open the Extracted CSV Files**|Use Excel for filtering|Displays app and network activity.|
|**2. Identify Running Applications**|Look at the `Application Name` column|Shows what was running during an attack.|
|**3. Review Network Usage**|Check `Bytes Sent` and `Bytes Received`|Helps detect data exfiltration.|
|**4. Analyze User Logons**|Look at `User SID` and `Session Start Time`|Determines when a user was active.|
|**5. Correlate with Other Artifacts**|Compare with Prefetch, Event Logs, and Amcache|Provides deeper insights into system activity.|

---

## **🚨 Real-World Use Cases**

### **📌 Incident Response**

- Detect **which applications were running before/during an attack**.
- Identify **malware that used network connections**.

### **📌 Malware Analysis**

- Track **data exfiltration attempts** based on high network activity.
- Detect **persistent malware that re-executes periodically**.

### **📌 Insider Threat Investigations**

- Identify **unauthorized software usage**.
- Investigate **large data transfers from the system**.

---

## **🔎 Summary**

|**Category**|**Details**|
|---|---|
|**Location**|`C:\Windows\System32\sru\SRUDB.dat`|
|**File Type**|ESE Database|
|**Extraction Tool**|`srumecmd`|
|**Key Information**|Running applications, network usage, user sessions|
|**Forensic Value**|Tracks software execution, network activity, and user behavior|

---
