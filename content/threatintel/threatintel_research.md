---
title: "Threat Intel Research"
date: 2023-04-20T04:53:31+02:00
draft: true
tags: ["Threat Intel", "Phishing"]
author: "@R1ddl3"
# author: ["Me", "You"] # multiple authors
showToc: false
TocOpen: false
draft: false
hidemeta: false
comments: true
description: "Identify New Phishing Technique"
disableHLJS: true # to disable highlightjs
disableShare: false
hideSummary: false
searchHidden: false
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
UseHugoToc: true
cover:
    image: "https://i.imgur.com/q6VNo66.png" # image path/url
    alt: "Phishing" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
---
Hey folks, During a recent threat intelligence research, I discovered concerning findings regarding website security. Specifically, I uncovered that 1,200 websites are being compromised and used for phishing campaigns and also most of them being leaked every 4-6 days, with a majority of 60% being published as FTPS access. Furthermore, sensitive credentials from numerous companies, institutes, and even governments were also found to be leaked, including endpoints that may not have been accessible through typical reconnaissance measures, such as internal VPN access and employee portals. The attackers used (info stealers), and unfortunately, many of the leaked credentials are still valid. Shockingly, many of these endpoints do not even utilize two-factor authentication.

It is clear that many companies lack proper security awareness, as there needs to be a heightened sense of mistrust towards employee activity, and mentors should educate all employees on the dangers of phishing and how to avoid it. This is not just for non-security employees, as I also discovered leaked credentials for those working in security companies.

Lastly, I came across a leak containing the personal information of approximately 10,000 individuals who were scammed. This information, including (credit card details, emails, IDs, and SSNs).

The top targeted entities during these attacks were financial institutions like (Citi Bank, Bank of America and USAA Bank also south Africa banks), as well as shipping companies such as (DHL) and the (Post Office) service.

## Samples

#### IDs Leak
This leak contains 60 ID CARDS WITH SELFIE For People who were scammed.

![[]](https://i.imgur.com/q6VNo66.png)

#### Credit Card Leak
This leak contains 10,000 individuals who were scammed
![[]](https://i.imgur.com/ng5hGIq.png)

#### Credentials Leak
This leak contains sensitive credentials from numerous companies, institutes, and even governments such as (Vodafone, Etisalat, Brazil Government, Customers for BanqueMisr, su.edu.sa and many more)
![[]](https://i.imgur.com/v0SHwTz.png)
![[]](https://i.imgur.com/l0hSCu8.png)

#### Compromised Sites leak
This leak contains 4,600 compromised Website & FTPS access.
![[]](https://i.imgur.com/6eMvnNx.png) 

### Conclusion

last thing it is crucial that companies ensure their threat intelligence teams are proactively monitoring for breaches and that employees are educated on how to avoid falling prey to scams and phishing attempts.

- Thanks For Reading..