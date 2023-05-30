---
title: "New Phishing Technique"
date: 2023-01-20T03:32:43+02:00
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
    image: "https://www.ncsc.gov.uk/images/Phishing-vector%20-%20Copy.png" # image path/url
    alt: "Phishing" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
---
Hello folks, I will talk about nowadays technique that (spammers) use to scam the victims and get their Bank OTP-Code

from several years websites were using (2D Payment Gateway) because (2D Payment Gateway) processes payments after cardholders enter their personal card information along with the CVV, the connection is between the (Buyer) and (online seller).

after (3D Payment Gateway) came, most of the websites started to use it because it's similarly to a 2D payment gateway, but with an extra verification step that improves its security. An OTP (one time password) is generated before the amount is deducted from the card holder’s bank account.

So when the (spammers) steal your credit card they will face an obstacle while they purchasing something from websites that require (OTP-Code). so how they will override this obstacle.
they are using (Voice Services API) like, Twilio, sinch, plivo, messagebird and Telnyx to make an OTP-BOT scripted by python or any other language like Nodejs and they host their bot on telegram to send commands and receive OTP-Codes.

So in this demo (btw it's a real demo from a spammer's group) one of them is showing his bot that calls victims as it from the bank and ask for the (OTP-Code), to enter it in the verification page while he is purchasing something or maybe getting the money out somehow.

[![Demo](https://i.imgur.com/ZQG4sQV.png)](https://dms.licdn.com/playlist/C4D05AQFKf8YmhH7F9w/mp4-720p-30fp-crf28/0/1672511962991?e=1683165600&v=beta&t=BzuZbdJAUOA36XDS72AII7ShKFdgXvGeaEbZD2fLgPI "OTP-BOT Demo")

Basically, this technique involves in 2 parts

## Part 1 / Hunt for targets

To begin with, the attackers require a target, hence they initiate phishing campaigns to reach their desired victims. They obtain email addresses of individuals who have accounts on popular e-commerce platforms like PayPal, Amazon, Apple, and the like by using dorks to locate SQL injection vulnerabilities specifically in shopping websites. A SQL Vulnerability scanner is then employed to identify vulnerable websites, which the attackers then exploit to extract customer email addresses. They utilize a tool called "Checker" that connects to an endpoint to validate whether the victim email is registered with the targeted company such as PayPal, ensuring that the victim does indeed have an account with the targeted platform. The attackers also gather email addresses by keeping track of any new site leaks and downloading the leaked data. Once they obtain credit card details, they move on to part two.

## Part 2 / Building The BOT
Once the attackers acquire the victim's information, they create an OTP-Bot. The structure of the Bot is fairly straightforward, and they use Python or Nodejs to develop it. The choice between Python and Nodejs depends on whether the Bot will be hosted on Telegram or Discord. Python is used for Telegram, while Nodejs is used for Discord. The Bot's structure consists of a sqlite3 database file and Voice Scripts. The database serves the purpose of identifying which users and admins have access to the Bot, as well as subscriptions. The Voice Scripts, on the other hand, are the messages that the Bot will deliver to the victim. Commonly used voice scripts are typically available in both English and French.

Some samples of the Discord OTP-BOT's structure and commands have been included for reference.

#### Available Voices
![[]](https://i.imgur.com/1Rs1GKZ.png) 

#### Voices.mp3
![[]](https://i.imgur.com/A3LGVxP.png)

#### Config file

![[]](https://i.imgur.com/Se7m94m.png)


– Thanks For Reading