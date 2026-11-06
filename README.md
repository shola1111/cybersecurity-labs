## Phishing Email Analysis - SOC LEVEL 1 LAB

## Objective/Scenerio
"In this scenerio, I acted as a Level 1 SOC Analyst. As the first line of defense, my role was to identify
phisihing and spam emails reported by end users. The objective was to carefully review and analyze multiple suspicious emails that have been escalated by coworkers."

Goals of the Investigation:

1)Extract key indicators (IOCs) from each email.
2)Identify any signs of malicious activity.
## Email 1
![ Email 1 Overview ](screenshots/header-email(1).png)

Email :"Your Netflix Account is on hold"

Header Analysis:


Sender: N e t f I i x <JGQ47wazXe1xYVBrkeDg-JOg7ODDQwWdR@JOg7ODDQwWdR-yVkCaBkTNp[.]gogolecloud[.]com> (Notice brand name that was spoofed NETFLIX)

![ Email 1 Overview ](screenshots/header-email(1).png)

Intended receiver: redacted@yahoo[.]com

Received from IP:10[.]197[.]37[.]234

Return-Path / Reply-To: etekno[.]xyz


DKIM : unkown
SPF: none 
Sender Domain: etekno[.]xyz
![ Email 1 Header ](screenshots/header-email(2).png)


Email Body Analysis:
Call to Action: The email contains a button labeled "Update account Now.
This uses urgency to trick the user into clicking.
![ Email 1 button ](screenshots/body-button-urlemail(3).png)

Hidden Link (URL SHORTENER): When viewing the email in thunderbird, hovering over the button reveals a shortened URL instead of actual destination.Phishing use URL shorteners to hide malicious domain and bypass security filters.

Extracted URL: hxxps://t[.]co/yuxfZm8KPg?amp=1

![ Email 1 button ](screenshots/body-button-urlemail4.png)

---




## Email 2: "Netflix Payment Update" (PDF Attachment Analysis) 
![ Email 2 Overview ](screenshots/email2yy.png)
![ Email 2 Overview ](screenshots/Email2yyy.png)
### Objective 
Investigate a suspicious attachment ('Payment-update.pdf') using the ANY.RUN sandbox environment to observe its execution behavior, network activity, and extract Indicators of Compromise (IOCs).

### Sandbox Analysis (ANY.RUN)
![ ANY.RUN Execution ](screenshots/Email2yyyExe.png)


**1 File Execution & Behavior:**
Attachment Name: 'Payment-Update.pdf'
When executed in the sandbox, the PDF opened a web browser process "firefox.exe".
Instead of displaying a document, the PDF silently redirected browser to a fake Netflix "Account on Hold" login page.
**ANY.RUN Classification:**The sandbox classified this as a "Suspicious activity" and specifically refer to it as "Potentially Bad Traffic".

**2 Network Activity & Payload Delivery:**
The PDF document contained an embedded URL that forced the browser to navigate to: 'hxxps://lihi1[.]com/JgdmJ'.
This URL resoled to the IP address: 35[.]244[.]149[.]249
The page was designed to harvest user credentials by tricking the victim into entering their Netflix password.

## Indicators of Compromise (IOCs)**
* File Name: 'Payment-Update.PDF'
* DM5 Hash: '4a2775eae2ebef41901a3f08d3b857c8'
* Malicious URL: 'hxxps://lihi1[.]com/JgdmJ'
* IP ADDRESS: '35[.]244[.]149[.]249'

### CONCLUSION
The attachment is a malicious PDF. It uses an embedded URL to redirect the victim to a credential harvesting site. The URL ('lihi1.com') is a know shortener, which attackers use to hide their final destination and bypass email filters.

---





## Email 3: Malicious Excel Document (.xlsx) - EQNEDT32 Exploit

![Email 3 Document](screenshots/Email39999.png)

### Objective
Investigate a different suspicious phishing attachment (`CBJ200620083959.xlsx`) using the ANY.RUN sandbox. The goal was to review the execution results to identify notable behaviors, process activity, network connections, and IOCs.

### Sandbox Analysis (ANY.RUN)
![ANY.RUN Execution](screenshots/ANY-RUN-EXECUTE.png)

**1. Document Content (Social Engineering):**
* The attachment is an Excel spreadsheet disguised as a "Supplier Appraisal Form" (written in Chinese). 
* This is a social engineering tactic to convince the user to click "Enable Editing" or "Enable Macros" to view the content, which triggers the malicious payload.

**2. File Execution & Process Activity:**
* **Attachment Name:** `CBJ200620083959.xlsx`
* When launched, the file drops and executes a suspicious process called `EQNEDT32.EXE`.
* **Full Path:** `C:\Program Files\Common Files\Microsoft Shared\EQUATION\EQNEDT32.EXE`
* **Analysis:** `EQNEDT32.EXE` is the legitimate Microsoft Equation Editor. Attackers abuse this process to execute malicious code (Remote Code Execution) and bypass security controls.
![File Execute & Process Activity](screenshots/FILE-EXE-PROCESS-ACT.png)

**3. Exploit Identified:**
* The malicious file attempts to exploit **CVE-2017-11882**.
* This is a famous memory corruption vulnerability in the Equation Editor. Even though it is an older vulnerability, it remains highly effective in phishing campaigns because many systems are unpatched.

**4. Network Activity (Payload Delivery):**
* Once the exploit executes, the malware reaches out to the internet to download its final payload.
* The sandbox intercepted a `GET` request to download a COVID-themed malicious executable:
* **Download URL:** `hxxp://big9holdings[.]com/INVOICE/COVID19[.]exe`
![Net Act](screenshots/Network-Th1.png)

### Indicators of Compromise (IOCs)
* **Malicious File:** `CBJ200620083959.xlsx`
* **Suspicious Process:** `EQNEDT32.EXE`
* **Exploited Vulnerability:** `CVE-2017-11882`
* **Malicious Domain:** `big9holdings[.]com`
* **Network Threat:** ET INFO Suspicious GET Request with Possible COVID-19 URI M1

### Conclusion
This is a weaponized Excel document. By exploiting CVE-2017-11882, the attacker can execute arbitrary code without needing the user to manually enable macros. The malware immediately downloads a secondary payload from `big9holdings[.]com`. In a real SOC environment, this would be escalated as a critical incident, the endpoint would be isolated, and the domain would be blocked at the firewall.
