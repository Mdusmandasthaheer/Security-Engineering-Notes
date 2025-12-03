<!DOCTYPE html>
<html>

<body>

<h1>📁 FTP Enumeration - Quick Notes</h1>

<p>FTP is often left wide open during pentests. Port 21 is juicy because it frequently allows anonymous access or weak credentials. Here's my go-to workflow:</p>

<h2>🔍 Nmap FTP Detection (Pro/Expert)</h2>

<ul>
    <li><code>nmap -p 21 192.168.1.0/24</code> → Basic FTP port sweep</li>
    <li><code>nmap -p 21 --script ftp-anon,ftp-vuln* 192.168.1.100</code> → Check anonymous + vulns</li>
    <li><code>nmap -p 21 --script ftp-bounce 192.168.1.100</code> → FTP bounce attack detection</li>
    <li><code>nmap -sV -sC -p 21 192.168.1.100</code> → Full version + default scripts</li>
    <li><code>nmap --script ftp-brute -p 21 192.168.1.100</code> → Built-in brute force</li>
</ul>

<h2>🔓 Hydra FTP Brute Force</h2>
<img src="https://github.com/Mdusmandasthaheer/Security-Engineering-Notes/blob/76e829aca8d6123880c2d4911d18789883597dfe/Offsec%20Essentials/Files/ftp-01.png" alt="Hydra FTP Brute Force" class="ftp-img">

<pre><code>hydra -l admin -P /usr/share/wordlists/rockyou.txt ftp://192.168.1.100</code></pre>

<h2>📤 FTP Client Login</h2>
<img src="https://github.com/Mdusmandasthaheer/Security-Engineering-Notes/blob/76e829aca8d6123880c2d4911d18789883597dfe/Offsec%20Essentials/Files/ftp-02.png" alt="FTP Login Attempt" class="ftp-img">

<pre><code>ftp 192.168.1.100
# username: [found_username]
# password: [found_password]</code></pre>

<h2>✅ Successful Access</h2>
<img src="https://github.com/Mdusmandasthaheer/Security-Engineering-Notes/blob/76e829aca8d6123880c2d4911d18789883597dfe/Offsec%20Essentials/Files/ftp-03.png" alt="FTP Successful Login" class="ftp-img">
<img src="https://github.com/Mdusmandasthaheer/Security-Engineering-Notes/blob/76e829aca8d6123880c2d4911d18789883597dfe/Offsec%20Essentials/Files/ftp-04.png" alt="FTP Directory Listing" class="ftp-img">

<h2>🛠️ FTP Client Commands</h2>

<table>
    <tr><th>Command</th><th>Purpose</th><th>Example</th></tr>
    <tr><td><code>binary</code></td><td>Binary mode (for .exe, images)</td><td>Download malware without corruption</td></tr>
    <tr><td><code>put file.txt</code></td><td>Upload single file</td><td>Upload webshell.php</td></tr>
    <tr><td><code>get file.txt</code></td><td>Download single file</td><td>Grab config backups</td></tr>
    <tr><td><code>mput *.txt</code></td><td>Upload multiple files</td><td>Batch upload wordlists</td></tr>
    <tr><td><code>mget *.bak</code></td><td>Download multiple files</td><td>Exfil all backups</td></tr>
    <tr><td><code>ls</code></td><td>List directory</td><td>Recon target directory</td></tr>
    <tr><td><code>cd /var/www</code></td><td>Change directory</td><td>Navigate to webroot</td></tr>
</table>

<div class="note-box">💡 <strong>Pro Tip:</strong> Always try <code>ftp-anon</code> NSE script first - 30% of FTPs allow anonymous with write access. Instant foothold!</div>

</body>
</html>
