## ✅ **What is it?**

Software Restriction Policies (**SRP**) are **Windows security settings** that define which applications **can or cannot run** on a system. They help prevent the execution of **unauthorized programs, malware, and scripts**.

Forensically, **SRP is useful** because:

- It helps determine **if an attacker modified security policies** to allow malicious execution.
- It reveals **restrictions placed on software**, useful in incident response.
- It can show **attempted policy bypass attempts** by attackers.

> **⚠️ Limitations:**
> 
> - **SRP is not enabled by default** on most Windows systems.
> - Attackers **can disable or manipulate policies** to allow malware execution.
> - It only tracks **policy enforcement**, not every executed process.

---

## **📍 Where to Find It?**

SRP settings are stored in the **Windows Registry** under:

|**Registry Path**|**Purpose**|
|---|---|
|`HKLM\Software\Policies\Microsoft\Windows\Safer`|Stores global SRP settings.|
|`HKCU\Software\Policies\Microsoft\Windows\Safer`|Stores user-specific SRP settings.|

SRP rules also appear in **Local Group Policy**:

|**Location**|**Purpose**|
|---|---|
|`gpedit.msc > Computer Configuration > Windows Settings > Security Settings > Software Restriction Policies`|GUI for managing SRP rules.|

---

## **🛠️ How to Extract It (Step by Step)**

We will use **RegRipper** to extract SRP data from the Windows Registry.

### **Method 1: Manual Extraction**

1. **Open Registry Editor (`regedit`)**.
2. **Navigate to the SRP Key**:
    
    ```
    HKLM\Software\Policies\Microsoft\Windows\Safer
    ```
    
3. **Look for Policy Rules**:
    - `DefaultLevel`: Defines the enforcement level (Disallowed, Unrestricted, Basic User).
    - `ExecutableTypes`: Lists restricted file types (e.g., `.exe, .bat, .ps1`).
    - `Paths`: Specifies allowed or blocked paths.

---

### **Method 2: Automated Extraction with RegRipper**

#### **1️⃣ Download RegRipper**

- Get it from **[RegRipper GitHub](https://github.com/keydet89/RegRipper3.0)**.
- Extract it to a working directory.

#### **2️⃣ Extract SRP Policies from the Registry**

First, save the **SYSTEM registry hive**:

```cmd
reg save HKLM\SOFTWARE C:\Temp\SOFTWARE.hive
```

Then, run RegRipper:

```cmd
rip.exe -r C:\Temp\SOFTWARE.hive -p srp
```

- This extracts **all Software Restriction Policies** from the registry.

#### **3️⃣ Review Extracted Data**

- Open the **output text file** and look for:
    - **Restricted paths or extensions**.
    - **Policy enforcement level**.
    - **Possible tampering attempts**.

---

## **📊 How to Analyze It (Step by Step)**

|**Step**|**Action**|**Details**|
|---|---|---|
|**1. Open Extracted Registry Data**|View output from RegRipper or regedit|Displays all SRP policies.|
|**2. Identify Restriction Level**|Look at `DefaultLevel`|Determines if policies are enforced.|
|**3. Review Blocked/Allowed Paths**|Check `Paths` values|Shows what applications are restricted.|
|**4. Investigate Bypasses**|Look for removed or altered policies|May indicate attacker tampering.|
|**5. Correlate with Process Execution Artifacts**|Compare with Prefetch, Amcache, and Event Logs|Confirms if blocked applications were executed anyway.|

---

## **🚨 Real-World Use Cases**

### **📌 Incident Response**

- Detect **if an attacker modified SRP settings** to allow malware execution.
- Verify **if security policies prevented or allowed unauthorized programs**.

### **📌 Malware Analysis**

- Check if **SRP was bypassed** by malware to execute unauthorized code.
- Investigate **whitelisted applications used for lateral movement**.

### **📌 Insider Threat Investigations**

- Determine if an **employee disabled SRP to install unauthorized software**.
- Verify if **script execution was restricted or allowed**.

---

## **🔎 Summary**

|**Category**|**Details**|
|---|---|
|**Location**|`HKLM\Software\Policies\Microsoft\Windows\Safer`|
|**File Type**|Registry Keys|
|**Extraction Tool**|`RegRipper`|
|**Key Information**|Blocked/allowed apps, policy enforcement, possible bypasses|
|**Forensic Value**|Tracks software execution restrictions and policy modifications|

---
