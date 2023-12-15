<h1>Offensive Security CTF</h1>

<h2>Description</h2>
This project demonstrates the offensive security skills I learned in UT Austin's cybersecurity bootcamp to attack a fictional organization, Rekall Corporation, to determine and exploit it's various web and server vulnerabilities. The lab spanned over the course of one week, and myself along with four other bootcamp colleagues participated in the following tasks:
<ul>
 <li>Day 1: Attempted to identify and exploit vulnerabilities on Rekall's web application.</li>
 <li>Day 2: Identified and exploited vulnerabilities on Rekall's Linux servers.</li>
 <li>Day 3: Identified and exploited vulnerabilities on Rekall's Windows servers.</li>
</ul>

<h2>Security Tools/Techniques & Utilities Used</h2>

- <b>Kali Linux</b>
- <b>MSFconsole</b> 
- <b>Metasploit</b>
- <b>Nmap/Zenmap</b>
- <b>Nessus</b>
- <b>Metasploit</b>
- <b>Mimikatz-Kiwi</b>
- <b>https://centralops.net/co/DomainDossier.aspx</b>

<h2>Environments Used </h2>

- <b>Rekall Web Application</b>
- <b>Azure Windows 10 VM</b>

<h2>Project Scenario</h2>
<ul>
 <li>Rekall Corporation is a fictional company that specializes in offering virtual reality experiences based on images that customers upload.</li>
 <ul>
  <li>These experiences could include dream vacations, adventures, or even secret missions.</li>
  <li>Rekall guarantees that these virtual reality experiences will feel real.</li>
 </ul>
 <li>Rekall is about to go live with their business, and they need penetration testers to find any vulnerabilities within their technical systems.</li>
 <ul>
  <li>Rekall has a brand new web application and several Windows and Linux servers that manage their businesses.</li>
 </ul>
</ul>

<h2>Day 1: Probing Rekall's Web Application</h2>
<h3>Setup:</h3>

<ul>
 <li>Using a VM, I logged into Kali Linux with the following credentials:</li>
 <ul>
  <li>User: root</li>
  <li>Password: kali</li>
 </ul>
 <li>In a terminal, and cd over to: /root/Documents/day_1 and ran the following commands:</li>
 <ul>
  <li>Type: docker-compose pull and press Enter, then...</li>
  <li>Type: docker-compose up and press Enter.</li>
 </ul>
 <li>I then opened a browser in Firefox and accessed the web application at http://192.168.14.35. The webpage should resemble the following image:</li>
</ul>

<p align="center">
<img src="https://i.imgur.com/LwhZ2iT.png" height="80%" width="80%" alt="Rekall Homepage"/>
<br />
</p>

