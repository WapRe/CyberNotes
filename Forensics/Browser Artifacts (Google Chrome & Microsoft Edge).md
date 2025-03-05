## ✅ **What are Browser Artifacts?**

Browser artifacts contain **user activity data** from web browsing sessions, including:

- **Visited websites (browsing history).**
- **Stored cookies (session authentication tokens, tracking data).**
- **Cache files (locally stored web content, scripts, and images).**
- **Download history (file names, URLs, and timestamps).**
- **Autofill data (saved logins, form inputs, and payment details).**

Forensically, **browser artifacts are critical** because:

- They **track user activity**, even if history is cleared (**some remnants may persist**).
- **Session cookies may contain active authentication tokens**.
- **Download records reveal what files were obtained from the web**.

> **⚠️ Limitations:**
> 
> - **Incognito Mode** reduces stored artifacts (but DNS and prefetch artifacts remain).
> - **Cloud syncing (Google Sync, Microsoft Sync)** may remove or modify local traces.
> - **Encryption in some files (e.g., Chrome passwords)** requires user credentials to decrypt.

---

## **📍 Where to Find Chrome Artifacts?**

Google Chrome stores browsing artifacts in **SQLite databases and cache folders**:

|**Artifact**|**Location**|**Format**|
|---|---|---|
|**Browsing History**|`C:\Users\%USERNAME%\AppData\Local\Google\Chrome\User Data\Default\History`|SQLite (`History`)|
|**Cookies**|`C:\Users\%USERNAME%\AppData\Local\Google\Chrome\User Data\Default\Cookies`|SQLite (`Cookies`)|
|**Cache**|`C:\Users\%USERNAME%\AppData\Local\Google\Chrome\User Data\Default\Cache\`|Cached web files|
|**Downloads**|`C:\Users\%USERNAME%\AppData\Local\Google\Chrome\User Data\Default\History`|SQLite (`downloads`)|
|**Autofill & Logins**|`C:\Users\%USERNAME%\AppData\Local\Google\Chrome\User Data\Default\Web Data`|SQLite (`autofill`, encrypted passwords)|

### **Google Chrome Forensic Considerations**

- **Cookies can be used to hijack active sessions** (if not expired).
- **DNS Cache and Prefetch** may store evidence of visited sites, even if browser history is cleared.
- **Deleted downloads can sometimes be recovered from the MFT ($MFT)**.

---

## **📍 Where to Find Microsoft Edge Artifacts?**

Edge (Chromium-based) follows **the same structure** as Chrome but stores its artifacts in a different location:

|**Artifact**|**Location**|**Format**|
|---|---|---|
|**Browsing History**|`C:\Users\%USERNAME%\AppData\Local\Microsoft\Edge\User Data\Default\History`|SQLite (`History`)|
|**Cookies**|`C:\Users\%USERNAME%\AppData\Local\Microsoft\Edge\User Data\Default\Cookies`|SQLite (`Cookies`)|
|**Cache**|`C:\Users\%USERNAME%\AppData\Local\Microsoft\Edge\User Data\Default\Cache\`|Cached web files|
|**Downloads**|`C:\Users\%USERNAME%\AppData\Local\Microsoft\Edge\User Data\Default\History`|SQLite (`downloads`)|
|**Autofill & Logins**|`C:\Users\%USERNAME%\AppData\Local\Microsoft\Edge\User Data\Default\Web Data`|SQLite (`autofill`, encrypted passwords)|

### **Microsoft Edge Forensic Considerations**

- **Edge uses the same SQLite structure as Chrome**, making forensic analysis identical.
- **Microsoft account syncing** may cause artifacts to be stored remotely.
- **Some cached pages remain even after history is deleted**.

---

## **🛠️ How to Extract Chrome & Edge Artifacts (Step by Step)**

We will use **DB Browser for SQLite** for local database analysis and **BrowsingHistoryView** for bulk extraction.

### **Method 1: Manual Extraction**

1. **Copy Browser Database Files**
    
    - Navigate to:
        - **Chrome**: `C:\Users\%USERNAME%\AppData\Local\Google\Chrome\User Data\Default\`
        - **Edge**: `C:\Users\%USERNAME%\AppData\Local\Microsoft\Edge\User Data\Default\`
    - Copy **History, Cookies, Web Data, Downloads** files to a forensic workstation.
2. **Use SQLite to Open the Databases**
    
    - Install **DB Browser for SQLite**.
    - Open the copied database files.
    - Run queries like:
        
        ```sql
        SELECT url, title, visit_count, last_visit_time FROM urls ORDER BY last_visit_time DESC;
        ```
        
    - This retrieves **browsing history with timestamps**.

---

### **Method 2: Automated Extraction with BrowsingHistoryView**

#### **1️⃣ Download BrowsingHistoryView**

- Get it from **[NirSoft BrowsingHistoryView](https://www.nirsoft.net/utils/browsing_history_view.html)**.
- Extract the tool to a working directory.

#### **2️⃣ Run BrowsingHistoryView**

Navigate to the tool’s folder and run:

```cmd
BrowsingHistoryView.exe /scomma C:\ExtractedResults\browsing_history.csv
```

- This extracts **history from all installed browsers**.

#### **3️⃣ Review Extracted Data**

- Open `browsing_history.csv` in **Excel**.
- Look for:
    - **Suspicious domains** visited.
    - **Repeated logins to sensitive sites**.
    - **File downloads from malicious sources**.

---

## **🔎 How to Recover Deleted Browser History**

Even if history has been deleted within the browser, **some traces may still exist** in other system artifacts:

|**Method**|**Description**|
|---|---|
|**MFT Analysis**|If history files were deleted, file system logs (MFT, USN Journal) may contain references to them.|
|**DNS Cache**|Run `ipconfig /displaydns` to see recent domain name resolutions.|
|**Windows Search Index**|Check `Windows.edb` for indexed URLs.|
|**Event Logs**|Check `Microsoft-Windows-WebServices/Operational.evtx` for browser activity.|
|**Network Captures**|If a packet capture tool (e.g., Wireshark) was running, HTTP requests may be available.|
|**Registry Artifacts**|`TypedURLs` in `HKCU\Software\Microsoft\Internet Explorer\TypedURLs` may store URLs typed into the address bar.|

---

## **📊 How to Analyze Browser Artifacts (Step by Step)**

|**Step**|**Action**|**Details**|
|---|---|---|
|**1. Open Extracted Databases**|Use DB Browser for SQLite|Displays raw browsing data.|
|**2. Identify Suspicious URLs**|Look at `url` and `visit_count`|Shows frequently visited sites.|
|**3. Check for Downloads**|Query `downloads` table|Reveals what files were obtained from the web.|
|**4. Extract Authentication Tokens**|Query `cookies` table|May contain active session data.|
|**5. Review Autofill & Saved Passwords**|Query `formhistory.sqlite`|May reveal stored credentials.|
|**6. Correlate with Other Artifacts**|Compare with DNS Cache and Event Logs|Helps confirm browsing activity.|

---

## **🚨 Real-World Use Cases**

### **📌 Incident Response**

- Identify **phishing sites accessed** before an attack.
- Detect **compromised credentials stored in autofill**.

### **📌 Malware Analysis**

- Track **downloads of malicious files**.
- Extract **session cookies used in active attacks**.

### **📌 Insider Threat Investigations**

- Verify if an employee accessed **restricted sites**.
- Retrieve **deleted browsing history** that still exists in cache.

---

## **🔎 Summary**

|**Category**|**Details**|
|---|---|
|**Location**|`AppData\Local\Google\Chrome\User Data\Default\`, `AppData\Local\Microsoft\Edge\User Data\Default\`|
|**File Type**|SQLite Databases|
|**Extraction Tool**|`DB Browser for SQLite`, `BrowsingHistoryView`|
|**Key Information**|Browsing history, downloads, cookies, cached web content|
|**Forensic Value**|Tracks user web activity, credentials, and downloaded files|

---
