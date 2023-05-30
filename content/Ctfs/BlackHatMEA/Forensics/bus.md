---
title: "BlackHatMEA | Bus"
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
description: "Solving Bus Forensics Challenge."
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
    alt: "Bus" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
---

> Challenge Name: Bus

>Points: 150

![enter image description here](https://miro.medium.com/max/640/1*Vcbfovigm3SEdluqzHkBog.png)


The Challenge was a [ **PCAP File** ], hmm don't like to analyze these types but it's okay let's dive in!

First thing let's open it in **Wireshark** and see the traffic.

![enter image description here](https://media.discordapp.net/attachments/973549672608186398/1025883150280310826/unknown.png)

as usual messy traffic xd, let's take a look at traffic that look at modbus protocol there’s nothing interesting in this protocol except the **Data** section.

![enter image description here](https://media.discordapp.net/attachments/973549672608186398/1025884061039853658/unknown.png)

i displayed them as a **Column** to make things more clear to me

![enter image description here](https://media.discordapp.net/attachments/973549672608186398/1025884896129974312/unknown.png)

Data are `ff00 or 0000`
`0000` is represents **0** and `ff00` represents **1** Like Signals 

so i used `tshark` to extract all the Data

> tshark -r bus.pcap -T fields -e modbus.data -Y "modbus.data != 0 and
> tcp.dstport == 502" > bus.txt


by replacing every 0000 and ff00 to there 0 and 1 value i got the following

    011110010110111101110101011100100010000001000110010011000100000101000111001000000110100101110011001110100010000001001101011011110110010001100010011101010111001101011111011010010111001101011111011001010110000101110011011110010101111101100001011001100111010001100101011100100101111101100001011011000110110000100001



 Great!, it's a binary data, convert it  [**CyberChef**](https://gchq.github.io/CyberChef/) .

![enter image description here](https://media.discordapp.net/attachments/973549672608186398/1025888809629532240/unknown.png)


> Flag: BlackHatMEA{Modbus_is_easy_after_all!}

![enter image description here](https://miro.medium.com/max/1400/1*_nWlEGA12PRqerHc81l6IQ.png)

Thanks For Reading