<h1>Offensive Security CTF</h1>

<h2>Description</h2>
This project demonstrates the offensive security skills I learned in UT Austin's cybersecurity bootcamp to attack a fictional organization, Rekall Corporation, to determine and exploit it's various web and server vulnerabilities. The lab spanned over the course of one week, and myself along with four other bootcamp colleagues participated in the following tasks:

<h3>Timeline</h3>
<ul>
 <li>Day 1: Attempted to identify and exploit vulnerabilities on Rekall's web application.</li>
 <li>Day 2: Identified and exploited vulnerabilities on Rekall's Linux servers.</li>
 <li>Day 3: Identified and exploited vulnerabilities on Rekall's Windows servers.</li>
</ul>

<h2>Security Tools/Techniques & Utilities Used</h2>

<ul>
 <li>Penetration testing methodology</li>
 <li>MITRE framework</li>
 <li>OSINT tools</li>
 <li>Metasploit/Meterpreter</li>
 <li>Vulnerability scanning with Nmap and Nessus</li>
 <li>Burp Suite</li>
</ul>

</br>

<ul>
 <li>Conducted a penetration test against a mock organization following the PTES methodology and MITRE framework.</li>
 <li>Found and exploited vulnerabilities on the organization’s web application and Linux and Windows hosts.</li>
 <li>Summarized findings and recommended mitigations in a penetration testing summary report.</li>
</ul>

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
 <li>Vulnerability: Reflected XSS</li>
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
 
 <li>Vulnerability: Advanced Reflected XSS</li>
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
 
 <li>Vulnerability: Stored XSS</li>
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
 
  <li>Vulnerability: Data Exposure - HTTP Response Headers</li>
 <ul>
  <li>Viewed the HTTP response headers of the About-Rekall.php section of the web app revealing sensitive information as well as the fourth flag.</li>
  <li>Command used: <i>curl -v http://192.168.14.35/About-Rekall.php</i></li>
  <li>Suggested remediation: Implement proper access controls and server-side validation.</li>
 </ul>
 <p align="center">
 <img src="https://i.imgur.com/ovggOBe.png" height="80%" width="80%" alt="Flag 4"/>
 <br />
 </p>
 
  <li>Vulnerability: Local File Inclusion (LFI)</li>
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
 
  <li>Vulnerability: Advanced LFI</li>
 <ul>
  <li>When probing the secondary upload field on the memory-planner page, pen testers from Team 10 LLC attempted uploading the same .php script file, renamed as “script.jpg.php.” This prompted a response from the web application to reveal sensitive data which can be further exploited.</li>
  <li>Affected Hosts: 192.168.13.45/Memory-planner.php</li>
  <li>Suggested remediation: File upload validation + Sanitization - Ensure only files with ‘.jpg’ format are accepted and the upload field is configured to sanitize the user input to prevent LFI attempts.</li>
 </ul>
 <p align="center">
 <img src="https://i.imgur.com/q0IknYi.png" height="80%" width="80%" alt="Flag 6"/>
 <br />
 </p>
 
  <li>Vulnerability: Suspected SQL Injection</li>
 <ul>
  <li>When probing the user login fields, I discovered the login.php page is vulnerable to SQL injection attacks. I was unable to determine the proper command to input into the right field but was able to yield the following error message indicating a potential vulnerability:</li>
  <li>Injection query used: <i>ok' or 1=1--</i></li>
 </ul>
 <p align="center">
 <img src="https://i.imgur.com/sGB13B2.png" height="80%" width="80%" alt="Flag 7"/>
 <br />
 </p>
 
  <li>Vulnerability: Data Exposure - Admin Credentials</li>
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
 
  <li>Vulnerability: Data Exposure - Directory Traversal Attack</li>
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

<h2>Day 2: Probing Rekall's Linux Servers</h2>
<h3>Setup:</h3>

<ul>
 <li>Using a VM, I logged into Kali Linux with the following credentials:</li>
 <ul>
  <li>User: root</li>
  <li>Password: kali</li>
 </ul>
 <li>In a terminal, and cd over to: /root/Documents/day_2 and ran the following commands:</li>
 <ul>
  <li><i>docker-compose pull</i></li>
  <li><i>docker-compose up</i></li>
 </ul>
 <li>I then opened a browser in Firefox and accessed Nessus by navigating to: https://kali:8834/. Once I had everything set up, I then began using the hints provided by the TA's on how to uncover each flag one by one. Here are the following vulnerabilities (flags) I found during this portion of the lab:</li>
</ul>

