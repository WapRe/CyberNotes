## ✅ **What is it?**

Windows Defender is **Microsoft’s built-in antivirus and endpoint protection system**. It logs **threat detections, scans, and security-related events** that can provide forensic insights into:

- **Malware infections and remediation actions**.
- **Unauthorized file modifications or deletions**.
- **Real-time protection events (blocked executions, quarantined files, suspicious activity detections)**.
- **Tampering attempts (when an attacker tries to disable Defender)**.

Forensically, **Windows Defender logs are useful** because:

- They provide **detection timestamps** that correlate with an attack timeline.
- They help **identify deleted/quarantined malware**.
- They reveal **attempts to disable security settings**.

> **⚠️ Limitations:**
> 
> - Logs **may be cleared** by an attacker.
> - If another **third-party AV** is installed, Defender may be disabled.
> - Some **detections may be false positives**.

---

## **📍 Where to Find It?**

Windows Defender logs are stored in multiple locations:

|**Location**|**Purpose**|
|---|---|
|`C:\ProgramData\Microsoft\Windows Defender\Support\MPLog-*.log`|Main log files for Defender activity.|
|`C:\ProgramData\Microsoft\Windows Defender\Scans\History\Service\DetectionHistory`|Stores threat detection history.|
|`C:\Windows\System32\winevt\Logs\Microsoft-Windows-Windows Defender%4Operational.evtx`|Event logs for real-time detections.|

---

## **🛠️ How to Extract It (Step by Step)**

We will use **Event Viewer** for real-time detections and **MPLogParser** for historical logs.

### **Method 1: Extracting Defender Event Logs**

1. **Open Event Viewer (`eventvwr.msc`)**.
    
2. **Navigate to**:
    
    ```
    Applications and Services Logs > Microsoft > Windows > Windows Defender > Operational
    ```
    
3. **Look for Key Events**:
    
    - **Event ID 1006** → Malware detected.
    - **Event ID 1116** → Malware quarantined.
    - **Event ID 5007** → Defender settings changed (possible tampering).
    - **Event ID 5010** → Real-time protection disabled.
4. **Export the logs**:
    
    - Click **Save All Events As...** and save the file for analysis.

---

### **Method 2: Parsing Defender Logs with MPLogParser**

#### **1️⃣ Download MPLogParser**

- Get it from **[Microsoft Security Tools](https://github.com/microsoft/MDETools)**.
- Extract to a working directory.

#### **2️⃣ Run MPLogParser on Defender Logs**

Navigate to the tool’s folder and run:

```cmd
MPLogParser.exe -i "C:\ProgramData\Microsoft\Windows Defender\Support\MPLog-*.log" -o C:\ExtractedResults
```

- This extracts **detection events, scan results, and remediation actions**.

#### **3️⃣ Review Extracted Data**

- Open the `.csv` output in **Excel**.
- Look for:
    - **Detected threats and their file paths**.
    - **Actions taken (quarantined, removed, ignored)**.
    - **Timestamps of detections**.

---

## **📊 How to Analyze It (Step by Step)**

|**Step**|**Action**|**Details**|
|---|---|---|
|**1. Open Extracted Logs**|Load the `.csv` or `.evtx` output|Displays malware detections and actions.|
|**2. Identify Detected Threats**|Check `ThreatName` and `FilePath` columns|Reveals what malware was found.|
|**3. Review Defender Actions**|Look at `ActionTaken` field|Shows if malware was removed or ignored.|
|**4. Check for Tampering Attempts**|Look for `Event ID 5007`|Indicates if Defender settings were changed.|
|**5. Investigate Disabled Protection**|Look for `Event ID 5010`|Reveals if real-time protection was turned off.|
|**6. Correlate with Other Artifacts**|Compare with Prefetch, MFT, and Event Logs|Helps confirm malware execution.|

---

## **🚨 Real-World Use Cases**

### **📌 Incident Response**

- Determine **when and where malware was detected**.
- Identify **if an attacker disabled security settings** before launching an attack.

### **📌 Malware Analysis**

- Track **how malware was executed and whether it was quarantined**.
- Investigate **files flagged as suspicious but not removed**.

### **📌 Insider Threat Investigations**

- Detect **if an employee ignored Defender warnings** and ran flagged executables.
- Check **if security software was tampered with** before unauthorized activities.

---

## **🔎 Summary**

|**Category**|**Details**|
|---|---|
|**Location**|`C:\ProgramData\Microsoft\Windows Defender\`, `C:\Windows\System32\winevt\Logs\Microsoft-Windows-Windows Defender%4Operational.evtx`|
|**File Type**|`.log`, `.evtx`|
|**Extraction Tool**|`MPLogParser`, `Event Viewer`|
|**Key Information**|Detected malware, security settings changes, remediation actions|
|**Forensic Value**|Tracks security alerts, malware execution, and Defender tampering|

---
