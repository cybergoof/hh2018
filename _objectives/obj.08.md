---
layout: objective
title: "Network Traffic Forensics"
#date: 2018-12-03
number: "8"
#image: "obj.2/obj.2.challenge.md"
images: []
question: "Santa has introduced a web-based packet capture and analysis tool at https://packalyzer.kringlecastle.com to support the elves and their information security work. Using the system, access and decrypt HTTP/2 network activity. What is the name of the song described in the document sent from Holly Evergreen to Alabaster Snowball? For hints on achieving this objective, please visit SugarPlum Mary and help her with the Python Escape from LA Cranberry Pi terminal challenge."
images: ["1.png","2.png","answer.png","question.png"]
elf-name: "SugarPlum Mary"
elf-terminal: "Python Escape from LA"
elf-directory: "sugarplum"
tags: [sample post, readability, test]
comments: false
image-dir: /assets/img/objectives/8
links: ["https://packalyzer.kringlecastle.com/"]
answer: "Mary Had a Little Lamb"
---

The website is a network packet analyzer website.  I created an account and logged in
<figure>
	<img src="/assets/img/objectives/8/1.png">
	<figcaption>Packalyzer Login</figcaption>
</figure>

After logging in, you can SNIFF TRAFFIC which will sniff 20 seconds of network traffic


<figure>
	<img src="/assets/img/objectives/8/2.png">
	<figcaption>Packalyzer Main Display</figcaption>
</figure>
From the hint, we know that we need to look for HTML comments to find a dev file.   The HTML comments describe an app.js file.

<figure>
	<img src="/assets/img/objectives/8/3.png">
	<figcaption>HTML Comments</figcaption>
</figure>



That file was accessible from the browser
<figure>
	<img src="/assets/img/objectives/8/4.png">
	<figcaption>UPDATE</figcaption>
</figure>

Opening that file, there were two areas of interest.  First, there is an SSLKEYLOGFILE turned on.  This is a file that the server will create that stores SSH Keys.   We can use these keys to decrypt the SSL Traffic in Wireshark per Chris Davis' talk (https://www.youtube.com/watch?v=YHOnxlQ6zec)
<figure>
	<img src="/assets/img/objectives/8/5.png">
	<figcaption>UPDATE</figcaption>
</figure>
The location of the file is the directory
```
__dirname/process.env.DEV/process.env.SSLKEYLOGFILE
__dirname - the current directory from where execution happens
process.env.DEV - an environment variable DEV
process.env.SSLKEYLOGFILE - likely the file name
```

I needed to extract these two variables.  I found this in the code:
<figure>
	<img src="/assets/img/objectives/8/6.png">
	<figcaption>UPDATE</figcaption>
</figure>

In DEV Mode (which is set), then allow all environment variables to be directories that are browsable.   Combining this with the hint from SugarPlum, I started using ```curl``` to manipulate URL calls.

I found that if I requested a URL where the directory browsing was allowed, ie there was an environment variable name, then I received a different error than if the directory is not browsable.

NOT BROWSABLE
<figure>
	<img src="/assets/img/objectives/8/7.png">
	<figcaption>UPDATE</figcaption>
</figure>
<figure>
	<img src="/assets/img/objectives/8/8.png">
	<figcaption>UPDATE</figcaption>
</figure>

BROWSABLE
<figure>
	<img src="/assets/img/objectives/8/9.png">
	<figcaption>UPDATE</figcaption>
</figure>
<figure>
	<img src="/assets/img/objectives/8/10.png">
	<figcaption>UPDATE</figcaption>
</figure>
Picking "dev" was completely random, and it actually confused me.  After some time being frustrated, I just threw in a weird URL and turned out to give me the answer I wanted.  I did not think that the message that was being returned would evaluate the input directory as a variable.
<figure>
	<img src="/assets/img/objectives/8/11.png">
	<figcaption>UPDATE</figcaption>
</figure>
<figure>
	<img src="/assets/img/objectives/8/12.png">
	<figcaption>UPDATE</figcaption>
</figure>

From the return value, we see that:
```
process.env.SSLKEYLOGFILE = packalyzer_clientrandom_ssl.log
```

Retrieving the file just required evaluating process.env.DEV and retrieving the file

```
curl -v --http2 https://packalyzer.kringlecastle.com/dev/packalyzer_clientrandom_ssl.log >> packalyzer_clientrandom_ssl.txt
```

With the SSL Keys, I downloaded a packat capture and used Wireshark to evaluate the SSL.  I found a JSON file with username and password information
<figure>
	<img src="/assets/img/objectives/8/13.png">
	<figcaption>Creds Found</figcaption>
</figure>


There were a number of other credentials
pepper/Shiz-Bamer_wabl182
alabaster/Packer-p@re-turntable192
bushy/Floppity_Floopy-flab19283

I logged into the Packalyzer with the credentials from Alabaster.  There is a file with the "super secret packet capture"
<figure>
	<img src="/assets/img/objectives/8/14.png">
	<figcaption>Found Secret Capture</figcaption>
</figure>


Using Wireshark, I found an email from Holly to Alabaster with an attachment
<figure>
	<img src="/assets/img/objectives/8/15.png">
	<figcaption>UPDATE</figcaption>
</figure>

Copying the attachment to a file and running base64 decode out to  a PDF
<figure>
	<img src="/assets/img/objectives/8/16.png">
	<figcaption>Decpded</figcaption>
</figure>

This provided the PDF that is talking about transposing on a piano, and the name of the song
