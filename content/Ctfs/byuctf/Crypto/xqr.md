---
title: "BYUCTF | XQR"
date: 2022-05-28T11:51:34+02:00
draft: true
tags: ["CTFS", "BYUCTF", "Cryptography"]
author: "@R1ddl3"
# author: ["Me", "You"] # multiple authors
showToc: false
TocOpen: false
draft: false
hidemeta: false
comments: true
description: "Solving XQR Cryptography Challenge."
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
    alt: "XQR" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
---

#### Me (@R1ddl3) and (0x3ashry) solved this challenge together


## Challenge

![enter image description here](https://i.imgur.com/ewHFSkd.png)



## Solution

XQR was a hard rated cryptography challenge and it was in a whole another level.  


It doesn’t contain except one massive image contain thousands of QR Codes

![massive-view](https://i.imgur.com/47hFTA0.png)

I first tried to read the first QR Code but it gave me `85TK6eDfb{SXQfvR70VXX` !!!

then i asked my friend to help me with any idea,

Through trials and errors we got that the size of each QR code is 27 pixels length and width, 
so we thought that cutting the whole image into smaller QR codes would help us to scan them

we made a python script to automate that.


    from PIL import Image

	imggg = Image.open('xqr.png')

	inc = 27

	for i in range(0, 2727 , 27):

	    for j in range(0, 2727, 27):

	        box = (j, i, j+27, i+27) # left, top, right, buttom

	        img2 = imggg.crop(box)

	        img2.save(r'QRCodes/myimage_' + str(i) + '_' + str(j) + '_cropped.jpg')



Now we have 10,201 QR Codes stored in folder called **QRCodes**, And we tried to scan them but wasn't useful so we took a break for a while to think…

Then my friend realized from the name of the challenge that **XQR** is near to **XOR** so what if we `XORed` all the **QR Codes** together…

we started with reading them using cv2 library from python-opencv and then in order to make our trick work

we changed the readed image to binary 0 and 1, black and white pixels. Then XORed each pixel with the same pixels in all the other 10,201 qr codes and saved it, Then displaying the final result:

Our Python Code:

	import cv2

	import matplotlib.pyplot as plt

	import os

	  
	imggg = Image.open('xqr.png')

	inc = 27

	for i in range(0, 2727 , 27):

	    for j in range(0, 2727, 27):

	        box = (j, i, j+27, i+27) # left, top, right, buttom

	        img2 = imggg.crop(box)

	        img2.save(r'QRCodes/myimage_' + str(i) + '_' + str(j) + '_cropped.jpg')

	  

	QR_dir = os.listdir(r"QRCodes")

	qr_codes = []

	for qr in QR_dir:

	    gray = cv2.imread("QRCodes/" + qr, cv2.COLOR_BGR2GRAY)

	    _, binary = cv2.threshold(gray, 150, 1, cv2.THRESH_BINARY_INV)

	    qr_codes.append(binary)

	  

	for i in range(27):

	    for j in range(27):

	        for q in range(len(qr_codes)):

	            if q+1 == 10201:

	                break

	            qr_codes[0][i][j] =  int(qr_codes[0][i][j] != qr_codes[q+1][i][j])

	  

	plt.imshow(qr_codes[0])

	plt.show()


![!\[\[XQR_2.png\]\]](https://i.imgur.com/QudLKOI.png)

Scanning it…

**Bingo !!! We got the flag** 

> Flag: byuctf{x0r_i5_u5eful}

Thanks For REading..







