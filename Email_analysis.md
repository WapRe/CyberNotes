<h1>Info to check basics in email analysis</h1>
<h2>Headers</h2>
<p>
  Information about sections:
  <table class="default">
    <tr>
      <th>Field</th>
      <th>Details</th>
    </tr>
    <tr>
      <td><b>From</b></td>
      <td>Sender's Address</td>
    </tr>
     <tr>
      <td><b>To</b></td>
      <td>Receiver's Address, including CC and BCC</td>
    </tr>
     <tr>
      <td><b>Date</b></td>
      <td>Timestamp when the email was Sent</td>
    </tr>
     <tr>
      <td><b>Subject</b></td>
      <td>Subject of the email</td>
    </tr>
     <tr>
      <td><b>Return Path</b></td>
      <td>The return address of the reply, a.k.a. "Reply-To". If you reply to an email, the reply will go to the address mentioned in this field.</td>
    </tr>
     <tr>
      <td><b>Domain Key and DKIM Signatures</b></td>
      <td>Email signatures are provided by email services to identify and authenticate emails.</td>
    </tr>
     <tr>
      <td><b>SPF</b></td>
      <td>Shows the server that was used to send the email. It will help to understand if the actual server is used to send the email from a specific domain.</td>
    </tr>
     <tr>
      <td><b>Message-ID</b></td>
      <td>Unique ID of the email.</td>
    </tr>
     <tr>
      <td><b>MIME-Version</b></td>
      <td>Used MIME version. It will help to understand the delivered "non-text" contents and attachments.</td>
    </tr>
     <tr>
      <td><b>X-Headers</b></td>
      <td>The receiver mail providers usually add these fields. Provided info is usually experimental and can be different according to the mail provider.</td>
    </tr>
     <tr>
      <td><b>X-Received</b></td>
      <td>Mail servers that the email went through.</td>
    </tr>
     <tr>
      <td><b>X-Spam Status</b></td>
      <td>Spam score of the email.</td>
    </tr>
     <tr>
      <td><b>X-Mailer</b></td>
      <td>Email client name.</td>
    </tr>
  </table>
  Quick analysis Quick Questions:
  <table class="default">
    <tr>
      <td>Questions to Ask / Required Checks </td>
      <th>Evaluation</th>
    </tr>
     <tr>
      <td>Do the "From", "To", and "CC" fields contain valid addresses?</td>
      <th>Having invalid addresses is a red flag.</th>
    </tr>
     <tr>
      <td>Are the "From" and "To" fields the same?</td>
      <th>Having the same sender and recipient is a red flag.</th>
    </tr>
     <tr>
      <td>Are the "From" and "Return-Path" fields the same?</td>
      <th>Having different values in these sections is a red flag.</th>
    </tr>
     <tr>
      <td>Was the email sent from the correct server?</td>
      <th>Email should have come from the official mail servers of the sender.</th>
    </tr>
     <tr>
      <td>Does the "Message-ID" field exist, and is it valid?</td>
      <th>Empty and malformed values are red flags.</th>
    </tr>
     <tr>
      <td>Do the hyperlinks redirect to suspicious/abnormal sites?</td>
      <th>Suspicious links and redirections are red flags.</th>
    </tr>
     <tr>
      <td>Do the attachments consist of or contain malware?</td>
      <th>Suspicious attachments are a red flag. File hashes marked as suspicious/malicious by sandboxes are a red flag.</th>
    </tr>
  </table>
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
