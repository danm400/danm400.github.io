---
layout: post
title: A Phishing E-Mail Investigation!
categories: [cybersec]
---

A suspect looking e-mail arrives in my inbox from a client, as i'm not expecting anything from them, I decide to dig deeper to find out where the e-mail is really from!

<!--more-->

Summary: An email from a known, usually safe client email address was received, which seemed to contain a link to a MS Word document. Open source investigation led to the conclusion that this email was a part of a wider phishing campaign targeting businesses by utilising Sqaurespace hosting infrastructure as part of the chain in order to appear legitimate. A number of squarespace domains matching the “username” format flagged on VirusTotal post and prior to the phishing attempt, indicating an ongoing campaign.

<h2>Investigation Details</h2>

The email in question:

<img src="danm400.github.io/assets/image
/1phish1.png" alt="A screenshot of a suspicious email">

Initially we weren't expecting anything from this client, and the email address was "correct," the first port of call was to make contact with the "sender" of the email to see if this was in fact sent by them, which they confirmed was NOT the case and they had indeed been compromised!

The Investigation begins….!

The first port of call was to examine the email headers for anything suspicious.  Both the DKIM and SPF checks were passed, which confirmed what our client had, their email address or domain has been compromised, likely by the same threat actor as part of the same phishing campaign and is now being used to carry out further phishing..




The next step was to  find a safe way to investigate any links or files within the email. In this case the endpoint within the “Open” button, to see where the domain  would take us.

For this I used the Any.Run sandbox. which would allow me to safely open the email and see any network or process information.

AnyRun is an interactive malware analysis tool that can be used for dynamic and static analysis of malware samples within a safe sandbox environment.

The subsequent resulting analysis in AnyRun identified the “Open” button contained the URL  accesspage853[.]ubpages[.]com.









Analysing the URL in urlscan showed the effective URL was in fact nectarine-glockenspiel-xm2m[.]squarespace[.]com, and resolved to IP 198[.]185[.]159[.]176  also belonging to Squarespace.



Digging deeper into the IP address on URLScan, my initial assessment was that the threat actor was using some kind of  domain generation algorithm, generating domains that follow a specific pattern of two random words followed by a 4 character string. Using the IP address as a pivot point within VirusTotal clearly showed a number of domains matching this format being flagged as malicious over a steady period of time post and prior analysis:


Searching through these domains using VirusTotal, an interesting detection is found under the domain, that it shows activity related to the AgentTesla Remote Access Trojan/Malware.



I flagged the IOC’s i had uncovered with a firiend, @Lawrence_Sec, a Senior Threat  Intel Analyst at Recorded Future, who shed more light on the Squarespace domains. These were not using a DGA however were in fact referencing a square space username. 

Prior research conducted by CheckPoint, indicates that the technique (BEC 3.0) of hosting malicious content on legitimate domains to bypass security solutions like VirusTotal is becoming more common, and is harder for end users to spot, as the original email and domain appear to be legitimate. This means that advanced protection like Click-Time Protection and URL Emulation are essential to protect businesses, along with user training to be aware of modern business email compromise.















