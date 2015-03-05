---
layout: post
title: "sCTF 2015 Q1 - Impromptu GET Walkthrough"
description: ""
category: Tutorial
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

{% endraw %}
{% endhighlight %}

The [link](http://compete.sctf.io/problems/2015q1/impromptuget.php) led to a PHP page that simply said "incorrect". My first thought was to try and test it for a [local file inclusion](http://hakipedia.com/index.php/Local_File_Inclusion), so I attempted the following check: 
{% highlight http %}
http://compete.sctf.io/problems/2015q1/impromptuget.php?file=index.html
{% endhighlight %}


This was unsuccessful. I figured that the scope of the competition wouldn't have anything particularly nasty, and since this was only 20 points the solution must be more obvious.

My next step was to try to pass the parameters directly and see if I could glean any information about the underlying router.
{% highlight http %}
http://compete.sctf.io/problems/2015q1/impromptuget.php?username=admin&password=admin
{% endhighlight %}


Unfortunately, I did not get any confirmation as to whether or not a username was correct. I was unfamiliar with the BRL-04FXP and honestly thought it was fictitious at first, but when I googled it, I was able to find a [manual (warning:PDF)](http://www.planex.net/pdf/router/BRL-04FXP_Manual_v1.1_Eng.pdf). The manual told me that the default was blank and the password was '0000'.
![Default Password](https://s3.amazonaws.com/fvd-data/notes/377895/1425527819-t9pwAe/screen.png)

I then tried to pass the parameters and got frustrated when I passed the space character %20 and 0000 to no avail. Utilizing the 'try-harder' mentality, I discovered that the successful username is actually 'blank' and the password is '0000'. The following URL correctly leads to the solution.

{% highlight http %}
http://compete.sctf.io/problems/2015q1/impromptuget.php?username=blank&password=0000
{% endhighlight %}


<strong>Difficulty: </strong> 3
<br>
<strong>Fun: </strong> 4
                                                                
