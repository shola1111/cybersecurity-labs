Phishing Email Analysis - SOC LEVEL 1 LAB

Objective/Scenerio
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
