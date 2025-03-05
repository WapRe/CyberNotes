## ✅ **What is it?**

The **DNS Cache** is a temporary database maintained by Windows that stores **recently resolved domain names** and their corresponding **IP addresses**. Every time a user visits a website or an application makes a network request, the **DNS query is stored in memory** for faster lookups.

Forensically, **DNS Cache is critical** because:

- It can reveal **visited domains**, even if browsing history was deleted.
- It provides **IP addresses associated with accessed domains**.
- It helps track **malicious command-and-control (C2) servers** used by malware.

> **⚠️ Limitations:**
> 
> - DNS Cache **is volatile** and is cleared upon reboot.
> - **Malware can flush the cache** to cover tracks (`ipconfig /flushdns`).
> - It does **not store timestamps**, only domain-IP mappings.

---

## **📍 Where to Find It?**

DNS Cache data is stored **in system memory** and can be retrieved using:

- **Command-line queries (`ipconfig /displaydns`)**.
- **Event Logs (`Microsoft-Windows-DNS-Client/Operational.evtx`)**.
- **Network captures (if logging is enabled)**.

---

## **🛠️ How to Extract It (Step by Step)**

We will use **ipconfig** for live analysis and **EvtxECmd** to extract DNS-related Event Logs.

### **Method 1: Live Extraction (Volatile Data)**

1. **Open Command Prompt as Administrator**.
2. **Dump the Current DNS Cache**:
    
    ```cmd
    ipconfig /displaydns > C:\Temp\dns_cache.txt
    ```
    
3. **Open and Analyze the File**:
    - Look for **suspicious domains**.
    - Identify **C2 servers or phishing sites**.

---

### **Method 2: Extracting DNS Logs from Event Viewer**

1. **Open Event Viewer (`eventvwr.msc`)**.
2. **Navigate to**:
    
    ```
    Applications and Services Logs > Microsoft > Windows > DNS-Client > Operational
    ```
    
3. **Look for DNS Query Events (`Event ID 1014`)**.
4. **Export the log** for forensic analysis.

---

### **Method 3: Automated Extraction with EvtxECmd**

#### **1️⃣ Download EvtxECmd**

- Get it from **[Eric Zimmerman's GitHub](https://ericzimmerman.github.io/)**.
- Extract to a working directory.

#### **2️⃣ Extract DNS Event Logs**

Run:

```cmd
EvtxECmd.exe -f "C:\Windows\System32\winevt\Logs\Microsoft-Windows-DNS-Client%4Operational.evtx" -o C:\ExtractedResults
```

- This extracts DNS query logs for review.

#### **3️⃣ Review Extracted Data**

- Open the CSV in **Excel**.
- Look for:
    - **Queried domains**.
    - **IP addresses returned**.
    - **Repeated requests to suspicious domains**.

---

## **📊 How to Analyze It (Step by Step)**

|**Step**|**Action**|**Details**|
|---|---|---|
|**1. Open Extracted Data**|Load the `.csv` or `.txt` output|Displays queried domains and IPs.|
|**2. Identify Suspicious Domains**|Check for `*.ru, *.cn, *.onion` domains|May indicate malicious traffic.|
|**3. Review Resolved IPs**|Compare with threat intelligence feeds|Identifies known malicious hosts.|
|**4. Check for High-Frequency Lookups**|Multiple requests in a short time|May indicate malware C2 activity.|
|**5. Correlate with Browser History and Network Logs**|Compare with other artifacts|Helps confirm unauthorized connections.|

---

## **🚨 Real-World Use Cases**

### **📌 Incident Response**

- Detect if an **attacker accessed external C2 servers**.
- Identify **phishing domains that a user visited**.

### **📌 Malware Analysis**

- Track **malware-generated DNS requests** (e.g., DGA-based malware).
- Correlate with **Sysmon logs (Event ID 22 - DNS Queries)**.

### **📌 Insider Threat Investigations**

- Determine if an employee accessed **restricted domains**.
- Check if **company data was exfiltrated** to cloud storage services.

---

## **🔎 Summary**

|**Category**|**Details**|
|---|---|
|**Location**|**Volatile memory** (`ipconfig /displaydns`), `Microsoft-Windows-DNS-Client/Operational.evtx`|
|**File Type**|Live Cache, Event Logs|
|**Extraction Tool**|`ipconfig`, `EvtxECmd`|
|**Key Information**|Queried domains, resolved IPs, network activity|
|**Forensic Value**|Tracks web access, malware C2 connections, phishing attempts|

---
