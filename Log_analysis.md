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
    <li>[a-z0-9] matchs any lowercase alphanumeric character</li>
    <li>[a-zA-Z0-9]+ matchs a string that is alphanumeric and case insensitive, plus operator means that we want to match a string, and we don't care how long it is, as long as it's composed of letters and numbers</li>
    <li>^[a-zA-Z]+[0-9]*$ matchs first part of the string is composed of letters and we want it to match regardless if there are numbers thereafter.</li>
    <li>^[a-z]{3,9}$ matchs just lowercase letters that are in between 3 and 9 characters in length</li>
    <li>^[a-zA-Z]{3}.{3}$ matchs a string that starts with 3 letters followed by any 3 characters</li>
  </ul>
  grep -e ^(www\.)?tryhackme\.com$ : match both www.tryhackme.com and tryhackme.com, would also avoid matching .tryhackme.com.<br>
  <ul><li>^(www\.)?: The ^ operator marks the start of the string, followed by the grouping of www and the escaped ., and immediately followed by the question mark operator</li></ul>
  <ul><li>tryhackme\.com$: The $ operator marks the end of the string, preceded by the string tryhackme, an escaped ., and the string com. If we don't escape the . operator, the regex engine will think that we want to match any character between tryhackme and com as well.</li></ul>
</p>
<h3>Regex</h3>
<p>
  " . " : Wildcard operator, match any character<br>
  " * " : Star operator, used if u don't care if the preceding token matches anything or no<br>
  " + " : Plus operator, used if you want to make sure that it matches at least once<br>
  " {} " : Curly braces operator, specifies the number of characters you want to match, {min,max}, specifies how many times the preceding token can be repeated<br>
  " ^ " and " $ " operators are called anchors, denote the start and end of the string we want to match, respectively<br>
  " () " and the" \ " operators, grouping and escaping respectively. Grouping is done to manage the matching of specific parts of the regex better while escaping is used so we can match strings that contain regex operators<br>
  " ? " operator, used to denote that the preceding token is optional<br>  
</p>
