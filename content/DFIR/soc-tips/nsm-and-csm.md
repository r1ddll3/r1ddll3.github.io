---
title: "How Can We Monitor"
date: 2022-11-02T02:27:46+02:00
draft: true
tags: ["SOC", "Types of Monitoring"]
author: "@R1ddl3"
# author: ["Me", "You"] # multiple authors
showToc: false
TocOpen: false
draft: false
hidemeta: false
comments: true
description: "Covered NSM and CSM 2 types of monitoring."
canonicalURL: "https://canonical.url/to/page"
disableHLJS: true # to disable highlightjs
disableShare: false
disableHLJS: false
hideSummary: false
searchHidden: false
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
UseHugoToc: true
cover:
    image: "https://i.imgur.com/qoVCwXR.gif" # image path/url
    alt: "How Can We Monitor" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
---

Hey folks, Today I will talk about:  **How We Can Monitor**

Let's Dive in!!

---------
First of all Monitoring has 2 main types:

1. **Endpoints**

2. **Network**
 
 so what is the different between them and what data can I see from them.
 
let's start with Network Monitoring:

## Network
First we have to put some Questions to answer.

- Do you know which **ports** are actually in use?
- Which **services** are actually being used on those ports?
- Do you know which **domains** are being visited and by who?
- Can you detect **malicious** encrypted traffic?
- Can you see **high-level bandwidth** and **traffic flow**?

You Should be noticed we're talking about network analyze.

 **So how do we get the answer?**

Here comes **NSM's** role and it stands for **Network Security Monitoring** 

## What is Network Security Monitoring?

Network security monitoring is an automated process that monitors network devices and traffic for security vulnerabilities, threats, and suspicious activities also it involves collecting and analyzing data, which in turn give companies the opportunity to detect and respond to intruders in their network.

we can basically say with Network Security Monitoring we can know 

> Who is talking to Who what they are saying and what type of service they are actually using.

## What are the benefits of (NSM)?
- Analyzing network traffic.
- Services: DNS, HTTP(S), SMB, RDP, FTP, SSH, etc.
- Identifying risky / compromise-like behavior

	- Exploit Delivery
	- Internal recon and pivoting
	- Command & Control (C2) Traffic
	- Data Exfiltration
	- Executable content transfer 

## NSM By Layer

- Layer 3 & 4
  
  - NetFlow, Firewall Logs, Statistical Data
- Layer 7
  - Service Logs
  - Packet Capture, IDS alerts

**NSM Event Collection Points and Formats**
![enter image description here](https://i.imgur.com/rQZggky.png)

## Why we need NSM?

You can read this article [Link](https://pchtechnologies.com/why-do-i-need-network-security-monitoring-for-my-network/)


## Endpoints
Also with Endpoints Monitoring we should put some Questions to answer.

The Questions Are:
- Has anyone installed unauthorized program?
- What Ports are listening and why?
- What exploits are you vulnerable to?
- Have any system files been changed? 
- Have any malicious scripts been run.?
 
 You should be noticed we're talking about Computers, Clouds, Servers

 **So how do we get the answer?**

Here comes **CSM's**  role and it stands for **Continuous Security Monitoring** or you can call it **ISCM** as [NIST](https://csrc.nist.gov/) definition, so what is it?

## **What is the Continuous Security Monitoring**?

**Continuous Security Monitoring (CSM)** is a **strategy** that **automates the process** of continuously **checking and evaluating your operational security**. The idea behind this approach is to enable you to identify vulnerabilities and fix them before cybercriminals exploit them.

Also you can read the Definition of [NIST](https://csrc.nist.gov/glossary/term/information_security_continuous_monitoring)

## **What are the benefits of CSM?**

- it is looking at endpoint data -- "data at rest" or the data being generated on the endpoint
- Provides real-time visibility  into your applications and infrastructure
- Vulnerability scanning
- File/Registry integrity monitoring
- Autoruns
- Services
- Running process
- Classifies devices:  to allow you to implement preventive measures

## CSM Event Collection

**Here are the CSM Event Collection Sources:**

- OS/Application auth logs
- Sysmon
- Antivirus
- EDR
- Whitelisting
- HIDS/HIPS
- Vulnerability Scanner

![LogsToSIEM](https://i.imgur.com/cI300o2.png)

## **How Does CSM Work?**

Continuous monitoring solutions work by providing real-time information about an organization's [security posture](https://www.upguard.com/blog/security-posture). According to the National Institute of Standards and Technology's white paper [NIST SP 800-137](https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-137.pdf), information security continuous monitoring (ISCM) works by

-   Maintaining situational awareness of all systems across the organization and its vendor ecosystem
-   Maintaining an understanding of threats and threat activities
-   Assessing all security controls
-   Collecting, correlating, and analyzing security-related information
-   Providing actionable communication of security status across all tiers of the organization; and
-   Active management of risk by organizational officials.
-   Integration of information security and risk management frameworks.

The NIST Cybersecurity Framework breaks down the entire process into the following core components:

-   Identification
-   Protection
-   Detection
-   Response
-   Recovery

## Why we need CSM?

Investigations will require **network & endpoint data**

For Example: Malware Infection occurs

- Traffic is generated to an IP on port 443

- While investigation with network data maybe you will see the bad IP or the bad domain for example..?

but what if you know that these processes created it
![enter image description here](https://i.imgur.com/8RabcTG.png)

- now you see the process tree **calc.exe | PID: 2092** and this calc.exe start **cmd.exe** of course this is not looking good?
- now we identified that this a persistence technique also now we know where is the file on the drive.

## Monitoring Data Sources Table

| NSM Data  | CSM Data  | 
|---|---|---|
|  Routers & Switches | Authentication | 
|  Network Firewalls | Antivirus | 
|  IDS & IPS | HIDS & HIPS | 
|  Proxy | Process CommandLine | 
|  WAF | Data Loss Prevent (DLP) |
|  Service Logs: FTP,SSH,HTTP(S),etc.    |   Vulnerability Scanners  |
 |                                       | Application access logs
 |                                       | Executables	


**Finally there is a one place to search and alert on events is your SIEM**

![enter image description here](https://i.imgur.com/7Wu2hFs.png)

## BOUNS

How Data Gets to The SIEM

This a small photo shows how (NSM) AND (CSM) are working with SIEM

![enter image description here](https://i.imgur.com/klALzkb.png) 


Resources I Used:

1. [SANS](https://www.sans.org) --

2. [logrhythm](https://logrhythm.com/) --

3. [NIST](https://www.nist.gov/) --

-- Thanks For Reading..
