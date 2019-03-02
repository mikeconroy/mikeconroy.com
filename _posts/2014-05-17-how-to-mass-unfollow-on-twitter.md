---
id: 176
title: How to mass unfollow on Twitter!
date: 2014-05-17T18:32:27+00:00
author: Mike Conroy
layout: post
guid: http://mikepconroy.com/?p=176
permalink: /2014/05/how-to-mass-unfollow-on-twitter/
categories:
  - Other
  - Technology
tags:
  - javascript
  - Twitter
  - unfollow
---
Yesterday, I wanted to unfollow everyone on an old account on Twitter. When searching Google for a tool to do this for me I found the ones that existed either weren&#8217;t very good or wanted a fee to do it (the tools that required a fee had many other options and features such as only unfollowing people who aren&#8217;t following you). After trying a couple of the tools I still had not managed to unfollow all the users I was following so decided to try and find my own solution and here it is:

1) Login to Twitter and click Following.

2) Scroll down to the bottom until everyone your following has loaded (Tip: press the end button to get to the bottom quicker).

3) Open up your browser console (CTRL + SHIFT + J for Chrome).

4) Copy & Paste the following Javascript and hit enter:

{% highlight javascript %}
var el= document.getElementsByClassName('button-text unfollow-text');
for(var i=0; i<el.length; i++){
    el[i].click();
}
{% endhighlight %}

5) Wait a second or two depending on how many users you are following.

Done!
