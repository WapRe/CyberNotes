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
