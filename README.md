# JACK-ROOM-From-THM
TryHackMe machine “Jack”: a step-by-step guide from reconnaissance and enumeration to exploitation and privilege escalation. Includes the exact commands used, attacker reasoning, and tips to help beginners quickly grasp the pentesting workflow.
<h3>  <img width="791" height="860" alt="image" src="https://github.com/user-attachments/assets/978b0eea-0802-441a-b8bc-0dc543775ae5" />
 </h3>
<h3>Maltego simulation map of the penetration test against the TryHackMe ‘Jack’ room.</h3>
===========================================================================
<h1>Pentest Summary — TryHackMe "Jack"</h1>

<h2>Primary Steps</h2>
<ul>
  <li><label><input type="checkbox"> <strong>1. Scope & Target Confirmation</strong> — define scope and confirm permitted targets.</label></li>
  <li><label><input type="checkbox"> <strong>2. Reconnaissance & Scanning</strong> — scan the target to discover open ports, services, and suspicious assets.</label></li>
  <li><label><input type="checkbox"> <strong>3. Service Exploitation</strong> — test and attack suspicious services discovered during enumeration.</label></li>
  <li><label><input type="checkbox"> <strong>4. Initial Access</strong> — exploit a vulnerability to obtain a reverse shell / install a backdoor (lab-permitted only).</label></li>
  <li><label><input type="checkbox"> <strong>5. Privilege Escalation</strong> — discover and exploit vectors to escalate to root / administrator.</label></li>
</ul>
<hr/>
===========================================================================
<h1>1. Scope & Target Confirmation</h1>
<h2>Connect to OpenVPN</h2>
<h3>(assumes you have a .ovpn file such as jack.ovpn or tryhackme.ovpn)</h3>
<h4>Run from a terminal (Linux / WSL / macOS with OpenVPN installed):</h4>
=== run in foreground to see logs ===
<h5>sudo openvpn --config ~/Downloads/jack.ovpn</h5>
<h2>Edit /etc/hosts to map the lab IP to jack.thm</h2>
<h4>Interactive (nano)</h4>
<h5>sudo nano /etc/hosts</h5>
# add the line:
# 10.201.127.126    jack.thm
# Save: Ctrl+O, Enter. Exit: Ctrl+X
<h2>Verify connectivity</h2>
# ping the hostname
<h5>>ping -c 3 jack.thm</h5

<h1>2. Reconnaissance & Scanning</h1>
<h2>Performed an nmap scan which revealed an HTTP service hosting WordPress.</h2>

<img width="1309" height="587" alt="2" src="https://github.com/user-attachments/assets/ae95a920-4b1e-49bc-ad73-a55778d34235" />
<h5>use the tool with a command: sudo nmap -sV -sC --open -oA nmap jack.thm</h5>
==> "_/wp-admin/"
<h2>WordPress enumeration (WPScan)</h2>

<img width="928" height="651" alt="3" src="https://github.com/user-attachments/assets/428c2d55-3695-42ed-804d-22770e4fe8b4" />
<h5>use the tool with a command: wpscan -e u,ap --url http://jack.thm</h5>
I see 3 users in WordPress
<img width="1482" height="532" alt="user" src="https://github.com/user-attachments/assets/532d3a37-9a87-44a5-b13d-c75faf65c317" />
