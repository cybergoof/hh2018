---
layout: elf
title: "Dev Ops Fail"
#date: 2018-12-03
#image: "challenge.md"
images: ["1.png"]
terminal-hyperlink: "https://docker.kringlecon.com/?challenge=gitpasshist"
elf-name: "Sparkle Redberry"
elf-directory: "sparkle"
tags: [sample post, readability, test]
comments: false
answer: minty.candycane
image-dir: /assets/img/elves/sparkle
links: []

comments: false
---

Since this is a terminal, I can't use TruffleHog.  So, will look at Git History.  Likely look for "password"

Doing a directory listing, I see a directory called ```kcconfmgmt```

<figure>
	<img src="/assets/img/elves/sparkle/1.png">
	<figcaption>Directory Listing</figcaption>
</figure>

Inside that directory is a .git project
<figure>
	<img src="/assets/img/elves/sparkle/2.png">
	<figcaption>Git Proj Directory listing</figcaption>
</figure>


Since the hint says that the creds in question are in Git, but were overwritten, we will try and figure out from the ```git log``` when the file was changed.
<figure>
	<img src="/assets/img/elves/sparkle/3.png">
	<figcaption>Git Log</figcaption>
</figure>

Its easy to see that ```60a2ffea7520ee980a5fc60177ff4d0633f2516b``` commit message states
```
Author: Sparkle Redberry <sredberry@kringlecon.com>
Date:   Thu Nov 8 21:11:03 2018 -0500

    Per @tcoalbox admonishment, removed username/password from config.js, default settings i
n config.js.def need to be updated before use
```

Thus, we need to checkout the git commit right before that one at ```b2376f4a93ca1889ba7d947c2d14be9a5d138802```
<figure>
	<img src="/assets/img/elves/sparkle/4.png">
	<figcaption>Checking out to earlier commit</figcaption>
</figure>


The commit message says the file config.js was changed, so look for that file with ```find``` and then ```cat``` the file.
<figure>
	<img src="/assets/img/elves/sparkle/5.png">
	<figcaption>Found a password</figcaption>
</figure>

username is ```sredberry```  password is ```twinkletwinkletwinkle```
