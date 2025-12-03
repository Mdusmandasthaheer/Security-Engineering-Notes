<!DOCTYPE html>
<html>
<body>

<h1>🔎 SNMP Enumeration Workflow</h1>
<p>SNMP (Simple Network Management Protocol) runs on UDP port 161 and is commonly used for managing networked devices. Enumeration reveals valuable system info, user lists, running services, and sometimes passwords.</p>

<h2>1️⃣ Initial Enumeration with <code>snmp-check</code></h2>
<pre><code>snmp-check 192.151.62.3</code></pre>
<p>Excellent tool for quick, human-readable SNMP data summary.</p>
<img src="https://github.com/Mdusmandasthaheer/Security-Engineering-Notes/blob/3222ae19ef71ccff5893bc62fbb9641f770a6874/Offsec%20Essentials/Files/snmp%2001.png" alt="snmp-check output" class="snmp-img">

<p class="note-box">Use this to gather system description, contact info, interfaces, and possible community strings.</p>

<h2>2️⃣ SNMP Bruteforce with Metasploit</h2>
<pre><code>msfconsole
use auxiliary/scanner/snmp/snmp_login
set RHOSTS 192.151.62.3
set COMMUNITY public
run</code></pre>
<p>Leverages a list of default or guessed community strings to find valid access.</p>
<img src="https://github.com/Mdusmandasthaheer/Security-Engineering-Notes/blob/3222ae19ef71ccff5893bc62fbb9641f770a6874/Offsec%20Essentials/Files/snmp%2002.png" alt="Metasploit SNMP brute force" class="snmp-img">

<p class="note-box">Getting a valid community string here opens doors to full SNMP enumeration capabilities.</p>

<h2>3️⃣ Detailed SNMP Enumeration via Nmap</h2>
<pre><code>sudo nmap -sU -p 161 --script=snmp-info,snmp-sysdescr,snmp-interfaces 192.151.62.3</code></pre>
<p>This uses Nmap's NSE scripts to grab system info, interfaces, and more from SNMP-enabled hosts over UDP port 161.</p>
<img src="https://github.com/Mdusmandasthaheer/Security-Engineering-Notes/blob/3222ae19ef71ccff5893bc62fbb9641f770a6874/Offsec%20Essentials/Files/snmp%2003.png" alt="Nmap SNMP Enumeration" class="snmp-img">

<h2>Additional Useful SNMP Commands</h2>
<table>
    <tr><th>Command</th><th>Description</th><th>Use Case</th></tr>
    <tr><td><code>snmpwalk -c public -v2c 192.151.62.3</code></td><td>Walk entire MIB tree</td><td>Full data dump, check for interesting info</td></tr>
    <tr><td><code>snmpget -c public -v2c 192.151.62.3 <OID></code></td><td>Query specific OID</td><td>Get exact details (e.g., sysDescr)</td></tr>
    <tr><td><code>onesixtyone -c community-list.txt 192.151.62.3</code></td><td>Community string discovery via bruteforce</td><td>Find valid community strings quickly</td></tr>
</table>

<h2>👇 How to use this info in real-world pentests or CTFs:</h2>
<ul>
    <li>Community string discovery enables you to query sensitive info like running services, OS version, and sometimes admin creds.</li>
    <li>Interface info can guide lateral movement by revealing connected devices.</li>
    <li>Legacy SNMP systems may allow write access - upload configs or commands.</li>
    <li>Use obtained info for identifying vulnerable services or crafting targeted exploits.</li>
    <li>For CTFs, SNMP data often contains hidden flags or helpful credentials.</li>
</ul>

</body>
</html>
