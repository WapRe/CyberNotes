<h2>OSINT</h2>
<h3>Sites</h3>
<p>
  https://who.is/ : domain information such as registrant, administrative, billing and technical contacts in a centralised database <br>
  https://haveibeenpwned.com/ : Check public data breaches for <b>emails or phones</b> <br>
  https://github.com/ : code repository <br>
  https://www.shodan.io/ : Search engine related to TheHarvester info, domains, ips, and others. Indexes all the internet and post the services related, very useful for IoT.<br>
  https://emailrep.io/ to check reputation of the sender <br>
  https://www.virustotal.com/gui/home/upload  A service that provides a cloud-based detection toolset and sandbox environment.<br>
  https://labs.inquest.net/ A service provides network and file analysis by using threat analytics. <br>
  https://ipinfo.io/ A service that provides detailed information about an IP address by focusing on geolocation data and service provider.<br>
  https://www.talosintelligence.com/ An IP reputation check service is provided by Cisco Talos. <br>
  https://urlscan.io/ A service that analyses websites by simulating regular user behaviour. Automate the process of browsing and crawling through websites to record activities and interactions. The information recorded includes the domains and IP addresses contacted, resources requested from the domains, a snapshot of the web page, technologies utilised and other metadata about the website.<br>
  https://www.browserling.com/ A browser sandbox is used to test suspicious/malicious links. <br>
  https://www.wannabrowser.net/ A browser sandbox is used to test suspicious/malicious links.<br>
  https://any.run/ Sandbox to run any phishing link, gather info about ASN, IP, Domains, and other. Gather info about all connections related.<br>
  https://metadefender.opswat.com/ upload files, urls, IP addr, domain, hash or CVE to get info<br>
  https://www.phishtool.com/ : tool against phishing emails, reverse engineering<br>
</p>
<h3>Other Interesting sites</h3>
<p>
  https://gchq.github.io/CyberChef/ best website to decode text with different decode options.<br>
  https://remix.ethereum.org/ : Tool to compile files. Safe and controlled test environment for smart contracts as if they were in the public blockchain.<br>
  https://www.rapidtables.com/convert/number/hex-to-decimal.html : Convertor decimal/hex<br>
  https://tdm.socprime.com/login : security professionals share their detection rules for different kinds of threats including the latest CVE's that are being exploited in the wild by adversaries.<br>
  https://abuse.ch/ : Developed to identify and track malware and botnets through several operational platforms developed under the project.<br>
<ul>
  <li>https://bazaar.abuse.ch/ : project to collect and share malware samples.</li>
  <li>Other projects: https://abuse.ch/#platforms
    <ul>
      <li>Malware Bazaar:  A resource for sharing malware samples.</li>   
      <li>Feodo Tracker:  A resource used to track botnet command and control (C2) infrastructure linked with Emotet, Dridex and TrickBot.</li>
      <li>SSL Blacklist:  A resource for collecting and providing a blocklist for malicious SSL certificates and JA3/JA3s fingerprints.</li>
      <li>URL Haus:  A resource for sharing malware distribution sites.</li>
      <li>Threat Fox:  A resource for sharing indicators of compromise (IOCs).</li>
    </ul>
</ul>
  https://www.mandiant.com/resources/insights/apt-groups : info about differents apt groups.<br>
</p>
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
<h3>Shodan Dorks:</h3>
<p>
<ul>
  <li>ASN:[number] : filter for ASN<br></li>
  <li>product:[MySQL] : filter with products</li>
  <li>vuln:ms17-010 : search for vulnerabilities (only academic or enterprise mode) </li>
  <li>vuln:CVE-2014-0160 : we can use different CVE too</li>
  <li>City Country Geo : we can look for cities or countries</li>
  <li>Hostname net : based on IP / CIDR</li>
  <li>os [system] : fins by Operating System</li>
  <li>port before/after : we can add timeframes too</li>
  <li>has_screenshot:true encrypted attention -> we can see different Ips with a ransomware login page</li>
  <li>screenshot.label:ics : ICS/SCADA pages or some webcams.</li>
  <li>https://github.com/jakejarvis/awesome-shodan-queries  :  There are more on github</li>
</ul>
</p>
<h3>Intelligence cycle</h3>
<p>
  <ul>
    <li>https://www.intelligencecareers.gov/icintelligence.html</li>
    <li>https://www.sciencedirect.com/topics/computer-science/intelligence-cycle</li>
    <li>https://www.e-education.psu.edu/sgam/node/15</li>
    <li>https://www.groupsense.io/resources/how-to-use-the-intelligence-cycle-to-secure-your-brand</li>
    <li>TL OSINT VM: https://www.tracelabs.org/initiatives/osint-vm</li>
    <li>DIY OSINT VM Guide: https://nixintel.info/tag/diy-buscador/</li>
  </ul>
</p>

<h3>Check your browser fingerprinting</h3>
<p>
  <ul>
    <li>https://coveryourtracks.eff.org</li>
    <li>https://browserleaks.com</li>
  </ul>
</p>
