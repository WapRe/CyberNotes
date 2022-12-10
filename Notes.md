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
  https://any.run/ Sandbox to run any phishing link<br>
  https://metadefender.opswat.com/ upload files, urls, IP addr, domain, hash or CVE to get info
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
  nmap -T4 -A -Pn MACHINE_IP : T4 is the speed of the scan, -Pn to treat all host online only<br>
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
    <li>Exemple: <i>emlAnalyzer -i /path/file --header -u --text --extract-all</i></li>
  </ul>
</p>
<h2>Decoding</h2>
<p>
  https://gchq.github.io/CyberChef/ best website to decode text with different decode options.
</p>
<h2>Docker</h2>
<p>
  /.dockerenv : in the root directory to check if there is any in the machine
</p>
<h2>Metasploit</h2>
<p>
  <h3>General commands:</h3>
  <ul>
    <li>msfconsole : starts the metasploit console</li>
    <li>search : to look for modules</li>
    <li>use : command to load modules</li>
    <ul><li>Exemple: use path/to/module</li></ul>
    <li>exploit(path/to/exploit/or/module) > info : to view information about, including options, description or CVE details...</li>
  </ul>
  <h3>After using a module, in the module:</h3>
  <ul>
    <li>show options : to view available options</li>
    <li>set rhost MACHINE_IP : set the target host</li>
    <li>set verbose true : logging to the target host</li>
    <li>set lhost LISTEN_IP : Set the payload listening address; this is the IP address of the host running Metasploit</li>
    <li>check : check the module</li>
    <li>run : run the module</li>
  </ul>
  <h3>Common Metasploit console commands for viewing and manipulating sessions</h3>
  <ul>
    <li>sessions; view sessions</li>
    <li>sessions -u -1: upgrade the last opened session to Meterpreter</li>
    <li>sessions -i session_id: interact with a session</li>
    <li>background: Background the currently interactive session, and go back to Metasploit</li>
  </ul>
  <h3>Meterpreter commands (advanced payload that provides interactive access to a compromised system. Meterpreter supports running commands on a remote target, including uploading/downloading files and pivoting.)</h3>
  <ul>
    <li>sysinfo: Get information about the remote system, such as OS</li>
    <li>upload local_file.txt: Upload a file or directory</li>
    <li>ipconfig: Display interfaces</li>
    <li>resolve remote_service1 remote_service2 : Resolve a set of host names on the target to IP address (PIVOTING)</li>
    <li>route : can be used to modify the internal routing table in order to PIVOT, determines where to send traffic</li>
  <ul><li>Exemple: route [add/remove] subnet netmask [comm/sid]</li></ul>
  <ul><li>route add 172.17.0.1/32 -1: Configure the routing table to send packets destined for 172.17.0.1 to the latest opened session</li></ul>
  <ul><li>route add 172.28.10.48/29 -1: Configure the routing table to send packets destined for 172.28.101.48/29 subnet to the latest opened session</li></ul>
  <ul><li>route print : Output the routing table</li></ul>
  </ul>
  <h3>Socks_Proxy</h3>
  A socks proxy is an intermediate server that supports relaying networking traffic between two machines. This tool allows you to implement the technique of pivoting. You can run a socks proxy either locally on a pentester’s machine via Metasploit, or directly on the compromised server. In Metasploit, this can be achieved with the auxiliary/server/socks_proxy module<br>
  <ul>
    <li>use auxiliary/server/socks_proxy</li>
    <li>run srvhost=127.0.0.1 srvport=9050 version=4a</li>
  </ul>
  Tools such as curl support sending requests through a socks proxy server via the --proxy flag<br>
  <ul><li>curl --proxy socks4a://localhost:9050 http://MACHINE_IP</li></ul>
  If "curl" does not natively support an option for using a socks proxy, ProxyChains can intercept the tool’s request to open new network connections and route the request through a socks proxy instead. For instance, an example with Nmap:<br>
  <ul><li>proxychains -q nmap -n -sT -Pn -p 22,80,443,5432 MACHINE_IP</li></ul>
</p>