<h3>Vulnerabilities Detected:</h3>
<ol>
 <li>Reflected XSS</li>
 <ul>
  <li>Probed the 'welcome.php' page of the Rekall web app by inserting a basic JavaScript alert payload into the "Put your name here" field.</li>
  <li>Exploit script used: <i><script>alert("You've been hacked!");</script></i></li>
  <li>Affected Hosts: 192.168.14.35/Welcome.php</li>
  <li>Suggested remediation: Implement input validation.</li>
 </ul>
 <p align="center">
 <img src="https://i.imgur.com/mw9qyzP.png" height="80%" width="80%" alt="Flag 1"/>
 <br />
 </p>
 
 <li>Advanced Reflected XSS</li>
 <ul>
  <li>Successfully attempted another reflected XSS injection with modified payload in the form of masking the script tags: </li>
  <li>Exploit script used: <i><SCRIPscriptT>alert("You've been hacked!");</SCRIPscriptT></i></li>
  <li>Affected Hosts: 192.168.14.35/Memory-planner.php</li>
  <li>Suggested remediation: Implement better input validation measures to restrict advanced scripting tags/scripting entries of any kind.</li>
 </ul>
 <p align="center">
 <img src="https://i.imgur.com/KA4BKuu.png" height="80%" width="80%" alt="Flag 2"/>
 <br />
 </p>
 
 <li>Stored XSS</li>
 <ul>
  <li>Performed XSS injection on comments.php page of totalrekall website to generate an alert.</li>
  <li>Exploit script used: <i><script>alert(“hi there”);</script></i></li>
  <li>Affected Hosts: 192.168.14.35/comments.php</li>
  <li>Suggested remediation: Implement output encoding to properly prevent user-generated content from being interpreted as HTML or JavaScript code that might execute a malicious payload.</li>
 </ul>
 <p align="center">
 <img src="https://i.imgur.com/csqW5uo.png" height="80%" width="80%" alt="Flag 3"/>
 <br />
 </p>
 
  <li>Data Exposure - HTTP Response Headers</li>
 <ul>
  <li>Viewed the HTTP response headers of the About-Rekall.php section of the web app revealing sensitive information as well as the fourth flag.</li>
  <li>Command used: <i>curl -v http://192.168.14.35/About-Rekall.php</i></li>
  <li>Suggested remediation: Implement proper access controls and server-side validation.</li>
 </ul>
 <p align="center">
 <img src="https://i.imgur.com/ovggOBe.png" height="80%" width="80%" alt="Flag 4"/>
 <br />
 </p>
 
  <li>Local File Inclusion (LFI)</li>
 <ul>
  <li>I uploaded a basic php script file into the first upload field on the memory-planner.php page. This revealed that this particular field is not configured to accept only image files which causes critical risk to the safety of the web app.</li>
  <li>Affected Hosts: 192.168.13.45/memory-planner.php</li>
  <li>Suggested remediation: File Upload Validation - Ensure that the only form of file that can be uploaded are files ending in .jpg or any other image related file.</li>
 </ul>
 <p align="center">
 <img src="https://i.imgur.com/4CIwRek.png" height="80%" width="80%" alt="Flag 5 - PHP Script"/>
 <br />
 </p>
 <p align="center">
 <img src="https://i.imgur.com/fYRKxHb.png" height="80%" width="80%" alt="Flag 5"/>
 <br />
 </p>
 
  <li>Advanced LFI</li>
 <ul>
  <li>When probing the secondary upload field on the memory-planner page, pen testers from Team 10 LLC attempted uploading the same .php script file, renamed as “script.jpg.php.” This prompted a response from the web application to reveal sensitive data which can be further exploited.</li>
  <li>Affected Hosts: 192.168.13.45/Memory-planner.php</li>
  <li>Suggested remediation: File upload validation + Sanitization - Ensure only files with ‘.jpg’ format are accepted and the upload field is configured to sanitize the user input to prevent LFI attempts.</li>
 </ul>
 <p align="center">
 <img src="https://i.imgur.com/q0IknYi.png" height="80%" width="80%" alt="Flag 6"/>
 <br />
 </p>
 
  <li>Suspected SQL Injection Vulnerability</li>
 <ul>
  <li>When probing the user login fields, I discovered the login.php page is vulnerable to SQL injection attacks. I was unable to determine the proper command to input into the right field but was able to yield the following error message indicating a potential vulnerability:</li>
  <li>Injection query used: <i>ok' or 1=1--</i></li>
 </ul>
 <p align="center">
 <img src="https://i.imgur.com/sGB13B2.png" height="80%" width="80%" alt="Flag 7"/>
 <br />
 </p>
 
  <li>Data Exposure - Admin Credentials</li>
 <ul>
  <li>Used Chrome developer tools feature to view the HTML structure of the login.php webpage. Further analysis revealed sensitive information stored within <p> tags containing admin credentials ‘dougquaid:kuato’. Successfully logged into the admin login field with credentials and was able to view networking.php page.</li>
  <li>Affected Hosts: 192.168.13.45/login.php</li>
  <li>Suggested remediation: Immediately modify source code of totalrekall web page to remove <font> tags or remove content in between them.</li>
 </ul>
 <p align="center">
 <img src="https://i.imgur.com/JYboR8N.png" height="80%" width="80%" alt="Flag 8"/>
 <br />
 </p>
  <p align="center">
 <img src="https://i.imgur.com/yu0SfvO.png" height="80%" width="80%" alt="Flag 8"/>
 <br />
 </p>
 
  <li>Data Exposure: Directory Traversal Attack</li>
 <ul>
  <li>I was able to use path traversal techniques on the disclaimer.php page to view the robots.txt file. With this, it was determined that the goodbot agent is allowed to access all parts of the website. The BadBot agent is not allowed to access any part of the website. The wildcard rule applied to all user agents not mentioned restricts access to certain directories and a particular souvenirs.php URL.
</li>
  <li>Affected Hosts: 192.168.13.45/disclaimer.php?page=robots.txt</li>
  <li>Suggested remediation: Implement Access Controls immediately to restrict access to any other sensitive files and directories. In addition, ensure that only authorized users are allowed to view critical files like robots.txt</li>
 </ul>
 <p align="center">
 <img src="https://i.imgur.com/5IPTRTM.png" height="80%" width="80%" alt="Flag 1"/>
 <br />
 </p>
</ol>















