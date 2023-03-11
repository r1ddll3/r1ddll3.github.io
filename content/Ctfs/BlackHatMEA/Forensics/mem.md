---
title: "BlackHatMEA | Mem"
date: 2022-10-02T00:04:34+02:00
draft: true
tags: ["CTFS", "Forensics", "BlackHatMEA Qualifications-2022"]
author: "@1nk0x01"
# author: ["Me", "You"] # multiple authors
showToc: false
TocOpen: false
draft: false
hidemeta: false
comments: true
description: "Solving Mem Forensics Challenge."
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
    image: "https://miro.medium.com/max/640/1*Vcbfovigm3SEdluqzHkBog.png" # image path/url
    alt: "Mem" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
---

> Challenge Name: Mem

>Points: 250

![enter image description here](https://miro.medium.com/max/640/1*C-9kjkpTtnm-t03tyvC6SA.png)


The Challenge was a [ ****RAW** file** ],

it is a memory dump file, so our hero for this chall will be [ **Volatility** ]


First thing as usual let's start with the basic vol command

but i use vol3 so maybe you will notice the command is not like yours


![enter image description here](https://media.discordapp.net/attachments/973549672608186398/1025892613951344700/unknown.png)

nothing useful i know but it just our routine while analyzing :D

so our desc is saying that we are looking for a file, hmm let's fire a scan for all the files 

![enter image description here](https://miro.medium.com/max/720/1*AH8Pe2-lzmKuFD7-qDy0ZA.png)

i have extracted it and it is has a flag.txt but protected with a password

so this what desc said about it we need this password to get our flag

after doin some analyze on the memory, process i noticed that the challenge said password stored locally so let's dive into windows.envars

by the following command 

    python3 vol.py -f ../mem.raw  windows.envars.Envars > vars.txt

![enter image description here](https://media.discordapp.net/attachments/973549672608186398/1025895806265466990/unknown.png)

    300     csrss.exe       0x2e1930        SystemP Ittm1Fc7hcuFrLZIQmxs


Bingo! This our Password **Ittm1Fc7hcuFrLZIQmxs**

![enter image description here](https://media.discordapp.net/attachments/973549672608186398/1025896169001463899/unknown.png)


> Flag: BlackHatMEA{Password_hints_are_the_retrievable}

![enter image description here](https://miro.medium.com/max/1400/1*_nWlEGA12PRqerHc81l6IQ.png)

Thanks For Reading