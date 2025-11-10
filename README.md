# JACK-ROOM-From-THM
TryHackMe machine “Jack”: a step-by-step guide from reconnaissance and enumeration to exploitation and privilege escalation. Includes the exact commands used, attacker reasoning, and tips to help beginners quickly grasp the pentesting workflow.
<h3>  <img width="791" height="860" alt="image" src="https://github.com/user-attachments/assets/978b0eea-0802-441a-b8bc-0dc543775ae5" />
 </h3>
<h3>Maltego simulation map of the penetration test against the TryHackMe ‘Jack’ room.</h3>
===========================================================================
<h1>Pentest Workflow for TryHackMe “Jack”</h1>

<h2>Checklist</h2>
<ul>
  <li><input type="checkbox"> <strong>1. Scope &amp; Rules of Engagement</strong> — confirm target &amp; constraints.</li>
  <li><input type="checkbox"> <strong>2. Passive Reconnaissance</strong> — OSINT &amp; non-interactive discovery.</li>
  <li><input type="checkbox"> <strong>3. Active Recon (Port/Service Scan)</strong> — nmap, banners.</li>
  <li><input type="checkbox"> <strong>4. Service &amp; App Enumeration</strong> — web/SMB/FTP enum.</li>
  <li><input type="checkbox"> <strong>5. Vulnerability Analysis &amp; Plan</strong> — map services → exploits.</li>
  <li><input type="checkbox"> <strong>6. Initial Exploitation / Access</strong> — get user shell / read access.</li>
  <li><input type="checkbox"> <strong>7. Post-Exploitation Enumeration</strong> — creds, configs, jobs.</li>
  <li><input type="checkbox"> <strong>8. Privilege Escalation</strong> — root/admin.</li>
  <li><input type="checkbox"> <strong>9. Pivoting / Lateral Movement</strong> (if any).</li>
  <li><input type="checkbox"> <strong>10. Cleanup</strong> — remove artefacts.</li>
  <li><input type="checkbox"> <strong>11. Technical Report</strong> — doc steps, evidence, risks.</li>
  <li><input type="checkbox"> <strong>12. Executive Summary &amp; Remediation</strong> — prioritized fixes.</li>
</ul>

<hr/>
