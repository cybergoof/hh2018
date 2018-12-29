---
layout: elf
title: "CURLing Master"
#date: 2018-12-03
#image: "challenge.md"
images: ["1.png"]
terminal-hyperlink: "https://docker.kringlecon.com/?challenge=vplaintext-chttp2"
elf-name: "Holly Evergreen"
elf-directory: "holly"
tags: [sample post, readability, test]
comments: false
image-dir: /assets/img/elves/holly
links: []
answer: Elinore
comments: false
---



As the Riddle says, looked at ```/etc/nginx``` and see there is an ```nginx.conf``` file.  A ```cat``` of ```nginx.conf``` shows that it is running ```http2```
<figure>
	<img src="/assets/img/elves/holly/1.png">
	<figcaption>NGINX File</figcaption>
</figure>


We are going to have to curl to get the data from HTTP2.

The example from the talk, using https://www.youtube.com/watch?v=PC6-mn9g9Cs was not working
<figure>
	<img src="/assets/img/elves/holly/2.png">
	<figcaption>Failed curl</figcaption>
</figure>

I looked at this page https://curl.haxx.se/docs/http2.html and used the switch ```--http2-prior-knowledge``` to create a post

<figure>
	<img src="/assets/img/elves/holly/3.png">
	<figcaption>CURL Tools</figcaption>
</figure>

