---
title: "Raidforums Leak"
date: 2023-05-30T14:25:15+02:00
draft: true
tags: ["Threat Intel", "Hacking Forums"]
author: "@R1ddl3"
# author: ["Me", "You"] # multiple authors
showToc: false
TocOpen: false
draft: false
hidemeta: false
comments: true
description: "Raidforums Database Leak!"
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
    image: "https://th.bing.com/th/id/R.d88c0b680e06852adfdc19f31e530f7b?rik=g5Oa13zG5ILlzQ&pid=ImgRaw&r=0" # image path/url
    alt: "Raidforums" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
---
Hey folks, in this month, a hacking forum known as "Exposed" has gained significant attention. Yesterday, the administrator, named **Impotent**, leaked a `RaidForums` database. This forum(Exposed) has been actively trying to be similar as Breached community in an aggressive manner, so far by attacking two other competing forums. This forum also has feature that `Breached`  didn't have, such as `ransomware` section. The leaked data includes users registered between 2020/2021. It should be noted that Impotent mentioned the removal of certain users without providing any explanation. Additionally, the source of the leak was not disclosed.

![enter image description here](https://i.imgur.com/dnd7xL4.png)

## More about Exposed
The Exposed forum was launched on May 9, 2023, with an advertisement on Twitter. However, the publisher restricted the visibility of the tweet posted by `Trlstan Wille` `https://twitter.com/D4RKR4BB1T47/status/1655821904979034112`. The forum was also promoted on Telegram under a different name, which we now know as `Impotent`, who is the admin of the forum. `Impotent` initially began sharing the forum on Twitter.

![enter image description here](https://i.imgur.com/wDQAqBv.png)

Subsequently, he transitioned to Telegram channels to promote and expand his forum.

**This first message was sent on May 9, 2023**

![enter image description here](https://i.imgur.com/ttChjyS.png)

![enter image description here](https://i.imgur.com/UmQXWMm.png)

### Back to Raidforums leak
The leaked data consists of a single SQL file containing a users table named `mybb_users`, which holds information for over 478,000+ users. 

![enter image description here](https://i.imgur.com/tyeczUg.png)

Also, old RaidForums members have verified that their information is indeed present in the leaked database, confirming its legitimately. The table contains information such as:

```
usernames, email addresses, hashed passwords, registration dates and much more
```
![enter image description here](https://i.imgur.com/AcAgHN0.png)

![enter image description here](https://i.imgur.com/8mlnXH3.png)

  
Although it is probable that law enforcement has obtained the database following the seizure of the forum, the leaked data remains valuable for security researchers. These researchers often construct profiles of threat actors, and the leaked registration information can contribute to their efforts. By analyzing this information, researchers can gain insights into the threat actors and potentially establish connections to other malicious activities.


### Conclusion

|   |   |   
|---|---|---
| Leaked site  | raidforums.com  |   
| Posted on  | exposed forum |
|Post date|5/29/2023 05:15 PM|
|   Posted by|  Impotent        |
| Leak Source | Unknown|  
|Admin telegram|@ImpotentDude|
|File Link|https[xx]//files[.]doxbin[.]gg/pcZQOWsY.rar|
|File name| raidforums.com.sql (Table: mybb_users)|
| File Hash  | 86156c7db10dc6f7b4257da50a01fa37 (MD5)  |