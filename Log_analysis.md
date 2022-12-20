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
  grep ".*\.zip$" : to look for a file, in this case, zip<br>
  grep -e [a-z] : to match any lowercase letter in the English alphabet, the "-" is for a range,  can pñay with this:<br>
  <ul>
    <li>[aeiou] for only vowels, the order doesn't matter</li>
    <li>[a-zA-Z] matchs any character</li>
    <li>[a-z0-9] maths any lowercase alphanumeric character</li>
  </ul>
</p>
<h3>Regex</h3>
