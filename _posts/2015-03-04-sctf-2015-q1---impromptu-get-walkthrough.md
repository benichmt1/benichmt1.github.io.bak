---
layout: post
title: "sCTF 2015 Q1 - Impromptu GET Walkthrough"
description: ""
category: Tutorial, CTF, Web Security
tags: [tutorial, CTF, Web Security, beginner]
---
{% include JB/setup %}
As a Physics teacher with a CS background, I always try to encourage my students to use their problem-solving skills in practical ways. When I found out that there were more than a few students interested in Information Security, I went head over heels trying to enrich their desire to learn about this field. Through Reddit's Netsec community, I found out about a really cool opportunity - the [sCTF](http://www.sctf.io), a CTF competition specifically targeting high school students. 

Disclaimer: These may not be the intended solution, but are only my own attempts after the competition time expired. All questions are the respective properties of their creators.

### Impromptu GET
The problem is given as follows:

{% highlight text %}
{% raw %}
Jonathan cloned our router online access page again... Model number BRL-04FXP by bRoad Lanner. Except there's been a slight issue, he didn't copy any of the elements on the page used to login and we lost the username and password, but there's some sensitive data we need to recover.

Luckily it uses GET. So now it looks like we'll have to just pass the username and password parameters manually. But, we just don't know the username and password...

I'll hand you the link, maybe you can figure it out.
{% endhighlight %}
{% endraw %}


                                                                
