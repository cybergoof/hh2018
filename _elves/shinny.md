---
layout: elf
title: "Sleigh Bell Lotttery"
#date: 2018-12-03
#image: "challenge.md"
images: ["1.png"]
terminal-hyperlink: "https://docker.kringlecon.com/?challenge=pwshmenu"
elf-name: "Shinny Upatree"
elf-directory: "shinny"
tags: [sample post, readability, test]
comments: false
image-dir: /assets/img/elves/shinny
links: []
answer: Scott
comments: false
---

Area 2  on the left


GDB Debugger
https://pen-testing.sans.org/blog/2018/12/11/using-gdb-to-call-random-functions


Using nm, got a listing of the functions.
<figure>
	<img src="{{site.baseurl}}/assets/img/elves/shinny/1.png">
	<figcaption>Tables in the database</figcaption>
</figure>
<figure>
	<img src="{{site.baseurl}}/assets/img/elves/shinny/2.png">
	<figcaption>Tables in the database</figcaption>
</figure>

The ```winnerwinner``` seems to be the most interesting.  

Start GDB and put a break at Main.  Then, did a jump to ```winnerwinner```.  
<figure>
	<img src="{{site.baseurl}}/assets/img/elves/shinny/3.png">
	<figcaption>Tables in the database</figcaption>
</figure>

This printed the winner message and achievement



