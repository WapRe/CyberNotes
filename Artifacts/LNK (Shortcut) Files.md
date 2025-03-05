## ✅ **What is it?**

LNK (shortcut) files are **Windows-generated files that store metadata about recently accessed files, folders, or applications**. They are automatically created whenever a user opens a file via **Windows Explorer**, a **network share**, or **removable media**.

Forensically, LNK files are valuable because:

- They **reveal file access history**, even if the file has been deleted.
- They **store full file paths**, timestamps, and drive serial numbers.
- They **track removable media activity** (USB devices, network shares).

> **⚠️ Limitations:**
> 
> - LNK files **are not created when files are opened from within applications** (e.g., opening a file in Word via "File > Open").
> - If **LNK caching is disabled**, fewer shortcuts may be available.
> - Attackers can **manipulate LNK files** to execute malware.

---

## **📍 Where to Find It?**

LNK files are typically stored in two locations:

|**Location**|**Purpose**|
|---|---|
|`C:\Users\%USERNAME%\AppData\Roaming\Microsoft\Windows\Recent\`|Tracks recently accessed files.|
|`C:\Users\%USERNAME%\AppData\Roaming\Microsoft\Windows\Recent\AutomaticDestinations\`|Works with Jump Lists to track frequent file usage.|

- LNK files can also be **manually placed on the Desktop** or in **custom locations**.

---

## **🛠️ How to Extract It (Step by Step)**

We will use **LECmd**, a forensic tool for parsing LNK metadata.

### **Method 1: Manual Collection**

1. **Navigate to the LNK Directory**
    
    - Open **File Explorer**.
    - Go to:
        
        ```
        C:\Users\%USERNAME%\AppData\Roaming\Microsoft\Windows\Recent\
        ```
        
    - Copy all `.lnk` files to a forensic workstation.
2. **Check Desktop and USB Locations**
    
    - Look for **shortcuts manually created** on the Desktop or external drives.

---

### **Method 2: Automated Extraction with LECmd**

#### **1️⃣ Download LECmd**

- Get it from **[Eric Zimmerman's GitHub](https://ericzimmerman.github.io/)**.
- Extract to a working directory.

#### **2️⃣ Run LECmd on LNK Files**

Navigate to the tool’s folder and run:

```cmd
LECmd.exe -d C:\Users\%USERNAME%\AppData\Roaming\Microsoft\Windows\Recent\ -o C:\ExtractedResults
```

- `-d` specifies the directory containing LNK files.
- `-o` defines the output folder for extracted data.

#### **3️⃣ Review Extracted Data**

- Open the CSV or text file generated.
- Look for:
    - **File paths** (`Target Path` column).
    - **Last access timestamps**.
    - **Drive serial numbers** (useful for tracking USB activity).

---

## **📊 How to Analyze It (Step by Step)**

|**Step**|**Action**|**Details**|
|---|---|---|
|**1. Open the Parsed Report**|Load `lnk_report.csv` in Excel or a text editor|Displays extracted metadata.|
|**2. Identify Accessed Files**|Look at the `Target Path` column|Shows the original location of the accessed file.|
|**3. Review Timestamps**|Check `Created`, `Last Modified`, `Last Accessed`|Helps reconstruct the file access timeline.|
|**4. Check for USB Activity**|Look at the `Drive Serial Number` field|Matches LNK files to specific USB devices.|
|**5. Look for Deleted Files**|If the file no longer exists, LNK files may still reference it|Can reveal evidence of tampering.|
|**6. Correlate with Other Artifacts**|Compare with Jump Lists and Registry entries|Helps verify file access history.|

---

## **🚨 Real-World Use Cases**

### **📌 Incident Response**

- Identify **which files an attacker accessed or exfiltrated**.
- Find **evidence of removable media usage (USB drives, network shares).**

### **📌 Malware Analysis**

- Detect **LNK-based malware**, where attackers craft malicious shortcuts to execute payloads.
- Track **execution paths** of suspicious programs.

### **📌 Insider Threat Investigations**

- Verify if a user accessed **confidential documents**.
- Detect **file tampering or deletion attempts**.

---

## **🔎 Summary**

|**Category**|**Details**|
|---|---|
|**Location**|`C:\Users\%USERNAME%\AppData\Roaming\Microsoft\Windows\Recent\`|
|**File Type**|`.lnk` (Shortcut files)|
|**Extraction Tool**|`LECmd`|
|**Key Information**|File paths, timestamps, USB device tracking|
|**Forensic Value**|Tracks user file access and potential data exfiltration|

---
