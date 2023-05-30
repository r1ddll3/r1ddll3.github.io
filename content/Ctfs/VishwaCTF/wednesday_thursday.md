---
title: "VishwaCTF 2023 -   Reverse Wednesday Thursday Friday"
date: 2023-04-02T23:38:15+02:00
draft: true
tags: ["CTFS", "VishwaCTF", "Reverse"]
author: "@R1ddl3"
# author: ["Me", "You"] # multiple authors
showToc: false
TocOpen: false
draft: false
hidemeta: false
comments: true
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
    alt: "VishwaCTF" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
---
----

We were given a [file](https://we.tl/t-kdQCNTeD6E) and that file was `ELF` and we can determine that by using DIE 
![enter image description here](https://i.imgur.com/TyKXj6r.png)

After we open the file in `IDA Pro` and press `F5` to view the pseudocode we will see below code
![enter image description here](https://i.imgur.com/yZPk2nB.png)

The code performs a series of mathematical conditions using the characters in the string `s` and checks if the results are equal to certain specific values. If all the conditions are matached, the program will print a message that tells us if the input is valid or invalid.

So, we can solve the challenge by mtaching these all conditions.

We can solve this challenge using `z3-solver` python library, solving script which I created is


	from z3 import Solver, BitVec

	a = [BitVec(f's{i}',8) for i in range(34)] # 34 is the length of the flag 
	# we knew that from the psudocode.

	solver = Solver()

	# ensure that each element of the list `a` is a printable ASCII character
	for i in range(10,33):
	    solver.add(a[i] >= ord('0'))
	    solver.add(a[i] <= ord('z'))

	# Set the flag format to 'VishwaCTF{'
	FLAG_FORMAT = "VishwaCTF{"

	# Add constraints to enforce that the first 11 elements of list `a`
	# correspond to the characters in the FLAG_FORMAT string
	for i, char in enumerate(FLAG_FORMAT):
	    solver.add(a[i] == ord(char))

	# enforce that the last element in the flag is `}`
	solver.add(a[33] == ord("}"))

	# Add constraints
	solver.add(a[3] + a[4] + a[1] + a[7] - a[8] * a[2] * a[6] * a[5] - a[11] - a[9] - a[10] == -52316790)
	solver.add(a[3] - a[4] - a[6] + a[9] + a[8] * a[11] * a[10] - a[2] + a[5] + a[7] * a[12] == 285707)
	solver.add(a[11] + a[10] * a[4] + a[3] - a[12] * a[7] - a[13] - a[5] * a[9] * a[6] + a[8] == -797145)
	solver.add(a[4] + a[12] - a[7] * a[11] - a[9] - a[5] * a[6] - a[14] - a[8] * a[13] * a[10] == -289275)
	solver.add(a[13] + a[14] + a[7] + a[6] - a[12] - a[15] * a[11] - a[5] + a[8] * a[10] * a[9] == 666868)
	solver.add(a[12] + a[15] * a[16] + a[11] + a[13] - a[10] + a[6] * a[8] - a[7] - a[9] + a[14] == 9837)
	solver.add(a[7] + a[11] - a[8] + a[16] * a[13] - a[17] - a[14] - a[9] + a[10] * a[15] - a[12] == 9858)
	solver.add(a[17] + a[12] + a[9] - a[18] - a[8] - a[15] + a[16] + a[11] * a[14] * a[13] - a[10] == 296504)
	solver.add(a[11] * a[13] * a[18] * a[16] - a[17] - a[10] + a[9] + a[15] * a[12] - a[19] - a[14] == 10963387)
	solver.add(a[17] + a[16] + a[20] + a[12] - a[14] * a[18] * a[15] * a[19] - a[13] - a[11] - a[10] == -65889660)
	solver.add(a[16] - a[19] - a[15] + a[11] * a[13] + a[18] + a[21] * a[12] + a[14] + a[17] * a[20] == 13340)
	solver.add(a[18] * a[16] + a[17] * a[15] - a[20] - a[12] - a[19] * a[14] + a[22] + a[13] * a[21] == 4641)
	solver.add(a[15] + a[20] + a[18] + a[21] + a[13] * a[19] - a[22] - a[16] - a[14] + a[17] * a[23] == 6428)
	solver.add(a[19] * a[24] + a[15] * a[20] + a[16] * a[14] + a[23] - a[18] * a[21] - a[22] * a[17] == 7851)
	solver.add(a[19] + a[24] + a[22] + a[21] + a[25] + a[16] + a[18] + a[20] * a[23] - a[15] + a[17] == 2997)
	solver.add(a[17] * a[23] + a[20] * a[25] - a[16] + a[26] * a[21] - a[24] + a[22] * a[19] * a[18] == 342425)
	solver.add(a[20] + a[26] + a[24] * a[17] + a[27] * a[22] * a[25] - a[21] - a[19] * a[18] + a[23] == 243251)
	solver.add(a[24] + a[22] + a[25] * a[21] - a[28] - a[19] - a[26] * a[27] * a[20] - a[23] + a[18] == -434772)
	solver.add(a[28] + a[19] + a[25] + a[29] - a[24] - a[21] - a[23] + a[27] - a[22] * a[26] + a[20] == -4957)
	solver.add(a[21] + a[30] + a[26] + a[22] * a[23] - a[29] + a[20] - a[24] * a[25] - a[27] - a[28] == -1625)
	solver.add(a[22] + a[26] + a[25] + a[30] + a[23] - a[24] - a[29] - a[31] - a[21] - a[27] - a[28] == -144)
	solver.add(a[29] + a[30] + a[31] - a[26] - a[25] - a[23] - a[28] - a[27] - a[22] - a[32] * a[24] == -7001)
	solver.add(a[33] + a[25] - a[31] * a[23] + a[27] - a[26] * a[32] + a[30] - a[24] * a[29] - a[28] == -18763)

	sat = solver.check() # Check if the model is "satisfied" 
	if sat:
	    model = solver.model() # returns an array of s[flag_length] = flag_chars
	    flag = ''
	    for i in a: # a = 34 = the length of the flag
	        flag += chr(model[i].as_long()) # combine the flag
	    print(f"Flag: {flag}")
	else:
	    print("Not satisfied") # Didn't work "unsatisfied"



So, by running this script I was able to get the flag easily.

![enter image description here](https://i.imgur.com/O854lHm.png)

> Flag: VishwaCTF{N3V3r_60NN4_61V3_Y0U_UP}
