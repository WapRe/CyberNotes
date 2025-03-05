## ✅ **What is it?**

UserAssist is a **Windows registry artifact that tracks programs launched via the GUI** (Graphical User Interface). It records:

- **Executed applications** (EXE, MSC, CPL).
- **Timestamps of execution** (last run).
- **Execution count** (how many times an app was launched).

Unlike Prefetch or ShimCache, which focus on system-wide execution, **UserAssist is user-specific** and only logs applications run via the **Start Menu, Desktop, or Explorer**.

> **⚠️ Limitations:**
> 
> - **Does NOT track CLI executions** (e.g., programs run from Command Prompt or PowerShell).
> - Data is **ROT13 encoded**, requiring decoding.
> - Entries are **overwritten over time** as new programs are used.

---

## **📍 Where to Find It?**

UserAssist data is stored in the **NTUSER.DAT** registry hive for each user.

|**Registry Path**|**Purpose**|
|---|---|
|`HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\UserAssist\{GUID}\Count`|Stores application execution details (ROT13 encoded).|

- The `{GUID}` changes depending on the **Windows version**.
- **Each user has their own UserAssist key** inside `NTUSER.DAT`.

---

## **🛠️ How to Extract It (Step by Step)**

We will use **UserAssistView**, a forensic tool for parsing UserAssist data.

### **Method 1: Manual Extraction**

1. **Copy the NTUSER.DAT Registry Hive**
    
    - Open **Command Prompt as Administrator**.
    - Copy the registry hive:
        
        ```cmd
        copy C:\Users\%USERNAME%\NTUSER.DAT C:\Temp\NTUSER.DAT
        ```
        
2. **Load the Hive in Registry Editor**
    
    - Open **Registry Editor (`regedit`)**.
    - Click **File > Load Hive**.
    - Select `NTUSER.DAT` and navigate to:
        
        ```
        HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\UserAssist
        ```
        
3. **Decode ROT13 Entries**
    
    - The values are stored in **ROT13 encoding** (a simple letter substitution cipher).
    - Manually decode using an **online ROT13 converter** or scripting tools.

---

### **Method 2: Automated Extraction with UserAssistView**

#### **1️⃣ Download UserAssistView**

- Get it from **[NirSoft UserAssistView](https://www.nirsoft.net/utils/userassist_view.html)**.
- Extract to a working directory.

#### **2️⃣ Run UserAssistView**

- Open **UserAssistView.exe**.
- It will automatically load the UserAssist entries for the current system.

#### **3️⃣ Export Results**

- Click **File > Save As CSV** to export the parsed data.
- Review execution details including:
    - **Application Name** (decoded).
    - **Execution Count**.
    - **Last Execution Time**.

---

## **📊 How to Analyze It (Step by Step)**

|**Step**|**Action**|**Details**|
|---|---|---|
|**1. Open UserAssistView**|Load the extracted NTUSER.DAT hive|Automatically decodes ROT13 values.|
|**2. Identify Executed Applications**|Look at the `Decoded Name` column|Shows which programs were launched via the GUI.|
|**3. Review Execution Counts**|Check the `Count` column|Determines how frequently an application was run.|
|**4. Check Last Execution Time**|Look at `Last Executed` timestamp|Helps reconstruct user activity.|
|**5. Investigate Suspicious Apps**|Look for unusual programs|Attackers may run malicious scripts via Explorer.|
|**6. Correlate with Other Artifacts**|Compare with Prefetch, Amcache, and Jump Lists|Strengthens program execution analysis.|

---

## **🚨 Real-World Use Cases**

### **📌 Incident Response**

- Confirm **which programs a user executed** during an attack.
- Identify **unauthorized software launches** (e.g., hacking tools, malware).

### **📌 Malware Analysis**

- Detect **stealthy malware execution** through GUI-based launch methods.
- Correlate execution with **event logs** and **Prefetch files**.

### **📌 Insider Threat Investigations**

- Check if an employee **launched forbidden applications**.
- Detect **file exfiltration tools** run from Explorer.

---

## **🔎 Summary**

|**Category**|**Details**|
|---|---|
|**Location**|`HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\UserAssist` (NTUSER.DAT)|
|**File Type**|Registry Keys (ROT13 encoded)|
|**Extraction Tool**|`UserAssistView`|
|**Key Information**|Executed programs, execution count, last executed timestamp|
|**Forensic Value**|Tracks user-launched applications via GUI|

---

