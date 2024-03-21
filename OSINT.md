<h2>OSINT</h2>
https://osintframework.com <br>
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
  https://www.hybrid-analysis.com/ Another sandbox to run malware
  https://www.joesecurity.org/ Another sandbox to run malware
  https://metadefender.opswat.com/ upload files, urls, IP addr, domain, hash or CVE to get info<br>
  https://www.phishtool.com/ : tool against phishing emails, reverse engineering<br>
  https://tineye.com/ : receive alerts when their images are identified on the internet, or check our images on the internet (identify phishings, fake social media, check if its a common image, brand reputation monitoring...) <br>
  https://images.google.com : similar to tineye, but from google<br>
  https://www.dehashed.com/ : user, pw, payable option refered to data leaks <br>
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
<h3>Tools</h3>
<p>
<ul><b>The Harvester</b>: Gather information about the target domain and retrieves information such as hostnames, IP addresses, employees (and their positions), email addresses, and much more<br>
  <li>theharvester -d google.com -l 100 -b google -> (tool) (target domain = google.com) (list 100 results max) (source = google) We get the IPs</li>
  <li>theharvester -d google.com -l 100 -b linkedin -> (tool) (target domain = google.com) (list 100 results max) (source = linkedin) We get employees</li>
</ul>
<ul><b>Maltego:</b>high-level data mining and information gathering tool, capable of obtaining real-time data on different types of entities (companies, people, websites, etc.)<br>
  <li>https://www.maltego.com/categories/tutorial/ documentation</li>
</ul>
<ul><b>Tweetdeck:</b> Monitor trends, follow hashtags, and perform live searches. Events in real-time, such as cyber-attacks, vulnerabilities being released, or even tracking malicious actors' activity<br>
  <li><b>“bluekeep” OR #bluekeep OR cve-2019-0708 </b>-> CVE-2019-0708, dubbed ‘BlueKeep’ was a Zero-Day vulnerability in Remote Desktop Protocol (RDP)</li>
  <li><b>#firefox OR #chrome OR #internetexplorer OR #IE</b> -> Following vulnerabilities in Firefox, Chrome, and Internet Explorer.</li>
  <li><b>#vulnerability OR #vulnerabilities OR #CVE</b> -> search term for vulnerabilities (does bring back a lot of non-security tweets due to common language).</li>
  <li><b>“Windows 10” and “vulnerability”</b> -> Monitoring for Windows 10 vulnerabilities.</li>
  <li><b>#0day OR #zeroday”</b> -> Monitoring for zero-day vulnerabilities that are publicly announced on Twitter.</li>
</ul>

</p>
<h3>Google Dorks</h3>
<p>
  <ul>
    <li>inurl: Searches for a specified text in all indexed URLs. For example, <b>inurl:hacking</b> or <b>inurl:admin</b> </li>
    <li>filetype: Searches for specified file extensions. For example, <b>filetype:pdf "hacking"</b>  </li>
    <li>site: Searches all the indexed URLs for the specified domain. For example, <b>site:tryhackme.com</b> </li>
    <ul><li>site:Facebook.com -site:www.Facebook.com -> (Look for sites that include .Facebook.com) (but NOT www.Facebook.com) Enumeration of domains, subdomains</li></ul>
    <li>cache: Get the latest cached version by the Google search engine. For example, <b>cache:tryhackme.com.</b></li>
    <li>intitle: The specified phrase MUST appear in the title of the page</li>
    <li>https://securitytrails.com/blog/google-hacking-techniques -> list of queries</li>
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

<h3>Email tools</h3>
<p>
  <ul>
    <li> https://toolbox.googleapps.com/apps/messageheader/analyzeheader -> Header analyzer</li>
    <li>https://mha.azurewebsites.net/ -> Header analyzer </li>
    <li>https://mailheader.org/ -> Header analyzer</li>
  </ul>
</p>

<h3>ANTI - OSINT</h3>
<p>
  <ul>
    <li>https://coveryourtracks.eff.org</li>
    <li>https://browserleaks.com</li>
    <ul> <b>Extensions for browser</b>
      <li>User-Agent Switcher and Manager: “spoof your browser “user-agent” string to a custom designation.”</li>
      <li>No Script: “Allows JavaScript, Java, Flash, and other plugins to be executed only by trusted web sites of your choice”</li>
      <li>Privacy Badger: “Stops advertisers and other third-party trackers from secretly tracking where you go and what pages you look at on the web”</li>
      <li>Ublock Origin: “Filters requests to display adverts and prevents your browser from retrieving and displaying marketing content.”</li>
      <li>Cookie AutoDelete: “Automatically delete unwanted cookies from your closed tabs while keeping the ones you want.”</li>
    </ul>
    <ul><b>SOCK PUPPETS</b>
      <li>“Welcome to the (Sock) Jungle”: https://youtu.be/v8EP6xOcB8M</li>
      <li>“The Art of The Sock”: https://www.secjuice.com/the-art-of-the-sock-osint-humint/</li>
      <li>“Creating an Effective Sock Puppet for OSINT Investigations”: https://web.archive.org/web/20210125191016/https://jakecreps.com/2018/11/02/sock-puppets/</li>
      <li>“Sock puppet Account Creation – My Process”: https://garrettmickley.com/sockpuppet-account-creation/</li>
      <li>“The World’s Best Sock Puppet…Not!”: https://keyfindings.blog/2019/01/21/the-worlds-best-sock-puppet-not/</li>
    </ul>
  </ul>
</p>
