---
layout: elf
title: "Lethal ForensicElfication"
#date: 2018-12-03
#image: "challenge.md"
images: ["1.png"]
terminal-hyperlink: "https://docker.kringlecon.com/?challenge=viminfo"
elf-name: "Tangle Coalbox"
elf-directory: "tangle"
tags: [sample post, readability, test]
comments: false
image-dir: /assets/img/elves/tangle
links: []
#answer: Elinore
comments: false
---


A quick listing shows that there is a file called ```poem.txt``` in a hidden file called ```.secrets/her/```
<figure>
	<img src="/assets/img/elves/tangle/1.png">
	<figcaption>Directory Listing</figcaption>
</figure>

Looking at the poem, it appears that the name of the subject of the poem has been replaced with "NEVERMORE"
<figure>
	<img src="/assets/img/elves/tangle/2.png">
	<figcaption>The File</figcaption>
</figure>


The ```.viminfo``` file in the home directory provides a list of previous commands. It could give us some clues.

<figure>
	<img src="/assets/img/elves/tangle/3.png">
	<figcaption>VimInfo</figcaption>
</figure>


by looking at .viminfo, I see ```%s/Elinore/NEVERMORE/g``` is a global replace of the word Elinore with NEVERMORE>

The subject of the poem is Elinore



