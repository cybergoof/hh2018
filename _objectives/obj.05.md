---
layout: objective
title: "AD Privilege Discovery"
#date: 2018-12-03
number: "5"
#image: "obj.2/obj.2.challenge.md"
images: []
question: "Using the data set contained in this SANS Slingshot Linux image, find a reliable path from a Kerberoastable user to the Domain Admins group. What’s the user’s logon name? Remember to avoid RDP as a control path as it depends on separate local privilege escalation flaws. For hints on achieving this objective, please visit Holly Evergreen and help her with the CURLing Master Cranberry Pi terminal challenge."
terminal-hint: "Describe the hints from the terminal"
images: ["1.png","2.png","answer.png","question.png"]
narrative: "3"
hans: "1"
elf-name: "Holly Evergreen"
elf-terminal: "CURLing Master"
elf-directory: "holly"
tags: [sample post, readability, test]
comments: false
image-dir: /assets/img/objectives/5
links: ["https://download.holidayhackchallenge.com/HHC2018-DomainHack_2018-12-09.ova"]
answer: "LDUBEJ00320@AD.KRINGLECASTLE.COM"
---


I downloaded an image put out by the incredible Jeff McJunkin

After changing the base memory to 8GB and setting the OS to Debian x64, I was able to log in
<figure>
	<img src="{{site.baseurl}}/assets/img/objectives/8/14.png">
	<figcaption>Found Secret Capture</figcaption>
</figure>

Bloodhound is already installed.  I opened it up and get a diagram that shows users to the domain
<figure>
	<img src="{{site.baseurl}}/assets/img/objectives/5/2.png">
	<figcaption>Starting Bloodhount</figcaption>
</figure>


I select the "Shortest Path" and get this image 
<figure>
	<img src="{{site.baseurl}}/assets/img/objectives/5/3.png">
	<figcaption>Shortest Path</figcaption>
</figure>

But, the right query is "Shortest Paths to Domain Admins from Kerberoastable Users"
<figure>
	<img src="{{site.baseurl}}/assets/img/objectives/5/4.png">
	<figcaption>Shortest Path to Domain Admins</figcaption>
</figure>

These were all the possible users.  

LDUBEJ00320@AD.KRINGLECASTLE.COM
SMARCELLA00089@AD.KRINGLECASTLE.COM
MTETTER00299@AD.KRINGLECASTLE.COM
LDUBEJ00320@AD.KRINGLECASTLE.COM
ZANDERA00437@AD.KRINGLECASTLE.COM
JGUMBEL00486@AD.KRINGLECASTLE.COM
ELANGONI00222@AD.KRINGLECASTLE.COM
JFOX00132@AD.KRINGLECASTLE.COM
AMARCELLA0089@AD.KRINGLECASTLE.COM
RLOEFFELHOLZ0041@AD.KRINGLECASTLE.COM
GLEONPACHER00047@AD.KRINGLECASTLE.COM
RHEYDEL00118@AD.KRINGLECASTLE.COM
JBETAK00084@AD.KRINGLECASTLE.COM

Based on the hint that RDP would not be a good path, I eliminated the ones that needed RDP.  I reran the query and retrieved these
<figure>
	<img src="{{site.baseurl}}/assets/img/objectives/5/5.png">
	<figcaption>Filter RDP</figcaption>
</figure>

That left just two users

------
LDUBEJ00320@AD.KRINGLECASTLE.COM
JBETAK00084@AD.KRINGLECASTLE.COM

Trying LDUBEJ0032 on the first try was the right one.