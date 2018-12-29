---
layout: elf
title: "Yule Log Analysis"
#date: 2018-12-03
#image: "challenge.md"
images: ["1.png"]
terminal-hyperlink: "https://docker.kringlecon.com/?challenge=spray-detect"
elf-name: "Pepper Minstix"
elf-directory: "pepper"
tags: [sample post, readability, test]
comments: false
answer: minty.candycane
image-dir: /assets/img/elves/pepper
links: []

comments: false
---




<figure>
	<img src="/assets/img/elves/holly/1.png">
	<figcaption>NGINX File</figcaption>
</figure>


There was an attack and a password spray against a tareget.  




Doing an ls, I see that there is a "evtx_dump.py" and the event trace file "ho-ho-no.evtx"
<figure>
	<img src="/assets/img/elves/pepper/1.png">
	<figcaption>Directory Listing</figcaption>
</figure>

With a spray, I am looking for lots of failed requests, and then a success.  The users "HealthMailBoxXXXXXXX" can be ingored.

I ran the command:
```
python evtx_dump.py ho-ho-no.evtx > out.txt
```


I copy/pasted the info into an editor.  

<figure>
	<img src="/assets/img/elves/pepper/3.png">
	<figcaption>Looking at Output</figcaption>
</figure>

Looking at the editor, I found the last failed login, and then the very next successful login.

Event ID 4625 is a failed login, and 4624 is a success.  There were a couple of options. Ignoring all the "HealthMailbox" logons, I focused in on:

<figure>
	<img src="/assets/img/elves/pepper/4.png">
	<figcaption>Minty User</figcaption>
</figure>

```minty.candycane```



