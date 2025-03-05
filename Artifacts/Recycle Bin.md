## ✅ **What is it?**

The **Recycle Bin** is where Windows temporarily stores **deleted files before permanent removal**. It allows users to recover files before they are permanently erased.

Forensically, it helps:

- **Recover deleted files** that have not been permanently removed.
- **Identify timestamps related to file deletion.**
- **Track who deleted a file and from where.**

> **⚠️ Limitations:**
> 
> - If a file is **shift-deleted (Shift + Del)**, it **bypasses** the Recycle Bin.
> - Files deleted from **USB drives or network shares** do not appear in the Recycle Bin.
> - If the bin is **emptied**, recovery depends on **MFT (Master File Table) analysis**.

---

## **📍 Where to Find It?**

The Recycle Bin structure differs between **Windows versions**:

```
C:\$Recycle.Bin\SID\
```

- Each user has a separate **SID-based folder**.
- Example:
    
    ```
    C:\$Recycle.Bin\S-1-5-21-1234567890-1001\
    ```
    

Inside each SID folder, there are **two file types**:

|**File Type**|**Naming Format**|**Purpose**|
|---|---|---|
|**$I Files**|`$I<random characters>.ext`|Stores metadata (original filename, size, deletion timestamp).|
|**$R Files**|`$R<random characters>.ext`|Stores actual deleted file content.|

- **$I files** contain important forensic data, even if the **$R file (content) is gone**.

---

## **🛠️ How to Extract It (Step by Step)**

We will use **Rifiuti2**, a forensic tool designed for analyzing Recycle Bin data.

### **Method 1: Manual Collection**

1. **Navigate to the Recycle Bin**
    
    - Open **File Explorer**.
    - Go to:
        
        ```
        C:\$Recycle.Bin\S-1-5-21-1234567890-1001\
        ```
        
    - Copy all `$I` and `$R` files to a forensic workstation.
2. **View Metadata from $I Files**
    
    - Open a **hex editor** (like HxD) and inspect `$I` files.
    - The original filename, file size, and deletion timestamp are embedded.

---

### **Method 2: Automated Extraction with Rifiuti2**

#### **1️⃣ Download Rifiuti2**

- Get it from **[GitHub Rifiuti2](https://github.com/abelcheung/rifiuti2)**.
- Extract the tool to a working directory.

#### **2️⃣ Run Rifiuti2 on Recycle Bin Files**

Navigate to the tool’s folder and run:

```cmd
rifiuti.exe -o C:\ExtractedResults\recycle_report.csv C:\$Recycle.Bin\S-1-5-21-1234567890-1001\
```

- `-o` specifies the output report location.
- The tool will parse `$I` files and extract:
    - **Original filename and path.**
    - **Date and time of deletion.**
    - **File size before deletion.**

#### **3️⃣ Review Extracted Data**

- Open the `recycle_report.csv` in **Excel** for easier filtering.

---

## **📊 How to Analyze It (Step by Step)**

|**Step**|**Action**|**Details**|
|---|---|---|
|**1. Open the Parsed Report**|Load `recycle_report.csv`|Displays deleted file metadata.|
|**2. Identify Deleted Files**|Look at `Original Filename` column|Shows the name and location before deletion.|
|**3. Check Deletion Timestamps**|Review the `Deletion Date` field|Helps reconstruct when a file was deleted.|
|**4. Confirm File Size**|Look at the `Original Size` column|Determines if the file was large (potential exfiltration risk).|
|**5. Recover File Content**|If `$R` file exists, rename it to its original extension|Allows full recovery of deleted files.|
|**6. Correlate with Other Artifacts**|Compare with Prefetch and Jump Lists|Helps verify if the file was accessed before deletion.|

---

## **🚨 Real-World Use Cases**

### **📌 Incident Response**

- Identify if an attacker **deleted logs or sensitive files**.
- Correlate deleted malware files with **Prefetch data**.

### **📌 Insider Threat Investigations**

- Detect **attempts to remove confidential documents**.
- Verify if an employee **deleted files before resignation**.

### **📌 Malware Analysis**

- Check if **malware self-deletes** after execution.
- Restore deleted **malicious payloads** for analysis.

---

## **🔎 Summary**

|**Category**|**Details**|
|---|---|
|**Location**|`C:\$Recycle.Bin\S-1-5-21-1234567890-1001\`|
|**File Type**|`$I` (metadata), `$R` (content)|
|**Extraction Tool**|`Rifiuti2`|
|**Key Information**|Deleted file paths, timestamps, sizes|
|**Forensic Value**|Tracks deleted files and attempts to cover activity|

---
