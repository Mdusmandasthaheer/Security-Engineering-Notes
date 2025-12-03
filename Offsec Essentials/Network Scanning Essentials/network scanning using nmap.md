<!DOCTYPE html>
<html>
<head>
    <title>Nmap Network Scanning - Pentest Notes</title>
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
        .note-box { background: #fff3cd; border-left: 5px solid #ffc107; padding: 15px; margin: 20px 0; border-radius: 6px; font-style: italic; }
    </style>
</head>
<body>

<h1>🔍 Nmap Network Scanning - Quick Notes</h1>

<p>Network scanning is your first port of call during a pentest. The goal? Discover which hosts are alive on the network and what services they expose. <strong>Nmap</strong> is your best friend here because it gives you reliable host discovery and precise port/service info to plan your attack.</p>

<img src="https://github.com/Mdusmandasthaheer/Security-Engineering-Notes/blob/2c73057f044ed7427257c79cf905539ec7374be9/Offsec%20Essentials/Files/Screenshot-01.png" alt="Nmap Scan Example" class="scan-img">

<h2>Host Discovery Commands</h2>

<ul>
    <li><code>sudo nmap -PE -sn 192.168.1.1/24</code>: Simple ICMP echo ping sweep to list live hosts.</li>
    <li><code>sudo nmap -PA -sn 192.168.1.1/24</code>: TCP ACK ping sweep, ideal for bypassing some firewalls.</li>
    <li><code>sudo arp-scan -interface eth0 -l</code>: ARP scan on local network, fastest way to find hosts in your subnet.</li>
</ul>

<h2>Open Port & Service Scans</h2>

<ul>
    <li><code>sudo nmap -A -sV -sC -v -T4 192.168.1.123</code>: Aggressive scan with service/version detection, default scripts, and verbose output.</li>
    <li><code>sudo nmap -sC -p- -A -Pn 192.168.1.112 -T4 --min-rate 1000</code>: Scan all ports with default scripts skipping ping, good for stealthy fast scans.</li>
    <li><code>sudo nmap -PA 433 --version-intensity 9 -T4 -g 53 -osscan-guess -v -p '*' --reason --stats-every 20s 192.168.1.120</code>: Detailed scan on port 433, guessing OS and reasons for findings, great for detailed reconnaissance.</li>
    <li><code>sudo nmap 192.168.1.12 -p- -sV -Pn -n --disable-arp-ping --packet-trace</code>: Scan all ports disabling ARP ping and tracing packet flow, useful for debugging or stealth.</li>
    <li><code>sudo nmap -PU 433</code>: UDP ping on port 433.</li>
    <li><code>sudo nmap -PY 433</code>: SCTP ping on port 433.</li>
    <li><code>sudo nmap -PM</code>: Modified ICMP ping for evasion.</li>
    <li><code>sudo nmap -sN</code>: Null scan to stealthily detect open ports.</li>
</ul>

<p class="note-box">Tip: You can add <code>--scan-delay 10ms</code> and <code>--data-length &lt;num&gt;</code> to fine-tune scan speed and evade detection systems.</p>

<h2>SMB Service Scan Example</h2>

<pre><code>sudo nmap -sV -A -p445 -sC -v -T4 192.168.1.123</code></pre>
<p>This command targets SMB on port 445 to enumerate versions and run default aggressive scripts to find vulnerabilities.</p>

</body>
</html>
