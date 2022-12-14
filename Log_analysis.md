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
