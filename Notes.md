<h1>Notes</h1>
<h2>OSINT</h2>
<h3>Google Dorks</h3>
<p>
  <ul>
    <li>inurl: Searches for a specified text in all indexed URLs. For example, <b>inurl:hacking</b> </li>
    <li>filetype: Searches for specified file extensions. For example, <b>filetype:pdf "hacking"</b>  </li>
    <li>site: Searches all the indexed URLs for the specified domain. For example, <b>site:tryhackme.com</b> </li>
    <li>cache: Get the latest cached version by the Google search engine. For example, <b>cache:tryhackme.com.</b></li>
    <li>intitle: The specified phrase MUST appear in the title of the page</li>
  </ul>
  Robots.txt: public file that allows or disallows crawlers, indexers.
</p>
<h3>Sites</h3>
<p>
  https://who.is/ : domain information such as registrant, administrative, billing and technical contacts in a centralised database <br>
  https://haveibeenpwned.com/ : Check public data breaches for <b>emails or phones</b> <br>
  https://github.com/ : code repository <br>
  https://www.shodan.io/ : Search engine related to TheHarvester info, domains, ips, and others. <br>
  https://emailrep.io/ to check reputation of the sender <br>
  https://www.virustotal.com/gui/home/upload  A service that provides a cloud-based detection toolset and sandbox environment.<br>
  https://labs.inquest.net/ A service provides network and file analysis by using threat analytics. <br>
  https://ipinfo.io/ A service that provides detailed information about an IP address by focusing on geolocation data and service provider.<br>
  https://www.talosintelligence.com/ An IP reputation check service is provided by Cisco Talos. <br>
  https://urlscan.io/ A service that analyses websites by simulating regular user behaviour.<br>
  https://www.browserling.com/ A browser sandbox is used to test suspicious/malicious links. <br>
  https://www.wannabrowser.net/ A browser sandbox is used to test suspicious/malicious links.<br>
  https://any.run/ Sandbox to run any phishing link
</p>
<h2>Log Analysis</h2>
Where to find?
<ul>
  <li>Windows - Event Viewer</li>
  <li>Linux - /var/log</li>
  <ul>
    <li><i>auth.log, dpkg.log, syslog, kern.log</i></li>
  </ul>
</ul>
<h3>Grep</h3>
<p>
  -i : insensitive search<br>
  -E : regular expressions (regex) <br>
  -r : recursive, you can use a directory <br>
  grep ".*\.zip$" : to look for a file, in this case, zip
</p>
<h2>Scanning Tools</h2>
<h3>Nmap</h3>
<p>
  nmap -sS MACHINE_IP : TCP SYN Scan; Get the list without completing the TCP three-way handshake and making the scan a little stealthier<br>
  nmap -sn MACHINE_IP : Ping Scan; Allows scanning without going deeper and checking for ports services etc <br>
  nmap -O MACHINE_IP : OS Scan; type of OS running <br>
  nmap -sV MACHINE_IP : Service Scan; Detecting Services. <br>
</p>
<h3>Nikto</h3>
Nikto is open-source software that allows scanning websites for vulnerabilities. It enables looking for subdomains, outdated servers, debug messages etc., on a website<br>
Can be used in terminal:<br>
nikto -host MACHINE_IP:port (or without port)<br>
<h2>Brute Force</h2>
<ul>Remote access protocols related:
  <li>SSH: Secure Shell. Remote login. It provides the user with a command-line interface (CLI) that can be used to execute commands.</li>
  <li>RDP: Remote Desktop Protocol; it is also known as Remote Desktop Connection (RDC) or simply Remote Desktop (RD). It provides a graphical user interface (GUI) to access an MS Windows system.</li>
  <li>VNC: Virtual Network Computing. It provides access to a graphical interface which allows the user to view the desktop and (optionally) control the mouse and keyboard. VNC is available for <b>any system</b> with a graphical interface, including MS Windows, Linux, and even macOS, Android and Raspberry Pi.</li>
</ul>
<h3>Hydra</h3>
<p>
  Standard format: <b>hydra -l username -P wordlist.txt server service -V</b>
  <ul>
    <li><b>-l username:</b> -l should precede the username, you should omit this option if the service does not use a username.</li>
    <li><b>-P wordlist.txt:</b> file or path to the list of passwords you want to try with the provided username. (Rockyou.txt)</li>
    <li><b>server</b> is the hostname or IP address of the target server.</li>
    <li><b>service</b> indicates the service in which you are trying to launch the dictionary attack. Such as <b>rdp, vnc, ftp, pop3 or any other protocol</b> supported by Hydra.</li>
    <li>Exemple: hydra -l mark -P /usr/share/wordlists/rockyou.txt MACHINE_IP ssh   or   hydra -l mark -P /usr/share/wordlists/rockyou.txt ssh://MACHINE_IP</li>
  </ul>
  Options you can use:
  <ul>
  <li>-V or -vV, for verbose, makes Hydra show the username and password combinations being tried.</li>
  <li>-d, for debugging, provides more detailed information about what’s happening. The debugging output can save you much frustration; for instance, if Hydra tries to connect to a closed port and timing out, -d will reveal this immediately.</li>
  </ul>
</p>
<h2>Email analysis</h2>
<h3>emlAnalyzer</h3>
<p>
  Terminal tool to check emails<br>
  <ul> Options
    <li>-i /path-to-file/filename , file to analyse</li>
    <li>--header , show header</li>
    <li>-u , Show URLs</li>
    <li>--text , Show cleartext data</li>
    <li>--extract-all , Extract all attachments</li>
    <li>Exemple: <i>emlAnalyzer -i /path/file --header -u --text --extract-all<i></li>
  </ul>
</p>
<h2>Decoding</h2>
https://gchq.github.io/CyberChef/ best website to decode text with different decode options.












