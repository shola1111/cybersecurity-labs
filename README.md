Phishing Email Analysis - SOC LEVEL 1 LAB

Objective/Scenerio
"In this scenerio, I acted as a Level 1 SOC Analyst. As the first line of defense, my role was to identify
phisihing and spam emails reported by end users. The objective was to carefully review and analyze multiple suspicious emails that have been escalated by coworkers."

Goals of the Investigation:

1)Extract key indicators (IOCs) from each email.
2)Identify any signs of malicious activity.

Email 1:"Your Netflix Account is on hold"

Header Analysis:

Sender: N e t f I i x <JGQ47wazXe1xYVBrkeDg-JOg7ODDQwWdR@JOg7ODDQwWdR-yVkCaBkTNp[.]gogolecloud[.]com> (Notice brand name that was spoofed NETFLIX)

Intended receiver: redacted@yahoo[.]com

Received from IP:10[.]197[.]37[.]234

Return-Path / Reply-To: etekno[.]xyz


DKIM : unkown
SPF: none 
Sender Domain: etekno[.]xyz

Email Body Analysis:
Call to Action: The email contains a button labeled "Update account Now.
This uses urgency to trick the user into clicking.

Hidden Link (URL SHORTENER): When viewing the email in thunderbird, hovering over the button reveals a shortened URL instead of actual destination.Phishing use URL shorteners to hide malicious domain and bypass security filters.

Extracted URL: hxxps://t[.]co/yuxfZm8KPg?amp=1
