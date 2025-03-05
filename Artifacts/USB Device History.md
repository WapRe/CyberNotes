## ✅ **What is it?**

Windows keeps track of **USB devices** that have been connected to the system. This includes:

- **Device names and unique serial numbers**.
- **First and last connection timestamps**.
- **User accounts that connected USB devices**.
- **Drive letters assigned to USB storage**.

Forensically, **USB artifacts are critical** because:

- They help **track unauthorized data transfers** via removable media.
- They reveal **potential exfiltration of sensitive files**.
- They can confirm if **malware was introduced via a USB device**.

> **⚠️ Limitations:**
> 
> - If a device was **only plugged in but not used**, fewer traces may exist.
> - **USB history may be cleared** by forensic-aware attackers.
> - Virtual machines may leave **false positives** due to USB passthrough.

---

## **📍 Where to Find USB Artifacts?**

Windows stores USB device artifacts in multiple locations:

### **1️⃣ USB Device History (Registry)**

|**Artifact**|**Registry Path**|**Purpose**|
|---|---|---|
|USB Storage History|`HKLM\SYSTEM\CurrentControlSet\Enum\USBSTOR`|Tracks connected USB storage devices.|
|USB Device Descriptions|`HKLM\SYSTEM\CurrentControlSet\Enum\USB`|Stores vendor and product details.|
|USB Drive Assignments|`HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\MountPoints2`|Lists drive letters assigned to USB devices.|
|Last Connected Timestamps|`HKLM\SYSTEM\CurrentControlSet\Control\DeviceClasses`|Records last USB connection time.|

### **2️⃣ USB Connection Logs (Event Logs)**

|**Log Name**|**Location**|**Purpose**|
|---|---|---|
|USB Plug-in Events|`Microsoft-Windows-DriverFrameworks-UserMode/Operational.evtx`|Logs device insertions/removals (Event ID 2003, 2100).|
|Disk Mount Events|`Microsoft-Windows-Partition/Diagnostic.evtx`|Records when storage volumes are mounted (Event ID 1006).|
|File Transfers via USB|`Microsoft-Windows-TaskScheduler/Operational.evtx`|Detects file copies if monitored.|

---

## **🛠️ How to Extract USB Artifacts (Step by Step)**

We will use **USBDeview** for listing connected devices, **RegRipper** for registry analysis, and **EvtxECmd** for event logs.

### **Method 1: Extracting USB History from Registry**

1. **Open Registry Editor (`regedit`)**.
2. **Navigate to:**
    
    ```
    HKLM\SYSTEM\CurrentControlSet\Enum\USBSTOR
    ```
    
3. **Look for Device Entries**
    - Each entry represents a **previously connected USB device**.
    - Device details include:
        - **VID (Vendor ID)** and **PID (Product ID)**.
        - **Serial number** (unique per device).
        - **First and last connected timestamps**.

#### **Automated Extraction with RegRipper**

Save the SYSTEM registry hive:

```cmd
reg save HKLM\SYSTEM C:\Temp\SYSTEM.hive
```

Then run:

```cmd
rip.exe -r C:\Temp\SYSTEM.hive -p usb
```

- This extracts **all USB device connection history**.

---

### **Method 2: Extracting USB Connection Logs (Event Logs)**

#### **1️⃣ Open Event Viewer**

- Navigate to:
    
    ```
    Applications and Services Logs > Microsoft > Windows > DriverFrameworks-UserMode > Operational
    ```
    
- Look for:
    - **Event ID 2003** → USB device inserted.
    - **Event ID 2100** → USB device removed.

#### **2️⃣ Export USB Event Logs**

Save logs for forensic analysis:

```cmd
wevtutil epl Microsoft-Windows-DriverFrameworks-UserMode/Operational C:\Temp\USB_Events.evtx
```

#### **3️⃣ Parse Logs with EvtxECmd**

Run:

```cmd
EvtxECmd.exe -f C:\Temp\USB_Events.evtx -o C:\ExtractedResults
```

- This extracts **timestamps, device details, and user interactions**.

---

### **Method 3: Listing Previously Connected USB Devices**

#### **1️⃣ Download USBDeview**

- Get it from **[NirSoft USBDeview](https://www.nirsoft.net/utils/usb_devices_view.html)**.
- Extract the tool to a working directory.

#### **2️⃣ Run USBDeview**

Navigate to the tool’s folder and run:

```cmd
USBDeview.exe /scomma C:\ExtractedResults\usb_history.csv
```

- This lists **all previously connected USB devices**, including:
    - **First and last connection timestamps**.
    - **Serial numbers**.
    - **Drive letters assigned**.

---

## **📊 How to Analyze USB Artifacts (Step by Step)**

|**Step**|**Action**|**Details**|
|---|---|---|
|**1. Extract USB History from Registry**|Use `RegRipper` on SYSTEM hive|Displays all USB devices ever connected.|
|**2. Analyze USB Connection Events**|Check Event ID 2003, 2100|Identifies who plugged in a device and when.|
|**3. Review File Transfers**|Look for Event ID 1006 in `Partition/Diagnostic` logs|Shows if files were copied from/to USB.|
|**4. Investigate USB Serial Numbers**|Compare with known devices|Helps track unauthorized USB usage.|
|**5. Correlate with File System Activity**|Compare timestamps with Jump Lists and MFT|Verifies file access via USB.|

---

## **🔎 How to Recover Deleted USB History**

If an attacker **clears USB history**, alternative forensic methods can help recover it:

|**Method**|**Description**|
|---|---|
|**MFT & USN Journal**|Tracks file creations, deletions, and movement on external drives.|
|**LNK Files & Jump Lists**|May store references to files opened from a USB device.|
|**Prefetch & Amcache**|Can log executables run from a USB.|
|**Event Logs**|Even if registry keys are deleted, event logs may persist.|
|**Windows Search Index (Windows.edb)**|May store file names and paths from USB storage.|

---

## **🚨 Real-World Use Cases**

### **📌 Incident Response**

- Identify **unauthorized USB connections** on secured systems.
- Detect **USB-based malware infections** (e.g., autorun scripts).

### **📌 Data Exfiltration Investigations**

- Determine **if sensitive files were copied to a USB drive**.
- Verify **which user account connected a specific device**.

### **📌 Insider Threat Investigations**

- Investigate **employees using USB drives for unauthorized access**.
- Recover **deleted USB connection records** to prove data theft.

---

## **🔎 Summary**

|**Category**|**Details**|
|---|---|
|**Location**|`Registry, Event Logs, USB Cache`|
|**File Type**|`.evtx`, `.dat`, `.bin`|
|**Extraction Tool**|`RegRipper`, `EvtxECmd`, `USBDeview`|
|**Key Information**|USB serial numbers, connection timestamps, assigned drive letters|
|**Forensic Value**|Tracks removable storage usage, data exfiltration, and unauthorized access|

---
