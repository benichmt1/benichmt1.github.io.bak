---
layout: post
title: "sCTF 2015 Q1   Hello World Solution"
description: ""
category: Tutorial
tags: [Intermediate, CTF, Tutorial, Reverse Engineering, Assembly]
---
{% include JB/setup %}
This problem is the second in my series on [sCTF Q1](http://www.sctf.io), a high-school capture the flag competition.

##Hello World
{% highlight text %}
{% raw %}
The flag is less than 8 characters.

Have Fun

NOTE: You don't have to run the problem to solve, and it isn't advised either .

{% endraw %}
{% endhighlight %}

The "Have Fun" text was linked to an executable file called 'qwerty.exe' (not posted here for reasons which you will see soon!)
I decided to take their warning to heart and scan it with VirusTotal before attempting any sandboxed debugging. The results of my [VirusTotal scan](https://www.virustotal.com/en/file/b584431436f5eef839b0eb5a81c981c2db3c30572538c9b41332c191b939792c/analysis/) were pretty telling - there was something going on with this file. I doubted it was an actual trojan and immediately guessed that the AV software was picking up some sort of obfuscator or packer.

I loaded up a virtual machine and analyzed in [OllyDbG](http://www.ollydbg.de/) and tried to search for the referenced ASCII strings. Olly turned up a few false positives, as seen below, but nothing particularly interesting.
![OllyDbG](http://i.imgur.com/kV3F1AIs.png)

There were a few strings which looked familiar to .NET applications, so I put it in [CFF explorer](www.ntcore.com/exsuite.php) and it confirmed my hunch that it was in fact a .NET app.
![CFF Explorer](http://i.imgur.com/L2373IFs.png)

Now that I knew I was dealing with a .NET app, my next step was to disassemble it. I used [ILSpy](ilspy.net) because it was free compared to Reflector. I didn't find the string I was looking for, but I did receive a major hint - a module titled "ConfusedBy" with a property of "ConfuserEx v0.4.0".
![ILSpy](http://i.imgur.com/Jj5DCEus.png)

After some research, I was able to peek at the source code for ConfuserEx but decided it would take too much time to work through the decryption manually. Back in the old days, I practiced ReverseMe exercises at a place called Tuts4You, so I decided to do a search of the forum. Conveniently, I remembered my old login and someone had posted a tool that could be used to reverse the Confuser packer. This was the [Tuts4You forum post that I used](https://forum.tuts4you.com/topic/36631-unconfuserex/).

After downloading and checking this application for viruses, I loaded up the original qwerty.exe into the unpacker.
![UnConfuserEx v1.0](http://i.imgur.com/y4aDDSt.png)

Finally, I was able to open it back up in CFF Explorer and see that now I could view a Metadata stream that made sense. Clearly there was an ascii stream that said something to the extent of: flag_not_the_flag_ qwerty. I recognized csrss.exe as a system process, so I tried several permutations of those words. It wasn't until after several tries that I figured out the flag was simply 'qwerty', which corresponds with the frustrating simplicity of a "Hello World" Program.
![Final Answer](http://i.imgur.com/i8LnTVN.png)



<strong> Difficulty: </strong> 7
<strong> Fun: </strong> 8




