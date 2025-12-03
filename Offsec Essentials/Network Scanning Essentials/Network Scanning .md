<!DOCTYPE html>
<html>
<head>
    <title>Nmap Network Scanning Guide</title>
    
</head>
<body>

<h1>🔍 Nmap Network Scanning Essentials</h1>
<p><strong>Network scanning</strong> is the first step in any pentest—discover live hosts, open ports, services, and OS versions to map your attack surface. Nmap is the gold standard.</p>

<img src="https://github.com/Mdusmandasthaheer/Security-Engineering-Notes/blob/2c73057f044ed7427257c79cf905539ec7374be9/Offsec%20Essentials/Files/Screenshot-01.png" alt="Nmap Scan Output Example" class="scan-img">

<h2>🎯 Host Discovery (Find Live Targets)</h2>
<p>Quickly identify which IPs are alive before deep scanning. Skip dead hosts to save time.</p>

<table>
    <tr><th>Scan Type</th><th>Command</th><th>When to Use</th></tr>
    <tr><td>ICMP Echo</td><td><code>sudo nmap -PE -sn 192.168.1.0/24</code></td><td>Standard ping sweep</td></tr>
    <tr><td>TCP ACK</td><td><code>sudo nmap -PA -sn 192.168.1.0/24</code></td><td>Firewall bypass (port 80/443)</td></tr>
    <tr><td>ARP Scan</td><td><code>sudo arp-scan -I eth0 192.168.1.0/24</code></td><td>Local network (fastest)</td></tr>
</table>

<div class="example"><strong>💥 Field Tip:</strong> <code>sudo nmap -sn 10.0.0.0/24 | grep "Nmap scan report" | cut -d' ' -f5 > live_hosts.txt</code> → Extract IPs to file instantly.</div>

<h2>🔓 Open Port & Service Scanning</h2>
<p>Find attack vectors—web servers, SSH, databases, anything exploitable.</p>

<table>
    <tr><th>Scan Type</th><th>Command</th><th>Scenario</th></tr>
    <tr><td>Full Aggro</td><td><code>sudo nmap -A -sV -sC -v -T4 192.168.1.123</code></td><td>Deep service/OS detection + scripts</td></tr>
    <tr><td>All Ports</td><td><code>sudo nmap -sC -p- -A -Pn 192.168.1.112 -T4 --min-rate 1000</code></td><td>65k ports + NSE scripts (no ping)</td></tr>
    <tr><td>Stealth TCP</td><td><code>sudo nmap -sS -p- -T4 --min-rate 5000 192.168.1.100</code></td><td>SYN scan all ports, high speed</td></tr>
    <tr><td>UDP Blast</td><td><code>sudo nmap -sU --top-ports 100 -T4 -Pn 192.168.1.120</code></td><td>Common UDP services</td></tr>
    <tr><td>Packet Trace</td><td><code>sudo nmap -p- -sV -Pn -n --disable-arp-ping --packet-trace 192.168.1.12</code></td><td>Debug what's happening</td></tr>
</table>

<h2>🕵️ Stealth & Evasion Scans</h2>
<p>Bypass firewalls and IDS without getting blocked.</p>

<table>
    <tr><th>Technique</th><th>Command</th><th>Effect</th></tr>
    <tr><td>Null Scan</td><td><code>sudo nmap -sN 192.168.1.10</code></td><td>No flags set (stealthy)</td></tr>
    <tr><td>TCP Connect</td><td><code>sudo nmap -PU 192.168.1.10</code></td><td>Both TCP+UDP quick scan</td></tr>
    <tr><td>Idle Zombie</td><td><code>sudo nmap -sS -f --scan-delay 1s 192.168.1.10</code></td><td>Fragment + slow timing</td></tr>
    <tr><td>Source Port</td><td><code>sudo nmap -sS --source-port 53 192.168.1.10</code></td><td>DNS port bypass</td></tr>
</table>

<div class="warning"><strong>⚠️ Pro Timing:</strong> <code>--scan-delay 10ms --data-length 16</code> → Custom packet timing to evade IDS rate limiting.</div>

<h2>🎭 Specialized Scans</h2>

<h3>SMB Enumeration</h3>
<pre><code>sudo nmap -p445 --script smb* -v 192.168.1.123
sudo nmap -sV -A -p445 --script smb-enum* 192.168.1.123</code></pre>
<div class="scenario"><em>🔥 SMB Goldmine: <code>nmap -p445 --script smb-vuln* 192.168.1.0/24</code> → EternalBlue, MS17-010, shares in seconds.</em></div>

<h3>Port 443 Deep Dive</h3>
<pre><code>sudo nmap -p443 -sV --version-intensity 9 -T4 --script ssl* 192.168.1.120</code></pre>

<h2>⚔️ Scan Matrix</h2>
<table>
    <tr><th>Phase</th><th>Command</th><th>Time</th><th>Risk</th></tr>
    <tr><td>Host Discovery</td><td><code>-sn</code></td><td>30s</td><td>Low</td></tr>
    <tr><td>Top 1000 Ports</td><td><code>-F -sV</code></td><td>2min</td><td>Medium</td></tr>
    <tr><td>Full Port Sweep</td><td><code>-p- -sV -Pn</code></td><td>15min</td><td>High</td></tr>
    <tr><td>NSE Vulns</td><td><code>-sC -A</code></td><td>5-30min</td><td>Very High</td></tr>
</table>

<div class="scenario"><em>💥 <strong>Real Pentest Flow:</strong> 1) <code>nmap -sn 192.168.1.0/24</code> → 2) <code>nmap -sC -sV -T4 live_hosts</code> → 3) Attack open ports. 90% of footholds found here.</em></div>

</body>
</html>
