---
id: 97
title: The Monty Hall Problem (Part 2)
date: 2013-06-16T15:38:14+00:00
author: Mike Conroy 
layout: post
guid: http://mikepconroy.com/?p=97
permalink: /2013/06/the-monty-hall-problem-part-2/
categories:
  - Computing
tags:
  - Java
  - maths
  - probability
  - programming
  - statistics
---
If you are unfamiliar with The Monty Hall Problem please read the first part of this blog post [here.]({{ site.baseurl }}{% link _posts/2013-06-16-the-monty-hall-problem-part-1.md %})

![Overview](/assets/images/MontyHall/overview.png){:data-action="zoom" .centre-image}
          
Due to my interest in programming and interest in this problem I decided to bring the two together and created a program that replicates the situation and outputs the statistics of wins and losses with switches and without (where the results can be seen further down).
          
**Computing the Problem**
          
I have uploaded the source code to the program which can be found <a href="https://github.com/mikecon94/TheMontyHallProblem/blob/master/MontyHallProblem.java" target="_blank">here.</a>
          
The program works by creating 3 doors at the start of each game and randomly choosing 1 to be the winner. The program then asks the user to pick one of the doors either 1, 2 or 3, after this it will then display one of the other doors (if the user has picked the winning door it will randomly choose one of the other 2 doors to show). The user is then given the choice to switch the door if they want to. The program then tells the user if they won or lost and prints out all the statistics of the total games which can be viewed below.
          
To make it easier to quickly run the program multiple times I created short java program to produce a file that can then be fed into the standard input of the main file to run the game 1000&#8217;s of time quickly and view the results. That program can be found <a href="https://github.com/mikecon94/TheMontyHallProblem/blob/master/PrintFile.java" target="_blank">here.</a>
          
**The Results**
          
I ran the program multiple times using the file printing program to give me a different number of inputs each time from 20 games to 20,000 here you can see the screenshots of the results below.

{% include image.html url="/assets/images/MontyHall/20games.png" description="Results of 10 switches and 10 none switches." %}

{% include image.html url="/assets/images/MontyHall/200games.png" description="Results of 100 switches and 100 none switches." %}

{% include image.html url="/assets/images/MontyHall/2000games.png" description="Results of 1000 switches and 1000 none switches." %}

{% include image.html url="/assets/images/MontyHall/20000games.png" description="Results of 10000 switches and 10000 none switches." %}
         
The main point of interest of these results is the percentages, and for anyone who wasn&#8217;t convinced of the solution to the problem these results clearly show that you have a greater chance of winning if you change from your original choice (as you&#8217;d expect). Also, we can see that the more games that are played the closer we get to the values of 1/3 (wins without switching) and 2/3 (wins with switching).
