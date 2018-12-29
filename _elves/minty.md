---
layout: elf
title: "The Name Game"
#date: 2018-12-03
#image: "challenge.md"
images: ["1.png"]
terminal-hyperlink: "https://docker.kringlecon.com/?challenge=pwshmenu"
elf-name: "Minty CandyCane"
elf-directory: "minty"
tags: [sample post, readability, test]
comments: false
image-dir: /assets/img/elves/minty
links: []
answer: Scott
comments: false
---
Need to make a nametag with someone she doesn't remember last name.  From California of New Yorker.  Last name Chan


Need a name of someone.  They are making a badge

There is a SQL Lite Database that the data is sent to

Its easy, so I think I need to just break out and run sqllite

In the Riddle, there are three options, 1, 2 and Q for quit.

Selecting option 2, you can provide and IP address and it will be pinged.  Assuming that the input is not properly santized, and that whatever is inputed is sent directly to the execution, I appended the IP address with a shell command

This gave me shell:

<figure>
	<img src="{{site.baseurl}}/assets/img/elves/minty/1.png">
	<figcaption>Shell Success</figcaption>
</figure>

There is a database called main and a table called "onboard"
<figure>
	<img src="{{site.baseurl}}/assets/img/elves/minty/1.1.png">
	<figcaption>The Database</figcaption>
</figure>




Seeing a table called "onboard", then use the .schema command to see the columns.

<figure>
	<img src="{{ site.baseurl }}/assets/img/elves/minty/2.png">
	<figcaption>Tables in the database</figcaption>
</figure>

Running the select statement, 
<figure>
	<img src="{{ site.baseurl }}/assets/img/elves/minty/2.png">
	<figcaption>Running Select Statement</figcaption>
</figure>

<figure>
	<img src="{{ site.baseurl }}/assets/img/elves/minty/3.png">
	<figcaption>Running Select Statement</figcaption>
</figure>

Then, run the sql command
select fname,lname from onboard where lname="Chan";



Then, runtoanswer then entered Scott.
