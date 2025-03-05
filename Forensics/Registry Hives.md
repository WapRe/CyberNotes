## ✅ **What is it?**

The Windows Registry is a hierarchical database that **stores system configurations, user preferences, and application settings**. It contains critical forensic artifacts, such as:

- **User activity (recently accessed files, last logged-in user, installed programs).**
- **System settings (startup programs, USB device history, network settings).**
- **Persistence mechanisms used by malware.**

> **⚠️ Limitations:**
> 
> - Some registry values are **volatile** and may disappear after a reboot.
> - The **registry can be manipulated by attackers** to hide traces.

---

## **📍 Where to Find It?**

Windows Registry data is stored in **hives**, which are collections of registry keys and values.

| **Registry Hive** | **File Location**                                                  | **Forensic Use**                                                          |
| ----------------- | ------------------------------------------------------------------ | ------------------------------------------------------------------------- |
| **SYSTEM**        | `C:\Windows\System32\config\SYSTEM`                                | Tracks startup settings, installed drivers, network configurations.       |
| **SOFTWARE**      | `C:\Windows\System32\config\SOFTWARE`                              | Lists installed programs, application settings.                           |
| **SAM**           | `C:\Windows\System32\config\SAM`                                   | Stores local user account details and password hashes.                    |
| **SECURITY**      | `C:\Windows\System32\config\SECURITY`                              | Contains security policies and audit settings.                            |
| **NTUSER.DAT**    | `C:\Users\%USERNAME%\NTUSER.DAT`                                   | Tracks user activity (recent files, last shutdown time, wallpaper, etc.). |
| **USRCLASS.DAT**  | `C:\Users\%USERNAME%\AppData\Local\Microsoft\Windows\UsrClass.dat` | Stores user shell settings, recent file access history.                   |

---

## **🛠️ How to Extract It (Step by Step)**

We will use **Registry Explorer**, a powerful tool for extracting and analyzing registry data.

### **Method 1: Manual Extraction**

1. **Navigate to Registry Hive Files**
    
    - Open **File Explorer**.
    - Copy the required hive file (e.g., `SYSTEM`, `NTUSER.DAT`) from:
        
        ```
        C:\Windows\System32\config\
        ```
        
        or
        
        ```
        C:\Users\%USERNAME%\
        ```
        
    - Paste them into a **forensic workstation**.
2. **If Access is Denied**
    
    - Run **Command Prompt as Administrator** and use:
        
        ```cmd
        takeown /F C:\Windows\System32\config\SYSTEM
        icacls C:\Windows\System32\config\SYSTEM /grant Administrators:F
        ```
        

---

### **Method 2: Automated Extraction with Registry Explorer**

#### **1️⃣ Download Registry Explorer**

- Get it from **[Eric Zimmerman's GitHub](https://ericzimmerman.github.io/)**.
- Extract the tool to a working directory.

#### **2️⃣ Load the Registry Hive**

- Open **RegistryExplorer.exe**.
- Click **File > Load Hive**.
- Select the copied `.dat` file (e.g., `NTUSER.DAT` or `SYSTEM`).

#### **3️⃣ Browse Key Evidence**

- Use **Ctrl+F** to search for specific registry keys (e.g., `Run` for startup programs).
- Navigate to:
    - `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services` (for installed services).
    - `HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run` (for persistence mechanisms).

---

## **📊 How to Analyze It (Step by Step)**

| **Step**                              | **Action**                                                        | **Details**                                   |
| ------------------------------------- | ----------------------------------------------------------------- | --------------------------------------------- |
| **1. Open RegistryExplorer**          | Load the extracted hive file                                      | Allows easy navigation of registry keys.      |
| **2. Identify Installed Programs**    | Navigate to `SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall` | Lists installed applications with timestamps. |
| **3. Check Startup Programs**         | Go to `SOFTWARE\Microsoft\Windows\CurrentVersion\Run`             | Malware often persists here.                  |
| **4. Review USB Device History**      | Look at `SYSTEM\CurrentControlSet\Enum\USBSTOR`                   | Tracks USB devices plugged into the system.   |
| **5. Investigate User Activity**      | Open `NTUSER.DAT` and check `RecentDocs`                          | Shows recently accessed files.                |
| **6. Correlate with Other Artifacts** | Compare with Event Logs and Amcache                               | Helps reconstruct full user activity.         |

---

## **🚨 Real-World Use Cases**

### **📌 Incident Response**

- Detect **malware persistence** by checking `Run` keys in the **SOFTWARE** hive.
- Investigate **unauthorized USB access** by analyzing the **SYSTEM** hive.

### **📌 Malware Analysis**

- Identify **hidden services or startup entries** that allow malware to persist.
- Track **modified registry values** used for privilege escalation.

### **📌 Insider Threat Investigations**

- Check **recently accessed files** in `NTUSER.DAT` to confirm unauthorized activity.
- Analyze **deleted user accounts** in the **SAM hive**.

---

## **🔎 Summary**

|**Category**|**Details**|
|---|---|
|**Location**|`C:\Windows\System32\config\` & `C:\Users\%USERNAME%\NTUSER.DAT`|
|**File Type**|`.dat` (Registry Hives)|
|**Extraction Tool**|`Registry Explorer`|
|**Key Information**|Installed programs, user activity, USB history, startup entries|
|**Forensic Value**|Tracks system changes, malware persistence, and user behavior|

---
