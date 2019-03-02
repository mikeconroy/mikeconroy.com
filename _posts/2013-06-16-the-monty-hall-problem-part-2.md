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
<p style="text-align: center;">
  <p style="text-align: center;">
    <p style="text-align: center;">
      <p style="text-align: center;">
        <p style="text-align: center;">
          <p style="text-align: center;">
            If you are unfamiliar with The Monty Hall Problem please read the first part of this blog post <a title="The Monty Hall Problem (Part 1)" href="//mikepconroy.com/?p=80">here.</a><a href="//mikepconroy.com/wp-content/uploads/2013/06/example.png"><img class="size-full wp-image-113 aligncenter" alt="The monty hall problem program" src="//mikepconroy.com/wp-content/uploads/2013/06/example.png" width="677" height="535" srcset="https://mikepconroy.com/wp-content/uploads/2013/06/example.png 677w, https://mikepconroy.com/wp-content/uploads/2013/06/example-300x237.png 300w, https://mikepconroy.com/wp-content/uploads/2013/06/example-624x493.png 624w" sizes="(max-width: 677px) 100vw, 677px" /></a>
          </p>
          
          <p>
            Due to my interest in programming and interest in this problem I decided to bring the two together and created a program that replicates the situation and outputs the statistics of wins and losses with switches and without (where the results can be seen further down).
          </p>
          
          <p>
            <strong>Computing the Problem</strong>
          </p>
          
          <p>
            I have uploaded the source code to the program which can be found <a href="https://github.com/mikecon94/TheMontyHallProblem/blob/master/MontyHallProblem.java" target="_blank">here.</a>
          </p>
          
          <p>
            The program works by creating 3 doors at the start of each game and randomly choosing 1 to be the winner. The program then asks the user to pick one of the doors either 1, 2 or 3, after this it will then display one of the other doors (if the user has picked the winning door it will randomly choose one of the other 2 doors to show). The user is then given the choice to switch the door if they want to. The program then tells the user if they won or lost and prints out all the statistics of the total games which can be viewed below.
          </p>
          
          <p>
            To make it easier to quickly run the program multiple times I created short java program to produce a file that can then be fed into the standard input of the main file to run the game 1000&#8217;s of time quickly and view the results. That program can be found <a href="https://github.com/mikecon94/TheMontyHallProblem/blob/master/PrintFile.java" target="_blank">here.</a>
          </p>
          
          <p>
            <strong>The Results</strong>
          </p>
          
          <p>
            I ran the program multiple times using the file printing program to give me a different number of inputs each time from 20 games to 20,000 here you can see the screenshots of the results below.
          </p><figure id="attachment_119" style="width: 676px" class="wp-caption aligncenter">
          
          <a href="//mikepconroy.com/wp-content/uploads/2013/06/20gamesCut.png"><img class="size-full wp-image-119" alt="Results of 10 switches and 10 none switches." src="//mikepconroy.com/wp-content/uploads/2013/06/20gamesCut.png" width="676" height="135" srcset="https://mikepconroy.com/wp-content/uploads/2013/06/20gamesCut.png 676w, https://mikepconroy.com/wp-content/uploads/2013/06/20gamesCut-300x59.png 300w, https://mikepconroy.com/wp-content/uploads/2013/06/20gamesCut-624x124.png 624w" sizes="(max-width: 676px) 100vw, 676px" /></a><figcaption class="wp-caption-text">Results of 10 switches and 10 none switches.</figcaption></figure> <figure id="attachment_122" style="width: 673px" class="wp-caption aligncenter"><a href="//mikepconroy.com/wp-content/uploads/2013/06/200gamesCut.png"><img class="size-full wp-image-122" alt="Results of 100 switches and 100 none switches." src="//mikepconroy.com/wp-content/uploads/2013/06/200gamesCut.png" width="673" height="132" srcset="https://mikepconroy.com/wp-content/uploads/2013/06/200gamesCut.png 673w, https://mikepconroy.com/wp-content/uploads/2013/06/200gamesCut-300x58.png 300w, https://mikepconroy.com/wp-content/uploads/2013/06/200gamesCut-624x122.png 624w" sizes="(max-width: 673px) 100vw, 673px" /></a><figcaption class="wp-caption-text">Results of 100 switches and 100 none switches.</figcaption></figure> <figure id="attachment_123" style="width: 674px" class="wp-caption aligncenter"><a href="//mikepconroy.com/wp-content/uploads/2013/06/2000gamesCut.png"><img class="size-full wp-image-123" alt="Results of 1,000 switches and 1,000 none switches." src="//mikepconroy.com/wp-content/uploads/2013/06/2000gamesCut.png" width="674" height="131" srcset="https://mikepconroy.com/wp-content/uploads/2013/06/2000gamesCut.png 674w, https://mikepconroy.com/wp-content/uploads/2013/06/2000gamesCut-300x58.png 300w, https://mikepconroy.com/wp-content/uploads/2013/06/2000gamesCut-624x121.png 624w" sizes="(max-width: 674px) 100vw, 674px" /></a><figcaption class="wp-caption-text">Results of 1,000 switches and 1,000 none switches.</figcaption></figure> <figure id="attachment_124" style="width: 672px" class="wp-caption aligncenter"><a href="//mikepconroy.com/wp-content/uploads/2013/06/20000gamesCut.png"><img class="size-full wp-image-124" alt="Results of 10,000 switches and 10,000 none switches." src="//mikepconroy.com/wp-content/uploads/2013/06/20000gamesCut.png" width="672" height="141" srcset="https://mikepconroy.com/wp-content/uploads/2013/06/20000gamesCut.png 672w, https://mikepconroy.com/wp-content/uploads/2013/06/20000gamesCut-300x62.png 300w, https://mikepconroy.com/wp-content/uploads/2013/06/20000gamesCut-624x130.png 624w" sizes="(max-width: 672px) 100vw, 672px" /></a><figcaption class="wp-caption-text">Results of 10,000 switches and 10,000 none switches.</figcaption></figure> 
          
          <p>
            The main point of interest of these results is the percentages, and for anyone who wasn&#8217;t convinced of the solution to the problem these results clearly show that you have a greater chance of winning if you change from your original choice (as you&#8217;d expect). Also, we can see that the more games that are played the closer we get to the values of 1/3 (wins without switching) and 2/3 (wins with switching).
          </p>
          
          <dl class="wp-caption aligncenter" id="attachment_104" style="width: 687px;">
            <dt class="wp-caption-dt">
            </dt>
          </dl>
