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
 
  <li>Stored XSS</li>
 <ul>
  <li>Probed the 'welcome.php' page of the Rekall web app by inserting a basic JavaScript alert payload into the "Put your name here" field.</li>
  <li>Exploit script used: <i><script>alert("You've been hacked!");</script></i></li>
 </ul>
 <p align="center">
 <img src="https://i.imgur.com/mw9qyzP.png" height="80%" width="80%" alt="Flag 1"/>
 <br />
 </p>
  <li>Stored XSS</li>
 <ul>
  <li>Probed the 'welcome.php' page of the Rekall web app by inserting a basic JavaScript alert payload into the "Put your name here" field.</li>
  <li>Exploit script used: <i><script>alert("You've been hacked!");</script></i></li>
 </ul>
 <p align="center">
 <img src="https://i.imgur.com/mw9qyzP.png" height="80%" width="80%" alt="Flag 1"/>
 <br />
 </p>
  <li>Stored XSS</li>
 <ul>
  <li>Probed the 'welcome.php' page of the Rekall web app by inserting a basic JavaScript alert payload into the "Put your name here" field.</li>
  <li>Exploit script used: <i><script>alert("You've been hacked!");</script></i></li>
 </ul>
 <p align="center">
 <img src="https://i.imgur.com/mw9qyzP.png" height="80%" width="80%" alt="Flag 1"/>
 <br />
 </p>
  <li>Stored XSS</li>
 <ul>
  <li>Probed the 'welcome.php' page of the Rekall web app by inserting a basic JavaScript alert payload into the "Put your name here" field.</li>
  <li>Exploit script used: <i><script>alert("You've been hacked!");</script></i></li>
 </ul>
 <p align="center">
 <img src="https://i.imgur.com/mw9qyzP.png" height="80%" width="80%" alt="Flag 1"/>
 <br />
 </p>
  <li>Stored XSS</li>
 <ul>
  <li>Probed the 'welcome.php' page of the Rekall web app by inserting a basic JavaScript alert payload into the "Put your name here" field.</li>
  <li>Exploit script used: <i><script>alert("You've been hacked!");</script></i></li>
 </ul>
 <p align="center">
 <img src="https://i.imgur.com/mw9qyzP.png" height="80%" width="80%" alt="Flag 1"/>
 <br />
 </p>
  <li>Stored XSS</li>
 <ul>
  <li>Probed the 'welcome.php' page of the Rekall web app by inserting a basic JavaScript alert payload into the "Put your name here" field.</li>
  <li>Exploit script used: <i><script>alert("You've been hacked!");</script></i></li>
 </ul>
 <p align="center">
 <img src="https://i.imgur.com/mw9qyzP.png" height="80%" width="80%" alt="Flag 1"/>
 <br />
 </p>
  <li>Stored XSS</li>
 <ul>
  <li>Probed the 'welcome.php' page of the Rekall web app by inserting a basic JavaScript alert payload into the "Put your name here" field.</li>
  <li>Exploit script used: <i><script>alert("You've been hacked!");</script></i></li>
 </ul>
 <p align="center">
 <img src="https://i.imgur.com/mw9qyzP.png" height="80%" width="80%" alt="Flag 1"/>
 <br />
 </p>
  <li>Stored XSS</li>
 <ul>
  <li>Probed the 'welcome.php' page of the Rekall web app by inserting a basic JavaScript alert payload into the "Put your name here" field.</li>
  <li>Exploit script used: <i><script>alert("You've been hacked!");</script></i></li>
 </ul>
 <p align="center">
 <img src="https://i.imgur.com/mw9qyzP.png" height="80%" width="80%" alt="Flag 1"/>
 <br />
 </p>
  <li>Stored XSS</li>
 <ul>
  <li>Probed the 'welcome.php' page of the Rekall web app by inserting a basic JavaScript alert payload into the "Put your name here" field.</li>
  <li>Exploit script used: <i><script>alert("You've been hacked!");</script></i></li>
 </ul>
 <p align="center">
 <img src="https://i.imgur.com/mw9qyzP.png" height="80%" width="80%" alt="Flag 1"/>
 <br />
 </p>
</ol>















