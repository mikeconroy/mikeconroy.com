---
id: 49
title: Java Sudoku Solver
date: 2013-03-22T17:12:12+00:00
author: mikescom
layout: post
guid: http://mikepconroy.com/?p=49
permalink: /2013/03/java-sudoku-solver-2/
categories:
  - Technology
tags:
  - code
  - Java
  - programming
  - solver
  - source
  - sudoku
---
I have just uploaded a program I wrote a couple of weeks ago to <a title="GitHub" href="https://github.com/mikecon94/JavaSudokuSolver#readme" target="_blank">GitHub</a>. The program is a sudoku solver which I wrote in Java. I am also posting the source code below.

**Usage**
  
The program reads the sudoku from a text file called &#8220;Sudoku.txt&#8221;. Which should be formatted like so:

<pre class="brush: plain; title: ; notranslate" title="">860020000
000700059
000000000
000060800
040000000
005300007
000000000
020000600
007509000
</pre>

Where the 0s are the blanks in the given puzzle. The program will then print the solution to the command line.
  
When input the puzzle above:

<img class="aligncenter size-full wp-image-138" alt="Sudoku Solver" src="//mikepconroy.com/wp-content/uploads/2013/03/example.png" width="676" height="344" srcset="https://mikepconroy.com/wp-content/uploads/2013/03/example.png 676w, https://mikepconroy.com/wp-content/uploads/2013/03/example-300x152.png 300w, https://mikepconroy.com/wp-content/uploads/2013/03/example-624x317.png 624w" sizes="(max-width: 676px) 100vw, 676px" />

Here is the source code:

<pre class="brush: java; title: ; notranslate" title="">import java.util.Scanner;
import java.io.File;

public class SudokuSolver
{
  public static void main(String[] args) throws Exception
  {
    Scanner fileScanner = new Scanner(new File(&quot;Sudoku.txt&quot;));

    int[][] sudoku = new int[9][9]; //Will hold the puzzle in a 2D array.
    //We will use this variable to hold the next line of the puzzle, then parse
    //each digit on that line.
	String line = fileScanner.nextLine();

    //Loops round placing the digits into the correct place of the array.
	for (int y = 0; y &lt; 9; y++)
	{
	  for (int x = 0; x &lt; 9; x++)
	  {
        //Gets the digit converts it from a char to an in and places it in the array.
        sudoku[y][x] = Character.getNumericValue(line.charAt(x));
        //At the end of each line we load the next line, but check there is a next
        //line before trying to load it so the program does not crash.
	    if (x == 8 &amp;&amp; fileScanner.hasNextLine())
		{
		  line = fileScanner.nextLine();
		}
	  } //for x
    } //for y

    //The recursive function that actually solves the sudoku (starting at 0,0)
    solve(sudoku, 0, 0);

  } //main

  //This is a recursive function used to go through each cell and place a valid number.
  //Until they are filled in.
  private static void solve(int[][] sudoku, int cellX, int cellY)
  {
    //If the y value is 9 then the sudoku has been solved.
    if(cellY &gt; 8)
    {
      printSudoku(sudoku);
      System.out.println();
      //System.exit(1); // = This will end the program quicker as it does not have to
      //&quot;go back up&quot; through the levels of recursion, but means the main
      //routine will not continue running.
      //Also if there is more than one solution to the sudoku using this will only print
      //the first solution found.
    }
    else
    {
      //Here we calculate the next digit for the solve routine to try.
      int nextX = cellX;
      int nextY = cellY;
      if(cellX == 8)
      {
        //When at the end of a row add 1 to the row and reset the &quot;column&quot; to 0.
        nextX = 0;
        nextY++;
      }
      else
      {
        nextX++;
      }

      //If the digit was already given to us, we can move onto the next one.
      if(sudoku[cellY][cellX] != 0)
      {
        solve(sudoku, nextX, nextY);
      }
      else
      {
        //Otherwise, starting at 1 through 9 we check if the number is &quot;legal&quot;
        //and if so place that number, and move on to the next cell.
        for(int checkNum = 1; checkNum &lt; 10; checkNum++)
        {
          if(checkSquare(sudoku, cellX, cellY, checkNum)
             &amp;&amp; checkRow(sudoku, cellY, checkNum)
             &amp;&amp; checkCol(sudoku, cellX, checkNum))
          {
            sudoku[cellY][cellX] = checkNum;
            solve(sudoku, nextX, nextY);
          }
        }
        //If we get to here it means in it's current state the sudoku is impossible
        //which means that one of the numbers we &quot;placed&quot; earlier is incorrect.
        sudoku[cellY][cellX] = 0;
      }
    }
  }

  //This method is given a cell location and a number to check, it then checks
  //whether that number is already in the 3x3 square and returns false if so.
  private static boolean checkSquare(int[][] sudoku, int reqX, int reqY, int toCheck)
  {
    int rowY;
    int colX;

    //First we work out which column the &quot;square&quot; belongs to.
    //We take the given x value and if it is below 3 then that means
    //the square we need is in the first column (out of 3). etc.
    if(reqX &lt; 3)
    {
      colX = 0;
    }
    else if (reqX &lt; 6)
    {
      colX = 3;
    }
    else
    {
      colX = 6;
    }

    //We do the same but for the rows. For example if the y value is 5 then
    //the related square would be on the second row.
    if(reqY &lt; 3)
    {
      rowY = 0;
    }
    else if (reqY &lt; 6)
    {
      rowY = 3;
    }
    else
    {
      rowY = 6;
    }

    //We have now defined the square we need to check and have the top left
    //co-ordinate stored in the variables rowY and colX.
    //We now loop round and check each digit in the square, and if a digit matches
    //we return false.
    for(int y = rowY; y &lt; rowY + 3; y++)
    {
      for(int x = colX; x &lt; colX + 3; x++)
      {
        if(sudoku[y][x] == toCheck)
          {
            return false;
          }
      }
    }

    return true; //number not in the square.

  }

  //Checks if a given number is in a given row and returns false if it is.
  private static boolean checkRow(int[][] sudoku, int rowY, int toCheck)
  {
    //loops round each digit in a row.
    for(int x = 0; x &lt; 9; x++)
    {
      //Checks if the given number is the same as the current digit
      //and returns false if so.
      if (toCheck == sudoku[rowY][x])
      {
        return false;
      }
    }
    return true; //the number is not in the row.
  }

  //Checks if a given number is in a given column and returns false if it is.
  private static boolean checkCol(int[][] sudoku, int colX, int toCheck)
  {
    //Loops round each digit in a column.
    for(int y = 0; y &lt; 9; y++)
    {
      //Checks if the current digit is the given digit and returns false if so.
      if (toCheck == sudoku[y][colX])
      {
        return false;
      }
    }
    return true; //the number is not in the column.
  }

  //Prints the sudoku to the screen.
  private static void printSudoku(int sudoku[][])
  {
    //Loops round each digit and prints it.
    for(int y = 0; y &lt; 9; y++)
	{
	  for(int x = 0; x &lt; 9; x++)
	  {
	    System.out.print(sudoku[y][x]);
	    //Starts a new line when at the end of a row.
        if(x == 8)
		{
		  System.out.println();
		}
	  } //for x
	} //for y
  } //printSudoku
} //SudokuSolver
</pre>