---
layout: elf
title: "Stall Mucking Report"
#date: 2018-12-03
#image: "challenge.md"
images: ["1.png"]
terminal-hyperlink: "https://docker.kringlecon.com/?challenge=vplaintext-creds"
elf-name: "Wunorse Openslae"
elf-directory: "wunorse"
tags: [sample post, readability, test]
comments: false
image-dir: /assets/img/elves/wunorse
links: []
answer: Elinore
comments: false
---



Doing an ls, I find the files
<figure>
	<img src="/assets/img/elves/wunorse/1.png">
	<figcaption>File Listing</figcaption>
</figure>

The hint said to look at memory.  So a ```ps -aux``` shows manager using their password
<figure>
	<img src="/assets/img/elves/wunorse/2.png">
	<figcaption>Looking for running processes</figcaption>
</figure>


The password that manager uses is revealed as ```directreindeerflatterystable```

Since the SMB service is ```//localhost/report-upload```, I can now try and push the file up
<figure>
	<img src="/assets/img/elves/wunorse/3.png">
	<figcaption>Upload with SMB</figcaption>
</figure>

I am able to upload the file and success

