<!DOCTYPE html>
<html>
<head>
    <title>Nmap Network Scanning Guide</title>
    <style>
        body { font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif; max-width: 900px; margin: 0 auto; padding: 30px 20px; line-height: 1.7; color: #333; }
        h1 { color: #1a1a1a; border-bottom: 3px solid #e74c3c; padding-bottom: 15px; font-size: 2.2em; }
        h2 { color: #2c3e50; margin-top: 40px; }
        h3 { color: #34495e; margin-top: 25px; }
        table { border-collapse: collapse; width: 100%; margin: 20px 0; box-shadow: 0 2px 8px rgba(0,0,0,0.1); }
        th, td { border: 1px solid #e0e0e0; padding: 14px 12px; text-align: left; }
        th { background: linear-gradient(135deg, #e74c3c 0%, #c0392b 100%); color: white; font-weight: 600; }
        code { background: #f8f9fa; padding: 4px 8px; border-radius: 4px; font-family: 'Monaco', 'Menlo', monospace; color: #d63384; }
        pre { background: #2d3748; color: #e2e8f0; padding: 20px; border-radius: 8px; overflow-x: auto; margin: 15px 0; font-size: 14px; }
        .scan-img { max-width: 100%; height: auto; border-radius: 8px; box-shadow: 0 4px 12px rgba(0,0,0,0.15); margin: 20px 0; }
        .example { background: #d4edda; border-left: 4px solid #28a745; padding: 12px; margin: 12px 0; border-radius: 4px; }
        .scenario { background: #fff3cd; border-left: 4px solid #ffc107; padding: 12px; margin: 12px 0; border-radius: 4px; }
        .warning { background: #f8d7da; border-left: 4px solid #dc3545; padding: 12px; margin: 12px 0; border-radius: 4px; }
        ul { padding-left: 20px; }
        li { margin-bottom: 8px; }
    </style>
</head>
<body>

<h1>🔍 Nmap Network Scanning Mastery</h1>
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
