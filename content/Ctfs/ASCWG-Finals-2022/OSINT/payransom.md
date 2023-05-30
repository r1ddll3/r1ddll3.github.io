---
title: "ASCWG-Finals-2022 | OSINT"
date: 2022-09-21
# weight: 1
tags: ["CTFS", "OSINT", "ASCWG-Finals-2022"]
author: "@R1ddl3"
# author: ["Me", "You"] # multiple authors
showToc: false
TocOpen: false
draft: false
hidemeta: false
comments: true
description: "Solving Arab Security Wargames 2022 OSINT Challenge."
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
    image: "https://i.imgur.com/JDMKgGd.png" # image path/url
    alt: "Pay Your Ransomware" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
---


> Challenge Name: OSINT - Pay Your Ransom

>Points: 600

> Level: Medium

> Description: 
 **One of our customer's computers was infected with ransomware, but we were unable to determine the ransomware family. Because of this, we have uploaded the ransom note to you in the hopes that you will be able to assist us in determining the ransomware family and discovering the key to decrypting and restoring the data.**


#### So let's get started....

while i was solving a Web Challenge my team were solving this challenge 

but they called me when they stucked in a Github Site .[drvirux0.github.io](https://drvirux0.github.io/Pay-Your-Ransom/ASCWG-RANSOM-NOTE.html), after i came i saw this blue screen from the github repo and it has a pastebin link and Base64 encoded

![Github ScreenShot](https://i.imgur.com/uZ4aOdF.png)

actually this a ransomware ran on a PC, nevermind let's investigate.. i saw the source code and i notiaced an html comment `<!-- this is and base64 megan35 algorithm -->` so i used cyberchef ofc to decode it and i got this result

![enter image description here](https://i.imgur.com/Uo4y343.png)

i went to this pastebin link .[Pastebin](https://pastebin.com/JE8sB3eT) but its protected with a password BTW the email that was mentioned in github was useless, but let's continue.. i went back to github site after i got pastebin link and i readed it with focus and i noticed this sentence ```
```
when you pay you will get your TLSH hash please submit it here to get your secret : https://pastebin.com/JE8sB3eT.

```

this the same link from previous encoded :) but the important part was mentioned that i need to get something called **TLSH hash** to be able to use it as a password to un-lock the pastebin.

hmm, how do i get it then and i dunno even how to start look for it, so i decided to make a steps i follow like a sequence for me


**1- i need to know the name of this ransomware**

**2- once i know the name, i need to figure out how can i get the TLSH hash**


my friends were trying in different ways but they all failed, but i got an idea, i took a screenshot for the ransomware without showing anything but the message and i searched in google image hopefully find anything interested. ![enter image description here](https://i.imgur.com/JDMKgGd.png)

i got a tweet that has the same screenshot of the ransomware .[Twitter](https://twitter.com/marcelorivero/status/1134526512923840512)

![enter image description here](https://i.imgur.com/Zt5Phvt.png)

So now **i have the name of this ransomware  ( chacha ) and the MD5 hash**, next step is looking in **Virustotal** using this **MD5 hash** :* and i found there is a malware exists |_^:^_|

![enter image description here](https://i.imgur.com/duJYBZo.png)

[Virustotal Result](https://www.virustotal.com/gui/file/3885589a3c94d0475a6d994e4644e682f4cff93f8b4d65f37508ffe706861363/) 
 now i need to get the **TLSH Hash**, by going to the Details section i got what i want 

![enter image description here](https://i.imgur.com/WzVbMDN.png)

i went to pastebin as fast and i typed it and i got message password should contain at most 64 chars, wait what!!!! WT,F is going on

![enter image description here](https://i.imgur.com/9AUrXIN.png)

i got an idea to split the TLSH Hash and get the first 64 Characters only using a little Python script

```python-code
string="T1CAA402127AE7A0B1D8BB427359648E964B3EFE654F218EC733C8464D06B56C05B32F63"
print(string[:64])
```

and it worked, hell yeah ! and this what was inside

![enter image description here](https://i.imgur.com/jCFHTbH.png)

The Message says:

```pastebin-ulock
https://pastebin.com/uyg8hdhY

Please take note that this ransomware generates 
a database file with the name foo. db this file 
has SHA-1 hash, and in order for you to open the bin that was mentioned earlier, you will need to obtain this hash.

```

##### Another Puzzle

so let's get deeper, ofc this second pastebin was protected too but the message says ransomware generates a db file with name foo.db and the sha-1 of this file/db will be the password for the flag so i went back to virustotal looking for any something that related to this db and i got something in behavior section 

![enter image description here](https://i.imgur.com/hFtV6ca.png)

there are dropped files hmmm this what i'm looking for... i opened Dr.Web to see to these files.

![enter image description here](https://i.imgur.com/MNzhr3t.png)

![enter image description here](https://i.imgur.com/or6pkxb.png)

**db file is there and the SHA-1 too cool**

i used it as a password and i finally got the Flag

![enter image description here](https://i.imgur.com/zbU8xKk.png)


> FLAG: ASCWG{V1rUs_7Ot4L_$UPeR_5aYaN}
