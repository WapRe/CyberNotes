## ✅ **What is it?**

BitLocker is a **full-disk encryption feature** built into Windows to protect data from unauthorized access. When enabled, BitLocker encrypts the entire drive, requiring a password or recovery key to unlock.

The **BitLocker Recovery Key** is a unique **48-digit numerical key** that can be used to decrypt the drive if access credentials are lost. Forensically, **locating the recovery key can help investigators decrypt BitLocker-protected drives**.

> **⚠️ Limitations:**
> 
> - If the **BitLocker key is not backed up**, data is nearly impossible to recover.
> - Attackers may delete recovery keys after enabling BitLocker to prevent forensic access.
> - If **TPM-only protection is used**, recovery keys may not be available.

---

## **📍 Where to Find It?**

BitLocker Recovery Keys can be stored in **multiple locations**, depending on how the system was configured.

|**Storage Location**|**Path / Access Method**|**Forensic Use**|
|---|---|---|
|**Windows Registry**|`HKLM\SYSTEM\CurrentControlSet\Control\FVE\RecoveryGuid`|If not deleted, may contain recovery keys.|
|**Active Directory (AD)**|`msFVE-RecoveryInformation` attribute|If domain-joined, keys may be stored in AD.|
|**Microsoft Account**|`https://account.microsoft.com/devices/recoverykey`|If enabled, the key may be saved to a Microsoft account.|
|**Local Text File**|`C:\Users\%USERNAME%\Documents\BitLocker Recovery Key.txt`|Some users manually save recovery keys in files.|
|**USB Drive**|Plugging in a pre-configured USB|If BitLocker was set up with USB key storage.|

---

## **🛠️ How to Extract It (Step by Step)**

We will use **RegRipper** to extract potential recovery keys from the Windows Registry.

### **Method 1: Manual Extraction**

1. **Check the Registry for Recovery Keys**
    
    - Open **Command Prompt as Administrator**.
    - Run **Registry Editor** (`regedit`).
    - Navigate to:
        
        ```
        HKLM\SYSTEM\CurrentControlSet\Control\FVE
        ```
        
    - Look for values like:
        
        ```
        RecoveryGuid
        IdentificationField
        ```
        
    - If present, the **GUID value** can be used to check for stored recovery keys.
2. **Check Local Drives for Saved Recovery Keys**
    
    - Search for **BitLocker Recovery Key.txt** files:
        
        ```cmd
        dir /s /b "C:\BitLocker Recovery Key*.txt"
        ```
        
    - Check USB drives if the system was set up with a **startup key**.

---

### **Method 2: Automated Extraction with RegRipper**

#### **1️⃣ Download RegRipper**

- Get it from **[RegRipper GitHub](https://github.com/keydet89/RegRipper3.0)**.
- Extract it to a working directory.

#### **2️⃣ Extract BitLocker Recovery Keys from the SYSTEM Hive**

Before running RegRipper, extract the **SYSTEM registry hive**:

```cmd
reg save HKLM\SYSTEM C:\Temp\SYSTEM.hive
```

Then, run RegRipper:

```cmd
rip.exe -r C:\Temp\SYSTEM.hive -p bitlocker
```

- This extracts any BitLocker keys stored in the registry.

#### **3️⃣ Review Extracted Data**

- Open the **output text file** and search for:
    - **Recovery GUIDs**.
    - **Encrypted keys** that may be used for decryption.

---

## **📊 How to Analyze It (Step by Step)**

|**Step**|**Action**|**Details**|
|---|---|---|
|**1. Open RegRipper Output**|View extracted registry keys|Looks for BitLocker recovery GUIDs.|
|**2. Search for Recovery Keys**|Look for `RecoveryGuid` values|May indicate the presence of a stored key.|
|**3. Check for Saved Text Files**|Search for `BitLocker Recovery Key.txt`|Users sometimes save keys in documents.|
|**4. Investigate USB Startup Keys**|Check `C:\Boot\` or external drives|If USB-based unlocking was used.|
|**5. Correlate with AD or Microsoft Account**|If domain-joined, check Active Directory|If cloud-linked, attempt Microsoft account lookup.|

---

## **🚨 Real-World Use Cases**

### **📌 Incident Response**

- Recover access to **encrypted evidence drives**.
- Verify if **BitLocker was enabled by an attacker to lock out investigators**.

### **📌 Data Recovery**

- Retrieve **lost encryption keys** for forensic decryption.
- Extract BitLocker keys from **backups or previous system snapshots**.

### **📌 Insider Threat Investigations**

- Determine if **BitLocker was used to hide stolen data**.
- Check if an employee **enabled encryption right before departure**.

---

## **🔎 Summary**

|**Category**|**Details**|
|---|---|
|**Location**|`HKLM\SYSTEM\CurrentControlSet\Control\FVE\RecoveryGuid`|
|**File Type**|Registry Keys, Text Files, USB Startup Keys|
|**Extraction Tool**|`RegRipper`|
|**Key Information**|Recovery GUIDs, stored encryption keys, decryption options|
|**Forensic Value**|Helps recover encrypted drives, detect unauthorized encryption|

---
