<!DOCTYPE html>
<html>
<head>
    <title>Vim & Nano Text Editors Guide</title>
    <style>
        body { font-family: Arial, sans-serif; max-width: 800px; margin: 0 auto; padding: 20px; line-height: 1.6; }
        h1, h2 { color: #333; }
        h1 { border-bottom: 2px solid #007acc; padding-bottom: 10px; }
        table { border-collapse: collapse; width: 100%; margin: 20px 0; }
        th, td { border: 1px solid #ddd; padding: 12px; text-align: left; }
        th { background-color: #f2f2f2; font-weight: bold; }
        code { background: #f4f4f4; padding: 2px 6px; border-radius: 3px; font-family: monospace; }
        pre { background: #f4f4f4; padding: 15px; border-radius: 5px; overflow-x: auto; margin: 10px 0; }
        .green { color: #28a745; }
        .blue { color: #007bff; }
        em { color: #666; font-style: italic; }
    </style>
</head>
<body>

<h1>Vim & Nano Text Editors Guide</h1>

<h2 class="green">🟢 NANO – Simple & User-Friendly</h2>
<p>Nano is a lightweight terminal-based text editor, great for beginners.</p>

<p><strong>📄 Open or Create a File:</strong></p>
<pre><code>nano sample.txt</code></pre>

<p><strong>🔑 Common Shortcuts:</strong></p>
<table>
    <thead>
        <tr><th>Action</th><th>Shortcut</th></tr>
    </thead>
    <tbody>
        <tr><td>Cut a line</td><td>Ctrl + K</td></tr>
        <tr><td>Paste a line</td><td>Ctrl + U</td></tr>
        <tr><td>Search text</td><td>Ctrl + W</td></tr>
        <tr><td>Save file</td><td>Ctrl + O</td></tr>
        <tr><td>Exit editor</td><td>Ctrl + X</td></tr>
    </tbody>
</table>

<p><em>Use nano for quick edits in scripts or config files during pentests when you need speed without complexity.</em></p>

<h2 class="blue">🔵 VIM / VI – Powerful but Advanced</h2>
<p>Vim is a highly efficient, modal text editor often used in system administration and development.</p>

<p><strong>📄 Open or Create a File:</strong></p>
<pre><code>vi sample.txt</code></pre>

<p><strong>🔄 Modes in Vim:</strong></p>
<ul>
    <li><strong>Insert Mode:</strong> For editing text → Press <code>i</code> to enter</li>
    <li><strong>Command Mode:</strong> For running commands → Press <code>Esc</code> to return</li>
</ul>

<p><strong>🛠️ Useful Vim Commands (in Command Mode):</strong></p>
<table>
    <thead>
        <tr><th>Action</th><th>Command</th></tr>
    </thead>
    <tbody>
        <tr><td>Delete current line</td><td><code>dd</code></td></tr>
        <tr><td>Copy current line</td><td><code>yy</code></td></tr>
        <tr><td>Paste copied line</td><td><code>p</code></td></tr>
        <tr><td>Exit without saving</td><td><code>:q</code></td></tr>
        <tr><td>Force quit (no save)</td><td><code>:q!</code></td></tr>
        <tr><td>Save and exit</td><td><code>:wq</code></td></tr>
        <tr><td>Force save and exit</td><td><code>:wq!</code></td></tr>
    </tbody>
</table>

<p><em>Use Vim on remote servers during exploitation or lateral movement when nano isn't available—master these for efficient editing in restricted environments.</em></p>

<h2>✅ Summary</h2>
<table>
    <thead>
        <tr><th>Feature</th><th>Nano</th><th>Vim</th></tr>
    </thead>
    <tbody>
        <tr><td>Learning Curve</td><td>Easy</td><td>Moderate/Hard</td></tr>
        <tr><td>Interface</td><td>On-screen help + simple</td><td>Modal (Insert/Command)</td></tr>
        <tr><td>Ideal for</td><td>Beginners & quick edits</td><td>Power users & scripting</td></tr>
    </tbody>
</table>

</body>
</html>
