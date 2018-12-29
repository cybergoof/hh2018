---
layout: objective
title: "Badge Manipulation"
#date: 2018-12-03
number: "6"
#image: "obj.2/obj.2.challenge.md"
images: []
question: "Bypass the authentication mechanism associated with the room near Pepper Minstix. A sample employee badge is available. What is the access control number revealed by the door authentication panel? For hints on achieving this objective, please visit Pepper Minstix and help her with the Yule Log Analysis Cranberry Pi terminal challenge."
terminal-hint: "Describe the hints from the terminal"
images: ["1.png","2.png","answer.png","question.png"]
narrative: "4"
elf-name: "Pepper Minstix"
elf-terminal: "Yule Log Analysis"
elf-directory: "pepper"
tags: [sample post, readability, test]
comments: false
image-dir: /assets/img/objectives/6
links: ["https://www.the-qrcode-generator.com/","https://www.holidayhackchallenge.com/2018/challenges/alabaster_badge.jpg","https://docker.kringlecon.com/?challenge=qrcode"]
answer: "19880715"
---

I first downloaded the image to Alabaster's Badge.




The hint was to get Alabaster's badge, so I downloaded it from the provided link.
<figure>
	<img src="{{site.baseurl}}/assets/img/objectives/6/1.png">
	<figcaption>Alabaster</figcaption>
</figure>

I think I need to decode his badge, then makfe my own qr code

First, I needed to decode the QR Code on Alabaster's badge.
<figure>
	<img src="{{site.baseurl}}/assets/img/objectives/6/2.png">
	<figcaption>zxing.com</figcaption>
</figure>

I see that the result is ```oRjg5uGHmbduj2m```

I tried running ```oRjg5uGHmbduj2m``` through some decoders and hash detectors, but it was being recognized.  I was thinking it was some type of hash of the user's name.  So, I decided to try and run his card and see what message I get.

By putting in Alabaster's card, I get "no valid user account".   This made me think that the system was checking the value against some database.  So I attempted a simple SQL Injection.

I created a QR code that said:
```
test' or 1=1 limit 1#
```
The display says that there is a sytnax error.  The error told me that:
* This is a Mariadb database, which is similar to MySQL
* That the select should be 
``` 
SELECT FIRST_NAME, LAST_NAME, ENABLED FROM EMPLOYEES WHERE AUTHORIZED = 1 AND UID = '{?UserID?}' LIMIT 1;
```
The User ID is the string value of the QRC Code.

I therefore needed to create a SQL Injection that would return an Enabled user.

```
1}' or ENABLED=1 LIMIT 1; #
```
<figure>
	<img src="{{site.baseurl}}/assets/img/objectives/6/3.png">
	<figcaption>Working QR Code</figcaption>
</figure>


This also opened a door to Santa's secret workshop.
