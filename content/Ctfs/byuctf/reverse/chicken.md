---
title: "BYUCTF | Chicken"
date: 2022-05-28T11:51:34+02:00
draft: true
tags: ["CTFS", "BYUCTF", "Reverse"]
author: "@R1ddl3"
# author: ["Me", "You"] # multiple authors
showToc: false
TocOpen: false
draft: false
hidemeta: false
comments: true
description: "Solving Chicken Reverse Challenge."
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
    alt: "Chicken" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
---


# Chicken - REverse-Engineering
#### =====================



>Description: So I tried learning a new sorta-language, but I'm not very good at it and don't think I used it right. Can you check for me?


Challenge is a file named **chicken.chn** i opened it in VSCode

![!\[\[chickenwords.png\]\]](https://i.imgur.com/7MvVZUG.png)

   Opps, i don't know what is this chicken lol?..

   so google is my friend atm, after searching in different ways i found that chicken esolang known as (shockingly) [Reference](https://esolangs.org/wiki/Chicken).

   each line has the word "chicken" written a certain number of times.

   and that means when count the number of chicken on each line you will

   get a something called opcode Nvm Skip this part let's get into our missions

  

 1. i searched for tool that can translate those lines to me

   automatically and i found a tool on github:

   [GithubTool](https://github.com/kosayoda/chickenpy)

![!\[\[Capture.png\]\]](https://i.imgur.com/VrNPPBf.png)

  it translates the lines to be easier to read after i ran the tool and

  got the result it was kinda easy to me now to read it and extract the flag
   <h3>Output:</h3>
		
	chickenpy.VM - Storing 's' to 35
	
	chickenpy.VM - Storing '3' to 15

	chickenpy.VM - Storing '' to 12

	chickenpy.VM - Storing 't' to 7

	chickenpy.VM - Storing 'ˡ' to 24

	chickenpy.VM - Storing '' to 36

	chickenpy.VM - Storing 'e' to 19

	chickenpy.VM - Storing '0' to 23

	chickenpy.VM - Storing 'z' to 46

	chickenpy.VM - Storing 'n' to 33

	chickenpy.VM - Storing 'w' to 22

	chickenpy.VM - Storing '3' to 17

	chickenpy.VM - Storing '3' to 11

	chickenpy.VM - Storing '' to 40

	chickenpy.VM - Storing 'a' to 45

	chickenpy.VM - Storing '0' to 30

	chickenpy.VM - Storing 'f' to 5

	chickenpy.VM - Storing 'r' to 14

	chickenpy.VM - Storing 'l' to 31

	chickenpy.VM - Storing 'n' to 20

	chickenpy.VM - Storing '1' to 41

	chickenpy.VM - Storing '3' to 9

	chickenpy.VM - Storing '3' to 26

	chickenpy.VM - Storing 'y' to 1

	chickenpy.VM - Storing '4' to 13

	chickenpy.VM - Storing 'c' to 3

	chickenpy.VM - Storing '}' to 49

	chickenpy.VM - Storing 's' to 29

	chickenpy.VM - Storing 's' to 25

	chickenpy.VM - Storing 'y' to 48

	chickenpy.VM - Storing 'z' to 47

	chickenpy.VM - Storing 'm' to 42

	chickenpy.VM - Storing 't' to 4

	chickenpy.VM - Storing '' to 27

	chickenpy.VM - Storing 'r' to 10

	chickenpy.VM - Storing 'h' to 8

	chickenpy.VM - Storing 't' to 39

	chickenpy.VM - Storing 'g' to 34

	chickenpy.VM - Storing 'v' to 18

	chickenpy.VM - Storing '' to 21

	chickenpy.VM - Storing 'u' to 38

	chickenpy.VM - Storing '' to 16

	chickenpy.VM - Storing 'u' to 2

	chickenpy.VM - Storing '_' to 43

	chickenpy.VM - Storing '4' to 32

	chickenpy.VM - Storing 'l' to 44

	chickenpy.VM - Storing 'b' to 37

	chickenpy.VM - Storing '{' to 6

	chickenpy.VM - Storing 'e' to 28

	chickenpy.VM - Storing 'b' to 0


Hmm, i noticed that every number represents a letter for example: 

    chickenpy.VM - Storing 'b' to 0

    storing 'b' to 0, so index number 0
    
    is representing letter 'b'
    
	and so on like indexing in array we count from 0


 i started to combine them from index `0` to the last index
 
so since i start counting from `0` i will see if `0` matches the letter `b` cuz  the flag is always starts with letter `b`  and the flag pattern is `byuctf{answer...}` so if yes i will keep going to the next index and it matches letter `y` that means i am on the right track cuz next letter in the flag is `y`, i hope you understand this part xd

 once i done collected the flag i submitted it but it said wrong flag

 ~~byuctf{th3r3_4r3_3ven_w01s3_es0l4ngs_but_1m_lazzy}~~

 i asked the support and they told me
 
 `w01s3` not a word so i thought to replace the numbers with their
 
 normal letters and translate it on google like this 
 
 {there_are_even_woise_esolengs_but_im_lazzy} to see the meaning and
 
to be able to know the correct word for `w01s3`
and i found out the correct one is  `w0rs3`

 so i edited my flag and submitted it and 

Bingo!! i got chicken Challenge

> FLAG: byuctf{th3r3_4r3_3ven_w0rs3_es0l4ngs_but_1m_lazzy}

Thanks For REading..