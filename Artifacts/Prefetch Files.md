## ✅ **What is it?**

Prefetch files (`.pf`) are created by Windows to speed up the loading of frequently used applications. They store information about recently executed programs, such as:

- File paths of executed applications.
- Execution timestamps (first and last run).
- Number of times an application has been executed.
- List of DLLs and supporting files loaded by the application.

Prefetch is enabled by default on **Windows 7, 8, 10, and 11**, but **Windows Server editions** often disable it by default.

### **🔍 Why is it important in forensics?**

- Tracks **executed applications**, even if deleted from disk.
- Helps establish a **timeline of activity** based on execution timestamps.
- Detects **malicious executions** (e.g., malware or persistence mechanisms).
- Confirms **user activity** on a machine.

---

## **📍 Where to Find It?**

- **Location:** `C:\Windows\Prefetch\`
- **File Extension:** `.pf`
- **Naming Convention:** `<ApplicationName>-<Hash>.pf`
    - Example: `notepad.exe-1234ABCD.pf`

> **⚠️ Important:** Prefetch files are only created if **Prefetching is enabled** in Windows. If a system has `EnablePrefetcher` set to `0` in the registry (`HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management\PrefetchParameters`), there will be no `.pf` files.

---

## **🛠️ How to Extract It (Step by Step)**

We'll use **PECmd** from Eric Zimmerman's toolset, one of the most widely used forensic tools for Prefetch analysis.

### **Method 1: Manual Collection**

1. **Access the Prefetch Directory:**
    
    - Open `File Explorer`.
    - Navigate to `C:\Windows\Prefetch\`.
    - Copy all `.pf` files to a forensic workstation for analysis.
2. **If Access is Denied:**
    
    - Run `cmd` as Administrator and use:
        
        ```cmd
        takeown /F C:\Windows\Prefetch\* /A
        icacls C:\Windows\Prefetch\* /grant Administrators:F
        ```
        
    - This grants access to the Prefetch files.

---

### **Method 2: Automated Extraction with PECmd**

PECmd (`Prefetch Explorer Command Line`) is a powerful Prefetch parsing tool.

#### **1️⃣ Download PECmd**

- Download it from **Eric Zimmerman's repository**: [https://ericzimmerman.github.io/](https://ericzimmerman.github.io/)
- Extract the zip file and navigate to the directory containing `PECmd.exe`.

#### **2️⃣ Extract and Parse Prefetch Files**

Open **Command Prompt (cmd) as Administrator**, then navigate to the folder:

```cmd
cd C:\Path\To\PECmd
```

Run the following command to extract details from the Prefetch folder:

```cmd
PECmd.exe -d C:\Windows\Prefetch\ -o C:\ExtractedResults
```

- `-d` specifies the directory containing the Prefetch files.
- `-o` defines the output directory where the parsed data will be stored.

#### **3️⃣ Review Output**

- The results will be saved as `.csv` files, which you can open in Excel or a text editor.

> **Alternative Tool:** `WinPrefetchView` (GUI-based) for a quick overview.

---

## **📊 How to Analyze It (Step by Step)**

Once you have extracted the `.pf` files, the next step is to analyze them to determine execution history.

|**Step**|**Action**|**Details**|
|---|---|---|
|**1. Open Parsed Output**|Open the `.csv` report generated by PECmd|Use Excel or a forensic text editor to view the extracted data|
|**2. Identify Executed Programs**|Look at the `Application Name` field|This tells you which programs were executed on the system|
|**3. Review Execution Timestamps**|Check `Last Executed` and `First Executed` timestamps|Helps create a timeline of activity|
|**4. Check Execution Count**|Look at the `Run Count` column|Determines how frequently the program was run|
|**5. Analyze Loaded Modules**|Review the list of associated DLLs and files|Detects malware or uncommon dependencies|
|**6. Correlate with Other Artifacts**|Compare with Event Logs and Amcache|Cross-check execution history for more details|
|**7. Detect Suspicious Activity**|Look for unusual executables|Unexpected paths (e.g., `C:\Users\Public\Temp\malware.exe`) may indicate compromise|

---

## **🚨 Real-World Use Cases**

### **📌 Incident Response**

- Determine if a suspicious program was executed **even if it was later deleted**.
- Validate whether a script or attack tool (e.g., `mimikatz.exe`) was used.

### **📌 Malware Analysis**

- Prefetch files can reveal **hidden malware activity** by showing execution timestamps and associated DLLs.
- Useful for detecting **fileless malware**, as some payloads only exist in memory but still generate a Prefetch entry.

### **📌 Insider Threat Investigations**

- Detect unauthorized access by checking which tools an employee executed.
- Correlate Prefetch timestamps with **logins or remote access events**.

---

## **🔎 Summary**

|**Category**|**Details**|
|---|---|
|**Location**|`C:\Windows\Prefetch\`|
|**File Type**|`.pf`|
|**Extraction Tool**|`PECmd`|
|**Key Information**|First/last execution, execution count, associated files|
|**Forensic Value**|Tracks application execution history, detects malware activity|

---
