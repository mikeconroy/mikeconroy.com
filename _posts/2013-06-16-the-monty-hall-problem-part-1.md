---
id: 80
title: The Monty Hall Problem (Part 1)
date: 2013-06-16T13:45:47+00:00
author: Mike Conroy
layout: post
guid: http://mikepconroy.com/?p=80
permalink: /2013/06/the-monty-hall-problem-part-1/
categories:
  - Other
tags:
  - Java
  - maths
  - probability
  - programming
  - statistics
---
This part of the post is about explaining the problem itself and why the answer is what it is, whilst the second part is about computing the answer and &#8220;proving&#8221; it. Therefore, if you are already familiar with the problem skip to [Part 2]({{ site.baseurl }}{% link _posts/2013-06-16-the-monty-hall-problem-part-2.md %}) of the post.

Since reading about the problem in a <a title="book" href="http://en.wikipedia.org/wiki/The_Curious_Incident_of_the_Dog_in_the_Night-Time" target="_blank">book</a> when I was young, the monty hall problem, has always been something I have found interesting, and found myself on the <a title="Wikipedia page" href="http://en.wikipedia.org/wiki/Monty_Hall_problem" target="_blank">Wikipedia page</a> for it multiple times (including when it was used in one of Derren Browns shows, and in the movie <a title="21" href="http://en.wikipedia.org/wiki/21_(2008_film)" target="_blank">21</a>). So I decided to write a program that demonstrates it and write a blog post about it.

**The &#8220;Problem&#8221;**

Imagine you are on a game show and the host shows you 3 closed doors and asks you to pick one &#8211; either 1, 2 or 3. You are told that behind 2 of the doors there is a goat, but behind one of the doors is a grand prize of a car. After you have made your choice, let&#8217;s say you choose door number 1, the host (knowing which doors contain the goats) will then open one of the doors you haven&#8217;t picked to reveal a goat. For this example let&#8217;s say he shows you door number 2. After, showing you the goat behind this door, you are then given the option to swap your choice to the remaining door if you wish.

The question is, do you have a better chance of winning if you stick to your original choice (door 1) or are you more likely to win if you switch (to door 3)?
  
Or worded differently:
  
What are the chances of the car being behind door number 1, and the chances of it being behind door number 3?

**The Solution**

It seems like the answer is obvious &#8211; there is a 50% chance of winning whether you stick with your choice or if you switch, and therefore switching has no benefit. This answer is actually incorrect, despite it seeming so simple and clear.

The fact is you actually have 1 in 3 (33.33%) of chance of winning if you stick with your initial answer BUT if you decide to switch your chances of winning increase to 2/3 (66.66%).

**Explanation**

The main reason the chance of winning changes from 1/3 to 2/3 is because the host has to choose one of the losing doors.
  
On my first choice there is 1 in 3 chance of picking the grand prize, and a 2  in 3 chance of picking a goat.
  
If I pick a goat on my first choice (which is more likely), the host will then show the door which doesn&#8217;t have the car behind it, meaning when I switch I will win the car.

The <a title="Wikipedia page" href="http://en.wikipedia.org/wiki/Monty_Hall_problem#.27The_Economist.27" target="_blank">wikipedia</a> page does a nice job of explaining why the odds change, or if you prefer here is a youtube video which explains why (Skip to 2m 40s for the explanation of why):

<iframe width="560" height="315" src="https://www.youtube.com/embed/mhlc7peGlGg" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

The second part of this post can be found [here]({{ site.baseurl }}{% link _posts/2013-06-16-the-monty-hall-problem-part-2.md %}) where I discuss the program I created based on the problem and the results it produces.

&nbsp;
