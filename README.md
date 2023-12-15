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

<h2>Day 1: Web Application</h2>
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













