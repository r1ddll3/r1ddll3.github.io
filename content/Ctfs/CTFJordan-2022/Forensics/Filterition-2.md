---
title: "CTFJordan-2022 | Filterition-2"
date: 2022-09-30T11:51:34+02:00
draft: true
tags: ["CTFS", "Forensics", "CTF Jordan Qualifications-2022"]
author: "@R1ddl3"
# author: ["Me", "You"] # multiple authors
showToc: false
TocOpen: false
draft: false
hidemeta: false
comments: true
description: "Solving Filteration-2 Forensics Challenge."
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
    alt: "Filterition-2" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
---

> Challenge Name: Filterition-2

>Points: 200



#### Let's get started, given a (“pcapng”) so let's take a overall look first and get in deep later.

![pcap-view](https://i.imgur.com/Tr2oQnp.png)

messy requests :D | but the name of the challenge is **Filterition**

so i have to filter the requests 

i started filtering the requests, started with **dns** requests but nothing was interesting.
i took a look at **tcp** requests and i couldn't see the requests well so i thought that there is nothing useful :D

now time to check the ftp requests using this wireshark filter ( **ftp-data** ) and there i got a very interested thing.

![ftp-data](https://i.imgur.com/mEauVD5.png)
it is a zip file cool let's dig in..
i exported the file.
now i have a zip file looks interesting but it is protected with password :( | ofc i will brute force it .
i used zip2john to crack the password |

![zip2john](https://i.imgur.com/GKIVady.png)

the password is : **labeba**
BoOoOM am done :*

sry but nope i got file named secret_data.txt contains some codes

actually i have no clue what are they :(

![no-clue](https://i.imgur.com/Gny9UKr.png)
  
  ![what??](https://www.clipartmax.com/png/full/316-3163854_one-ohio-man-has-no-clue-whats-going-on-in-the-world.png)

i copied one random code and pasted it to google and i figured that those codes are RGB Codes and i noticed that also from the Name of the pcap file ( **colurfull.pcapng** )

now i need a way to convert those RGB Codes to image to be able to see the flag, it was an easy thing for me cause i solved chall like these before 

so i made a little python script to take all RGB Colors and convert it to image like magic :D


    from PIL import Image
    w,h = 289, 500
    rgbFile = open('secret_data.txt', 'r')
    data = rgbFile.readlines()
    rgblist = []
    
    for v in data:
        j = v.strip()
        k = v.split("-")
        rgb = (int(k[0]),int(k[1]),int(k[2]))
        rgblist.append(rgb)
        
    im = Image.new("RGB", (w, h))
    im.putdata(rgblist)
    im.save("flag.png")
    print("Bingo!")
    
    
 
i made the width 289 based on the trials i did so i figured that the best width to show the flag correctly \o/

and finally i got the flag

![Flag](https://i.imgur.com/5PIY88O.png)

> JISCTF{EXF1LT3R4T3D_D4T4_1N_1M4G3_F1L3}

Thanks For Reading..