<ol>
 <li>Vulnerability: Domain Registrar Data Exposure</li>
 <ul>
  <li>Exploit Method: I used the Domain Dossier tool on CentralOps.net to gather information about the domain ‘totalrekall.xyz.’ The team was able to view sensitive PII regarding Admin level credentials, phone numbers, email and mailing addresses, etc. This information was exposed by performing a domain WHOIS record search of the URL.
  </li>
  <li>Affected Hosts: totalrekall.xyz</li>
  <li>Suggested remediation: Remove sensitive data from the associated server immediately. </li>
 </ul>
  <p align="center">
 <img src="https://i.imgur.com/FqHhKar.png" height="80%" width="80%" alt="Day 2 Flag 1"/>
 <br />
 </p>

 <li>Vulnerability: DNS Record Exposure</li>
 <ul>
  <li>Exploit Method: I used the same Domain Dossier utility to view DNS records of totalrekall.xyz. This revealed sensitive information including IP addresses,subdomains, and email addresses associated with the URL.
  </li>
  <li>Affected Hosts: totalrekall.xyz</li>
  <li>Suggested remediation: Remove any immediately sensitive information from the records and implement logging and monitoring mechanisms to scan for any unauthorized access attempts.</li>
 </ul>
  <p align="center">
 <img src="https://i.imgur.com/IFhYKiw.png" height="80%" width="80%" alt="Day 2 Flag 2"/>
 <br />
 </p>

 <li>Vulnerability: Certificate Information Exposure</li>
 <ul>
  <li>Description: I used crt.sh tools to view certificate validity of totalrekall.xyz which revealed that there was no valid root/intermediate certificate.</li>
  <li>Affected Hosts: totalrekall.xyz</li>
  <li>Suggested remediation: Update the SSL certificate by contacting the Certificate Authority (CA) immediately.</li>
 </ul>
  <p align="center">
 <img src="https://i.imgur.com/WllYyaV.png" height="80%" width="80%" alt="Day 2 Flag 3"/>
 <br />
 </p>

 <li>Vulnerability: Apacher Tomcat Bypass RCE (CVE-2017-12617)</li>
 <ul>
  <li>Description: I used metasploit exploit modules to demonstrate RCE vulnerability and drop into root session on remote host 192.168.13.10. I searched for exploits that had Tomcat and JSP. I then used the exploit module <i>multi/http/tomcat_jsp_upload_bypass</i>, and set the RHOST to 192.168.13.10. After getting a Meterpreter shell, I then dropped into a system shell to get to the command line.</li>
  <li>Affected Hosts: 192.168.13.10 on port 80.</li>
  <li>Suggested remediation: Apply a patch or update to Apache Tomcat installed on the remote host. In addition, consider implementing better network security measures to restrict access on vulnerable ports.</li>
 </ul>
  <p align="center">
 <img src="https://i.imgur.com/n16r8ru.png" height="80%" width="80%" alt="Day 2 Flag 7"/>
 <br />
 </p>

 <li>Vulnerability: Shellshock</li>
 <ul>
  <li>Description: I ran MSFconsole and searched for exploits that had Shellshock. I then selected <i>exploit/multi/http/apache_mod_cgi_bash_env_exec</i> and the following options:</li>
  <ul>
   <li>target URI(The vulnerable webpage): /cgi-bin/shockme.cgi</li>
   <li>RHOST: 192.168.13.11</li>
   <li>To find the flag using this exploit, I ran the following command from a shell on the exploited machine: <i>cat /etc/sudoers</i></li>
  </ul>
  <li>Affected Hosts: 192.168.13.11</li>
  <li>Suggested remediation: Update to the most current version of BASH and assess if any other interconnected systems are vulnerable to Shellshock.</li>
 </ul>
  <p align="center">
 <img src="https://i.imgur.com/F1pjPBb.png" height="80%" width="80%" alt="Day 2 Flag 7"/>
 <br />
 </p>

 <li>Vulnerability: Struts</li>
 <ul>
  <li>Description: I used Nessus to determine RHOST 192.168.13.12 is vulnerable to Struts exploitation. I then used MSFconsole to use Struts exploit <i>multi/http/struts2_content_type_ognl</i> to establish a Meterpreter shell on the RHOST 192.168.13.12. With this, I was able to extract a special zip file containing sensitive information (Flag 9).</li>
  <ul>
   <li>Used Meterpreter to download the following file: /root/flagisinThisfile.7z</li>
   <li>In my Kali machine, I unzipped the file with the following command: 7z x flagisinThisfile.7z</li>
   <li>Used <i>cat</i> to view the flag file.</li>
  </ul>
  <li>Affected Hosts: 192.168.13.12</li>
  <li>Suggested remediation: Update Apache Struts depending on the version the host is using. In addition, consider implementing a Web Application Firewall to block malicious attempts to exploit Struts.</li>
 </ul>
  <p align="center">
 <img src="https://i.imgur.com/Gwehmf3.png" height="80%" width="80%" alt="Day 2 Flag 10"/>
 <br />
 </p>

 <li>Vulnerability: Drupal - CVE-2019-6340</li>
 <ul>
  <li>Description: I used MSFconsole to search for drupal exploits. Used the exploit <b>unix/webapp/drupal_restws_unserialize</b> to establish a meterpreter session in RHOST 192.168.13.13. Performed the <b>getuid</b> command and received <b>www-data</b> as the UID for that host.</li>
  <li>Affected Hosts: 192.168.13.13</li>
  <li>Suggested remediation: Update Drupal to the latest version that includes the latest security patches.</li>
 </ul>
  <p align="center">
 <img src="https://i.imgur.com/34ly5kp.png" height="80%" width="80%" alt="Day 2 Flag 11 Drupal"/>
 <br />
 </p>

  <li>Vulnerability: SUDO without password</li>
 <ul>
  <li>Description: I used password guessing techniques to SSH into RHOST 192.168.13.14 using information gathered in WHOIS records. Guessed password ‘alice’, successfully executed ssh into RHOST as alice and used sudo to extract sensitive data in root level directories.</li>
  <li>Affected Hosts: 192.168.13.14</li>
  <li>Suggested remediation: Update admin password to something more complex, and disable SSH on that port.</li>
 </ul>
  <p align="center">
 <img src="https://i.imgur.com/UFOHsK1.png" height="80%" width="80%" alt="Day 2 Flag 12 Password Guessing"/>
 <br />
 </p>
</ol>















