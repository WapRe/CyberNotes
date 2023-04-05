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
<br>
<h2>Networking</h2>
Basic IP address check:<br>
<b>ip a s eth0</b><br>
With this command it shows directly the IP of the device.<br>
We can change eth0 by wlan0 or others.<br>
<b>ip a s ens33</b> in case you are in a Ubuntu system.<br>
