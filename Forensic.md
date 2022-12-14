<h2>Memory Forensics</h2>
<h3>Volatility 3</h3>
<p>
<b>Info:</b>Volatility is an open-source memory forensics toolkit written in Python. Volatility allows us to analyse memory dumps taken from Windows, Linux and Mac OS devices and is an extremely popular tool in memory forensics. For example, Volatility allows us to:<br>
<ul>
  <li>List all processes that were running on the device at the time of the capture</li>
  <li>List active and closed network connections</li>
  <li>Use Yara rules to search for indicators of malware</li>
  <li>Retrieve hashed passwords, clipboard contents, and contents of the command prompt</li>
  <li>REQUIERED PYTHON INSTALLED</li>
</ul>
<b>Comands:</b><br>
<ul>
  <li>python 3 vol.py : runs volatility framework with a help menu</li>
  <li>-f : where you provide the name and location of the memory dump that you wish to analyse.</li>
    <ul><li><i>python3 vol.py -f /path/to/my/memorydump.vmem</i></li></ul>
  <li>-v : verbose option to see what is going on</li>
  <li>-p : override the default location of where plugins are stored </li>
    <ul><li><i>python3 vol.py -p /path/to/my/custom/plugins</i></li></ul>
  <li>-o : specify where extracted processes or DLLs are stored</li>
    <ul><li><i>python3 vol.py -o /output/extracted/files/here</i></li></ul>
</ul>
<b>Usefull exemples with Windows Pluggins:</b>
<ul>
  <li>python3 vol.py -f path/or/file windows.info : check the OS of</li>
  <li>python3 vol.py -f path/or/file windows.pslist : what processes were running on the system.</li>
  <li>python3 vol.py -f path/or/file windows.psscan : what a specific process was actually doing.</li>
  <li>python3 vol.py -f path/or/file windows.dumpfiles --pid**** : export a specific binary that allows us further to analyse it through static or dynamic analysis, adding the Id of the binary to be effective</li>
  <li>python3 vol.py -f path/or/file windows.netstat : lists all network connections at the time of the capture.</li>
</ul>
<b><i>All windows pluggin List: https://volatility3.readthedocs.io/en/stable/volatility3.plugins.windows.html</i></b><br>
</p>
