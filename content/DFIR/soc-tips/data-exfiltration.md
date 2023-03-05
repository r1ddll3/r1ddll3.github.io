---
title: "Spotting Data Exfiltration"
date: 2022-10-21T00:04:34+02:00
draft: true
tags: ["SOC", "Data Exfiltration"]
author: "@R1ddl3"
# author: ["Me", "You"] # multiple authors
showToc: false
TocOpen: false
draft: false
hidemeta: false
comments: true
description: "How to Detect Data Exfiltration."
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
    image: "" # image path/url
    alt: "Data Exfiltration" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
---


Hey folks, Today we will talk about how to Spot Data Exfiltration

Let's Dive in!!

---------

First of all we should know what is data exfiltration. according to [MITRE ATT&CK®](https://attack.mitre.org/) Data Exfiltration is the Step when The adversary is trying to steal data may use to steal data from your network.

This could be done over Web Service, over USB, over Cloud Storage, Emails and many more, you can read more about it [Resource](https://attack.mitre.org/tactics/TA0010/)

First i left you some samples of how the exfiltration done with some of Exfiltration Methods not all of course but i will leave you more sources to dig deep into the topic.

### Exfiltrate via HTTP


![enter image description here](https://blog.apnic.net/wp-content/uploads/2022/03/Figure-3-PowerShell-code-for-HTTP-POST-from-victim-host-plain.jpg)


### Exfiltrate via SMTP

SMTP is one of the most common methods for data exfiltration. Several malware programs exfiltrate the stolen information to an attacker-controlled SMTP server. For example [Agent Tesla](https://blogs.blackberry.com/en/2020/04/threat-spotlight-secret-agent-tesla) is a Windows-based keylogger and Remote Access Trojan (RAT) commonly uses SMTP to exfiltrate stolen data.

Attackers can use the following PowerShell code to send an email with an attached file (stolen data) to exfiltrate a remote address:


![enter image description here](https://blog.apnic.net/wp-content/uploads/2022/03/Figure-8-Victim-host-send-stolen-data-to-attacker-control-email-box-using-SMTP--1024x80.jpg)


![enter image description here](https://blog.apnic.net/wp-content/uploads/2022/03/Figure-9-Exfiltrate-data-delivered-to-attacker-email-box-1024x361.jpg)

**Stream**
![enter image description here](https://blog.apnic.net/wp-content/uploads/2022/03/Figure-10-SMTP-streams--1024x468.jpg)

### Exfiltrate via DNS

Since DNS is not a transport protocol, many organizations don't regularly monitor the DNS protocol! The DNS protocol is allowed in almost all firewalls in any organization network. For those reasons, threat actors prefer using the DNS protocol to hide their communications.

The DNS protocol has limitations that need to be taken into consideration, which are as follows,

- The maximum length of the Fully Qualified FQDN domain name (including .separators) is 255 characters.
- The subdomain name (label) length must not exceed 63 characters (not including .com, .net, etc).

Based on these limitations, we can use a limited number of characters to transfer data over the domain name. If we have a large file, 10 MB for example, it may need more than 50000 DNS requests to transfer the file completely. Therefore, it will be noisy traffic and easy to notice and detect.

- The attacker registers the domain name ZG5ZC2VJDXJPDHKK.COM, and sets up name server NS1.ZG5ZC2VJDXJPDHKK.COM
- The infected client encodes stolen information, in this case, the text `Pa$$w0rd`, into UGEKJHCWCMQK
- The client makes the DNS query for the domain with the encoded password as a subdomain: UGEKJHCWCMQK.ZG5ZC2VJDXJPDHKK.COM
- A recursive name server finds the authoritative name server NS1.ZG5ZC2VJDXJPDHKK.COM and sends the query there.
- The attacker recognizes the subdomain value as the encoded password. The attacker decodes the information UGEKJHCWCMQK back to recover `Pa$$w0rd`

Diagram:
![](https://infoblox.b-cdn.net/wp-content/uploads/dsrc-dns-issues-threats-how-does-data-exfiltration-work.jpg)


![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5d617515c8cd8348d0b4e68f/room-content/a7ac15da0501d577dadcf53b4143ff98.png)

Then the attacker receives the encoded data and decode it to get the sensitive data.


### Exfiltrate via DNS Tunneling

DNS tunneling is a difficult-to-detect attack that routes DNS requests to the attacker's server, providing attackers a covert command and control channel, and data exfiltration path.

The Client has a Firewall, IDS and proxies that are inspecting and blocking the susp traffic so how can they move the data?

Yes, they will abuse the DNS Protocol to create a covert channel and exfiltrate the sensitive data out.


So How this works:

- The Attacker established a domain with local DNS Server.
- Attacker Will try to query his DNS server from the client machine
- so what happens is when the client tries and goes to this website it will passed through local DNS and this DNS Server probably doesn't know the IP Address of the attacker's website so it will query this website and ask for the IP Address of it and the website will respond with the IP Address.
- since the queries are just packets so the attacker can manipulate it
- the attacker puts the sensitive data into the query and send it splitted so he won't get caught.
- and finally attacker receive it and reconstruct it and get his sensitive data 



### Exfiltrate via IPv6
 ![enter image description here](https://blog.apnic.net/wp-content/uploads/2022/03/Figure-22-IPv6teal-sender-script-running-on-victim-host--1024x90.jpg)
 shows the ‘IPv6teal receiver script’ running on the attacker-controlled machine; it is trying to listen and capture the targeted data:
 ![enter image description here](https://blog.apnic.net/wp-content/uploads/2022/03/Figure-23-IPv6teal-receiver-script-and-related-streams--768x275.jpg)

### You Will Find More Examples: [exfiltration-attacks](https://blog.apnic.net/2022/03/31/how-to-detect-and-prevent-common-data-exfiltration-attacks/)

## Detecting Data Exfiltration

so we are talking about transferring data so first thing is to check the volume of the data that being transfer over your network


- Monitor **High-Volume DNS tunneling** or **High-Volume Traffic being from unusual source but it is not should be 100% with high-volume.**

- a connection to unknown destination (C2) maybe

- Also, you have to check Process Creation Logs, maybe they compressed archive especially from CLI with password or 7z, WinRAR

- Pay attention to [**DLP**](), **UEBA alerts**
	the following file types to bypass DLP so take care:
	-   Plain Zip
	-   Password protected (AES) Zip
	-   Deeply nested Zips (many systems will stop scanning after 10-100 to avoid Zip Bombs)
	-   7zip
	-   RAR
	-   CAB
	-   Tar (+/- gzip)
	-   WIM image


- check multiple port firewall denies outbound from a single source

- Complex URLs or Unexplained URLs with long parameters
```
http://ooo.nu6tgnzvgm2tmmbzgq4a.rkgo---redacted---tw5.5z5i6fjnugmxfowy.beevish.com/xml.php?c=0&t=x&k=.txt&type=0&s=3500&n=example.txt
```

- They use Complex URLs to exfiltrate they data just to make you a bit blind or confused about the URL you will think a safe URL with params just like Microsoft URLs it has a long parameters but in fact they maybe carrying out some data

- **Monitoring for outbound traffic patterns**:- as malware needs to regularly communicate with C2 servers to maintain a consistent connection. Continuous monitoring provides opportunities to detect data exfiltration with common protocols such as HTTP:80 or HTTPS:443. It’s worth keeping in mind that some advanced malware randomize delays between C2 communications.



- **Keeping an up-to-date log of all approved IP addresses connections to compare against all new connections:** Along with this, it’s advised to keep an eye out for large data flows to unexpected IP addresses and major spikes in anomalous outbound traffic.

-    **Block unauthorized communication channels**: First, disable all unauthorized communication channels, ports and protocols by default, and re-enable on an as-needed basis.
- **Data Loss Prevention (DLP)**: Data loss prevention (DLP) is a strategy for detecting and preventing data exfiltration or data destruction. Many DLP solutions analyze network traffic and internal "[endpoint](https://www.cloudflare.com/learning/security/glossary/what-is-endpoint/)" devices to identify the leakage or loss of confidential information. Organizations use DLP to protect their confidential business information and [personally identifiable information (PII)](https://www.cloudflare.com/learning/privacy/what-is-pii/), which helps them stay compliant with industry and [data privacy](https://www.cloudflare.com/learning/privacy/what-is-data-privacy/) regulations.
---

Resources I used for this Article:

1. [attack.mitre.org](https://attack.mitre.org/)
2. [blog.apnic.net](https://blog.apnic.net/)
3. [www.sans.org](https://www.sans.org/)

-- Thanks For Reading.

