---
id: 176
title: How to mass unfollow on Twitter!
date: 2014-05-17T18:32:27+00:00
author: mikescom
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

<pre class="default prettyprint prettyprinted" style="color: #000000;"><code>&lt;span class="kwd" style="color: #00008b;">var el&lt;/span>&lt;span class="pun">=&lt;/span>&lt;span class="pln"> document&lt;/span>&lt;span class="pun">.&lt;/span>&lt;span class="pln">getElementsByClassName&lt;/span>&lt;span class="pun">(&lt;/span>&lt;span class="str" style="color: #800000;">'&lt;span style="color: #222222;">button-text unfollow-text&lt;/span>'&lt;/span>&lt;span class="pun">);
&lt;/span>&lt;span class="kwd" style="color: #00008b;">for&lt;/span>&lt;span class="pun">(&lt;/span>&lt;span class="kwd" style="color: #00008b;">var&lt;/span>&lt;span class="pln"> i&lt;/span>&lt;span class="pun">=&lt;/span>&lt;span class="lit" style="color: #800000;">0&lt;/span>&lt;span class="pun">; &lt;/span>&lt;span class="pln">i&lt;/span>&lt;span class="pun">&lt;&lt;/span>&lt;span class="pln">el&lt;/span>&lt;span class="pun">.&lt;/span>&lt;span class="pln">length&lt;/span>&lt;span class="pun">;&lt;/span>&lt;span class="pln"> i&lt;/span>&lt;span class="pun">++)&lt;/span>&lt;span class="pun">{&lt;/span>&lt;span class="pln">
    el&lt;/span>&lt;span class="pun">[&lt;/span>&lt;span class="pln">i&lt;/span>&lt;span class="pun">].&lt;/span>&lt;span class="pln">click&lt;/span>&lt;span class="pun">();
&lt;/span>&lt;span class="pun">}&lt;/span></code></pre>

5) Wait a second or two depending on how many users you are following.

Done!