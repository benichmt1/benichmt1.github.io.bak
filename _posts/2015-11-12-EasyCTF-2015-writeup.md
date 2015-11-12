---
layout: post
title: "EasyCTF 2015 Writeups"
description: ""
category: Tutorial
tags: [Intermediate, CTF, Tutorial, Reverse Engineering, Assembly]
---
{% include JB/setup %}
These writeups are for [EasyCTF](http://www.easyctf.com), another high-school capture the flag competition. 
This was our school's first time competing in EasyCTF.

Brecksville-Broadview Heights High School

Team: 
Anthony Citraro

Adam Galauner

Josh Jacob

Eric Fu

Ben Kang

Coach: Michael Benich

##lolteam - 65
###Writeup - Adam Galauner
{% highlight text %}
{% raw %}
There's a suspicious team out there called lolteam, I got my eyes on them for a while and I managed to wiretap their browser as they were changing their password. What did they change their password to?

{% endraw %}
{% endhighlight %}

Before using Wireshark, we were actually able to deduce the flag directly by opening the .pcapng file up in the browser. Looking through the file, you will see “password=”. The flag is spelled out. flag%7Bno%2C_lolteam_is_not_an_admin_account%7D. “&” means the end of the variable. “%” means a start of an ascii value in hexadecimal. Translate ‘7B’ to “{“, ‘2C’ to “,”, and ‘7D’ to “}”. The flag is spelled out: flag{no,_lolteam_is_not_an_admin_account}.

Upon further searching, a .pcapng file is one that can be opened in Wireshark. Opening the file allowed us to better inspect the packets. The data was very clearly sent in a form along with other dummy data.

![pcapng](http://staff.bbhcsd.org/benichm/files/2015/11/pcapng1.png)


<strong> Difficulty: </strong> 3

<strong> Fun: </strong> 3




