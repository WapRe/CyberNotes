## ✅ **What is it?**

The **USN Journal ($J)** is a hidden **NTFS system file** that records **all changes to files and directories** on a disk. It logs:

- **File creation, modification, deletion, and renaming**.
- **Metadata changes** (permissions, timestamps, attributes).
- **Volume-level changes** (formatting, disk management).

Forensically, **the USN Journal is one of the most detailed sources for tracking file activity** because:

- It provides **historical records of file operations**.
- It helps **recover details of deleted files**, even if the MFT is overwritten.
- It **tracks malware execution**, especially when attackers delete files to cover their tracks.

> **⚠️ Limitations:**
> 
> - Exists **only on NTFS partitions**.
> - **Old records are overwritten** as the journal grows.
> - If **USN journaling is disabled**, no data is available.

---

## **📍 Where to Find It?**

The USN Journal is stored in a hidden system file:

```
C:\$Extend\$UsnJrnl
```

It consists of:

- **$J** – The actual journal file containing change records.
- **$Max** – The configuration file controlling the journal size.

---

## **🛠️ How to Extract It (Step by Step)**

We will use **MFTECmd**, a forensic tool for parsing USN Journal data.

### **Method 1: Manual Extraction**

1. **Open Command Prompt as Administrator**.
    
2. **Check if USN Journaling is Enabled**:
    
    ```cmd
    fsutil usn queryjournal C:
    ```
    
    - If enabled, it will display:
        
        ```
        Usn Journal ID = 0xXXXXXXXXXXXXXXXX
        First Usn      = 0xXXXXXXXXXXXXXXXX
        Next Usn       = 0xXXXXXXXXXXXXXXXX
        ```
        
    - If disabled, journaling needs to be re-enabled to collect future data.
3. **Copy the USN Journal File**:
    
    ```cmd
    copy \\.\C:\$Extend\$UsnJrnl C:\Temp\UsnJrnl.dat
    ```
    

---

### **Method 2: Automated Extraction with MFTECmd**

#### **1️⃣ Download MFTECmd**

- Get it from **[Eric Zimmerman's GitHub](https://ericzimmerman.github.io/)**.
- Extract it to a working directory.

#### **2️⃣ Run MFTECmd on the USN Journal**

Navigate to the tool’s folder and run:

```cmd
MFTECmd.exe -f C:\Temp\UsnJrnl.dat -o C:\ExtractedResults
```

- `-f` specifies the input USN Journal file.
- `-o` defines the output folder for parsed data.

#### **3️⃣ Review Extracted Data**

- Open the **CSV files** in **Excel** or a forensic text editor.
- Look for:
    - **File creation, modification, deletion events**.
    - **Timestamps of file operations**.
    - **Executable files being written or deleted** (possible malware traces).

---

## **📊 How to Analyze It (Step by Step)**

|**Step**|**Action**|**Details**|
|---|---|---|
|**1. Open the Extracted CSV File**|Use Excel for filtering|Displays file system changes.|
|**2. Identify Created Files**|Look for `FILE_CREATE` events|Shows when new files appeared on disk.|
|**3. Track File Modifications**|Check `FILE_MODIFY` records|Helps detect unauthorized changes.|
|**4. Investigate Deleted Files**|Look for `FILE_DELETE` events|Reveals if important files were removed.|
|**5. Review Renamed Files**|Look at `FILE_RENAME` entries|Attackers may rename files to hide activity.|
|**6. Correlate with Other Artifacts**|Compare with Prefetch, Event Logs, and MFT|Helps reconstruct a complete attack timeline.|

---

## **🚨 Real-World Use Cases**

### **📌 Incident Response**

- Identify **which files were created or deleted during an attack**.
- Detect **attempts to wipe forensic evidence** (deletion logs).

### **📌 Malware Analysis**

- Track **when malware was written to disk and later deleted**.
- Detect **self-deleting payloads** that remove themselves after execution.

### **📌 Insider Threat Investigations**

- Investigate **sensitive file access and deletion**.
- Confirm if **data exfiltration tools were installed and later removed**.

---

## **🔎 Summary**

|**Category**|**Details**|
|---|---|
|**Location**|`C:\$Extend\$UsnJrnl`|
|**File Type**|NTFS System File|
|**Extraction Tool**|`MFTECmd`|
|**Key Information**|File system changes, creation/modification timestamps, deleted file records|
|**Forensic Value**|Tracks file modifications, malware activity, and deleted files|

---
