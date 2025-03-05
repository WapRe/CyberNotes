## ✅ **What is it?**

The **Master File Table (MFT)** is a core component of the **NTFS file system** that keeps track of **all files and directories** on a disk. Every file and folder has an **entry in the MFT**, which stores:

- **File name and path**.
- **Timestamps (Created, Modified, Accessed, MFT Entry Modified)**.
- **File size and location on disk**.
- **Deleted file records (until overwritten)**.

Forensically, the **MFT is invaluable** because:

- It **tracks file creation, modification, and deletion**, even if logs are cleared.
- It can **recover deleted file metadata**.
- It provides a **timeline of file activity**.

> **⚠️ Limitations:**
> 
> - The MFT only exists on **NTFS-formatted drives** (not FAT32, exFAT, etc.).
> - Deleted files can **lose content** if overwritten, but metadata may persist.
> - SSDs with **TRIM enabled** can erase MFT entries for deleted files.

---

## **📍 Where to Find It?**

The **MFT is a hidden system file** stored at:

```
C:\$MFT
```

Since it is a protected system file, it **cannot be accessed directly** from Windows Explorer.

---

## **🛠️ How to Extract It (Step by Step)**

We will use **MFTECmd**, a forensic tool for extracting and analyzing MFT data.

### **Method 1: Manual Extraction**

1. **Open Command Prompt as Administrator**.
2. **Copy the MFT to a working directory**:
    
    ```cmd
    copy \\.\C:\$MFT C:\Temp\$MFT
    ```
    
    - If access is denied, use a **live forensic boot disk**.

---

### **Method 2: Automated Extraction with MFTECmd**

#### **1️⃣ Download MFTECmd**

- Get it from **[Eric Zimmerman's GitHub](https://ericzimmerman.github.io/)**.
- Extract it to a working directory.

#### **2️⃣ Run MFTECmd to Parse the MFT**

Navigate to the tool’s folder and run:

```cmd
MFTECmd.exe -f C:\Temp\$MFT -o C:\ExtractedResults
```

- `-f` specifies the input MFT file.
- `-o` defines the output folder for parsed data.

#### **3️⃣ Review Extracted Data**

- Open the CSV files in **Excel**.
- Look for:
    - **File paths and names**.
    - **Creation, modification, access timestamps**.
    - **Deleted file records**.

---

## **📊 How to Analyze It (Step by Step)**

|**Step**|**Action**|**Details**|
|---|---|---|
|**1. Open the Extracted CSV File**|Use Excel for filtering|Displays file activity records.|
|**2. Identify File Creations**|Look at the `Creation Time` column|Shows when a file was first written.|
|**3. Track Modifications**|Check `Last Modified` timestamp|Helps detect unauthorized changes.|
|**4. Investigate Deleted Files**|Look for files marked as deleted but still in MFT|May reveal forensic recoverable data.|
|**5. Analyze MFT Entry Modifications**|Look at `MFT Entry Modified` time|Shows when a file's metadata was last altered.|
|**6. Correlate with Other Artifacts**|Compare with Event Logs and Prefetch|Provides a full timeline of file activity.|

---

## **🚨 Real-World Use Cases**

### **📌 Incident Response**

- Identify **which files were created, modified, or deleted during an attack**.
- Detect **timestamp tampering (anti-forensic techniques)**.

### **📌 Malware Analysis**

- Track **when a malicious file was dropped on the system**.
- Investigate **deleted malware remnants**.

### **📌 Insider Threat Investigations**

- Determine if **sensitive files were created or removed**.
- Verify if **a user attempted to hide activity by renaming files**.

---

## **🔎 Summary**

|**Category**|**Details**|
|---|---|
|**Location**|`C:\$MFT`|
|**File Type**|NTFS System File|
|**Extraction Tool**|`MFTECmd`|
|**Key Information**|File creation, modification, access, deletion records|
|**Forensic Value**|Tracks file system activity, deleted files, and timeline reconstruction|

---
