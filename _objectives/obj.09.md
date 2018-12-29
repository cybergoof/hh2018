---
layout: objective
title: "Network Traffic Forensics"
#date: 2018-12-03
number: "9"
#image: "obj.2/obj.2.challenge.md"
images: []
question: "Using the Word docm file, identify the domain name that the malware communicates with."
images: ["1.png","2.png","answer.png","question.png"]
narrative: "6"
hans: "3"
elf-name: "Shinny Upatree"
elf-terminal: "Sleigh Bell Lottery Cranberry Pi"
elf-directory: "shinny"
tags: [sample post, readability, test]
comments: false
image-dir: /assets/img/objectives/9
links: ["https://packalyzer.kringlecastle.com/"]
answer: "Rachmaninoff"
---

### Catch the Malware
<figure>
	<img src="{{site.baseurl}}/assets/img/objectives/9/9.1.png">
	</figure>
Need to help build a snort filter to identify the malware that is plaguing Santa's Castlce.  We know from Shinny, that the [powershell talk](https://www.youtube.com/watch?v=wd12XRq2DNk) is important.

Uses Powershell ISE, wireshark, procmon.exe, procdump64.exe, power_dump.py (https://github.com/chrisjd20/power_dump) and olevba

First, need to work on the SNORT termianl
https://docker.kringlecon.com/?challenge=snort


<figure>
	<img src="{{site.baseurl}}/assets/img/objectives/9/1.png">
	<figcaption>Snort Challenge</figcaption>
</figure>

More Info:
```
MORE INFO:
  A full capture of DNS traffic for the last 30 seconds is 
  constantly updated to:

  /home/elf/snort.log.pcap

  You can also test your snort rule by running:

  snort -A fast -r ~/snort.log.pcap -l ~/snort_logs -c /etc/snort/snort.conf

  This will create an alert file at ~/snort_logs/alert

  This sensor also hosts an nginx web server to access the 
  last 5 minutes worth of pcaps for offline analysis. These 
  can be viewed by logging into:

  http://snortsensor1.kringlecastle.com/

  Using the credentials:
  ----------------------
  Username | elf
  Password | onashelf

  tshark and tcpdump have also been provided on this sensor.

HINT: 
  Malware authors often user dynamic domain names and 
  IP addresses that change frequently within minutes or even 
  seconds to make detecting and block malware more difficult.
  As such, its a good idea to analyze traffic to find patterns
  and match upon these patterns instead of just IP/domains.elf@d5a01fce435e:~$ 
  ```

Looking at the Snort webpage, I get a directory listing of pcap that I can download and view in wireshark.  Nice touch!

<figure>
	<img src="{{site.baseurl}}/assets/img/objectives/9/2.png">
	<figcaption>Snort Sensor PCAP Files</figcaption>
</figure>



Looking at the DNS calls, there are alot of strange ones that follows a pattern 
```
1.77616E6E61636F6F6B69652E6D696E2E707331.bnugasherr.com
2.77616E6E61636F6F6B69652E6D696E2E707331.bnugasherr.com
4.77616E6E61636F6F6B69652E6D696E2E707331.bnugasherr.com
5.77616E6E61636F6F6B69652E6D696E2E707331.bnugasherr.com
```

Although the domain name changes, the 38 byte number ```77616E6E61636F6F6B69652E6D696E2E707331``` does not.

Tried to use the snort rule:
{% highlight shell %}
alert tcp any any -> any any (msg:"The DNS"; content: "77616E6E61636F6F6B69652E6D696E2E707331"; sid: 100003; rev:3;)
{% endhighlight %}

<figure>
	<img src="{{site.baseurl}}/assets/img/objectives/9/3.png">
	<figcaption>Snort Success</figcaption>
</figure>



The response is alot of text.  I'm guessing that we are looking at a DNS covert channel.
```
0000   45 00 01 a7 00 01 00 00 40 11 3e e9 27 08 08 60   E..§....@.>é'..`
0010   0a 7e 00 77 00 35 94 f8 01 93 d0 38 6f db 84 00   .~.w.5.ø..Ð8oÛ..
0020   00 01 00 01 00 00 00 00 01 32 26 37 37 36 31 36   .........2&77616
0030   45 36 45 36 31 36 33 36 46 36 46 36 42 36 39 36   E6E61636F6F6B696
0040   35 32 45 36 44 36 39 36 45 32 45 37 30 37 33 33   52E6D696E2E70733
0050   31 0a 62 6e 75 67 61 73 68 65 72 72 03 63 6f 6d   1.bnugasherr.com
0060   00 00 10 00 01 01 32 26 37 37 36 31 36 45 36 45   ......2&77616E6E
0070   36 31 36 33 36 46 36 46 36 42 36 39 36 35 32 45   61636F6F6B69652E
0080   36 44 36 39 36 45 32 45 37 30 37 33 33 31 0a 62   6D696E2E707331.b
0090   6e 75 67 61 73 68 65 72 72 03 63 6f 6d 00 00 10   nugasherr.com...
00a0   00 01 00 00 02 58 00 ff fe 36 39 37 34 37 39 32   .....X.ÿþ6974792
00b0   65 34 33 37 32 37 39 37 30 37 34 36 66 36 37 37   e43727970746f677
00c0   32 36 31 37 30 36 38 37 39 32 65 34 31 36 35 37   2617068792e41657
00d0   33 34 64 36 31 36 65 36 31 36 37 36 35 36 34 32   34d616e616765642
00e0   37 33 62 32 34 34 31 34 35 35 33 35 30 32 65 34   73b24414553502e4
00f0   64 36 66 36 34 36 35 32 30 33 64 32 30 35 62 35   d6f6465203d205b5
0100   33 37 39 37 33 37 34 36 35 36 64 32 65 35 33 36   3797374656d2e536
0110   35 36 33 37 35 37 32 36 39 37 34 37 39 32 65 34   56375726974792e4
0120   33 37 32 37 39 37 30 37 34 36 66 36 37 37 32 36   3727970746f67726
0130   31 37 30 36 38 37 39 32 65 34 33 36 39 37 30 36   17068792e4369706
0140   38 36 35 37 32 34 64 36 66 36 34 36 35 35 64 33   865724d6f64655d3
0150   61 33 61 34 33 34 32 34 33 33 62 32 34 34 31 34   a3a4342433b24414
0160   35 35 33 35 30 32 65 34 32 36 63 36 66 36 33 36   553502e426c6f636
0170   62 35 33 36 39 37 61 36 35 32 30 33 64 32 30 33   b53697a65203d203
0180   31 33 32 33 38 33 62 32 34 34 31 34 35 35 33 35   132383b244145535
0190   30 32 65 34 62 36 35 37 39 35 33 36 39 37 61 36   02e4b657953697a6
01a0   35 32 30 33 64 32 30                              5203d20
```

### Identify the Domain
<figure>
	<img src="{{site.baseurl}}/assets/img/objectives/9/9.2.png">
	</figure>
Albaster gives a hint to download and analyze a Word document.  The word document has a powershell malware in it.  
The malware is communciating with a server on the domain: 
```
erohetfanu.com
```
<figure>
	<img src="{{site.baseurl}}/assets/img/objectives/9/9.1.1.png">
</figure>

### Stop the Malware
<figure>
	<img src="{{site.baseurl}}/assets/img/objectives/9/9.3.png">
	</figure>
In the powershell is using a kill switch to determine if it needs to stop running.  If it can't communicate with it, it does a return and stops executing 
```
yippeekiyaa.aaay
```

### Discover Alabaster's Password
<figure>
	<img src="{{site.baseurl}}/assets/img/objectives/9/9.4.png">
</figure>
Walking through the code, I was able to see that it is creating a file encryption key, then encrypting that with a public key. The malware retrieves that 

```
7365727665722E637274.erohetfanu.com
```

The only way to decrypt that file encryption key, is with a private key.

The 7365727665722E637274 is a hex representation of "sever.crt"

Therefore, to get the server.key, I needed to make the DNS Request to 
```
7365727665728e6b6579.erohetfanu.com
```

With the private key, I needed to pull from memory a 512 hex string using powershell_dump.

I pulled that data into a file.

With some help, I used python code to decrypt the key.  
{% highlight python %}
from Crypto.PublicKey import RSA
from Crypto.Cipher import PKCS1_OAEP

payload = "3cf903522e1a3966805b50e7f7dd51dc7969c73cfb1663a75a56ebf4aa4a1849d1949005437dc44b8464dca05680d531b7a971672d87b24b7a6d672d1d811e6c34f42b2f8d7f2b43aab698b537d2df2f401c2a09fbe24c5833d2c5861139c4b4d3147abb55e671d0cac709d1cfe86860b6417bf019789950d0bf8d83218a56e69309a2bb17dcede7abfffd065ee0491b379be44029ca4321e60407d44e6e381691dae5e551cb2354727ac257d977722188a946c75a295e714b668109d75c00100b94861678ea16f8b79b756e45776d29268af1720bc49995217d814ffd1e4b6edce9ee57976f9ab398f9a8479cf911d7d47681a77152563906a2c29c6d12f971"

enc_session_key = bytes.fromhex(payload)
private_key = RSA.import_key(open('server.key').read())
cipher_rsa = PKCS1_OAEP.new(private_key)
session_key = cipher_rsa.decrypt(enc_session_key)
print(''.join('{:02x}'.format(x) for x in session_key))
{% endhighlight %}

I then reused the Powershell code to decrypt the wanacookie file, and got a SQLite database with a table called password:

```
alabaster.snowball|CookiesR0cK!2!#|active directory
alabaster@kringlecastle.com|KeepYourEnemiesClose1425|www.toysrus.com
alabaster@kringlecastle.com|CookiesRLyfe!*26|netflix.com
alabaster.snowball|MoarCookiesPreeze1928|Barcode Scanner
alabaster.snowball|ED#ED#EED#EF#G#F#G#ABA#BA#B|vault
alabaster@kringlecastle.com|PetsEatCookiesTOo@813|neopets.com
alabaster@kringlecastle.com|YayImACoder1926|www.codecademy.com
alabaster@kringlecastle.com|Woootz4Cookies19273|www.4chan.org
alabaster@kringlecastle.com|ChristMasRox19283|www.reddit.com
```
The 

It provided a hint:

```
Rachmaninoff
From: Alabaster Snowball
Really, it's Mozart. And it should be in the key of D, not E.
```
