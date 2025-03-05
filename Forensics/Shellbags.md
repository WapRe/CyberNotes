## ✅ **What is it?**

Shellbags are **Windows registry artifacts that track folder navigation in File Explorer**. They store information about **folders that have been accessed**, including those on:

- **Local drives** (C:, D:, etc.).
- **USB devices** (external hard drives, flash drives).
- **Network shares** (`\\server\share`).
- **Deleted directories** (folders that no longer exist but were accessed).

Forensically, Shellbags are valuable because:

- They **reveal evidence of accessed folders**, even if files or folders were deleted.
- They **track removable device usage**, helping to identify exfiltration.
- They **preserve timestamps** of folder access.
- They **record folder viewing preferences** (e.g., icon vs. list view).

> **⚠️ Limitations:**
> 
> - Shellbags **do not track individual file access**, only folder navigation.
> - They **do not store timestamps for all actions** (modification timestamps are limited).
> - They can be **manipulated or cleared** by attackers.

---

## **📍 Where to Find It?**

Shellbag data is stored in the **NTUSER.DAT** registry hive for each user.

|**Registry Path**|**Purpose**|
|---|---|
|`HKCU\Software\Microsoft\Windows\Shell\BagMRU`|Tracks folder navigation history.|
|`HKCU\Software\Microsoft\Windows\Shell\Bags`|Stores folder view settings (icons, list, details, etc.).|

**Location of Registry Hive:**

```
C:\Users\%USERNAME%\NTUSER.DAT
```

---

## **🛠️ How to Extract It (Step by Step)**

We will use **ShellBags Explorer**, a forensic tool for parsing Shellbags.

### **Method 1: Manual Extraction**

1. **Copy the NTUSER.DAT Registry Hive**
    
    - Open **Command Prompt as Administrator**.
    - Copy the registry hive for the target user:
        
        ```cmd
        copy C:\Users\%USERNAME%\NTUSER.DAT C:\Temp\NTUSER.DAT
        ```
        
2. **Load the Hive in Registry Viewer**
    
    - Open **Registry Editor (`regedit`)**.
    - Click **File > Load Hive**.
    - Select the copied `NTUSER.DAT` file.
    - Navigate to:
        
        ```
        HKCU\Software\Microsoft\Windows\Shell\BagMRU
        ```
        

---

### **Method 2: Automated Extraction with ShellBags Explorer**

#### **1️⃣ Download ShellBags Explorer**

- Get it from **[Eric Zimmerman's GitHub](https://ericzimmerman.github.io/)**.
- Extract the tool to a working directory.

#### **2️⃣ Run ShellBags Explorer**

- Open **ShellBagsExplorer.exe**.
- Click **File > Load Hive**.
- Select `NTUSER.DAT` from `C:\Temp\`.

#### **3️⃣ Review Extracted Data**

- Navigate through the **decoded folder structures**.
- Look for **timestamps, accessed paths, and USB device names**.

---

## **📊 How to Analyze It (Step by Step)**

|**Step**|**Action**|**Details**|
|---|---|---|
|**1. Open ShellBags Explorer**|Load the extracted NTUSER.DAT hive|Allows structured navigation.|
|**2. Identify Accessed Folders**|Look at `Path` column|Shows folder names and locations.|
|**3. Check Device Usage**|Look for `Removable Drives` or `Network Paths`|Tracks folders accessed on external devices.|
|**4. Review Folder Timestamps**|Look at `Last Modified` and `Last Accessed` fields|Helps reconstruct user activity.|
|**5. Look for Deleted Folders**|If a folder no longer exists on disk but appears in Shellbags|Indicates deleted evidence.|
|**6. Correlate with Other Artifacts**|Compare with Jump Lists and LNK files|Strengthens file access reconstruction.|

---

## **🚨 Real-World Use Cases**

### **📌 Incident Response**

- Determine if an **attacker browsed sensitive directories**.
- Confirm whether **USB devices or network shares** were accessed.

### **📌 Insider Threat Investigations**

- Track **employee access to restricted folders**.
- Detect attempts to **delete folders after accessing them**.

### **📌 Malware Analysis**

- Identify **folders where malware was executed from**.
- Detect **hidden persistence locations** used by attackers.

---

## **🔎 Summary**

|**Category**|**Details**|
|---|---|
|**Location**|`HKCU\Software\Microsoft\Windows\Shell\BagMRU` (NTUSER.DAT)|
|**File Type**|Registry Keys|
|**Extraction Tool**|`ShellBags Explorer`|
|**Key Information**|Accessed folders, timestamps, USB/network history|
|**Forensic Value**|Tracks user navigation, deleted folders, removable devices|

---
