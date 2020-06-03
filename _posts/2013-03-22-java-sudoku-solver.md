---
id: 49
title: Java Sudoku Solver
date: 2013-03-22T17:12:12+00:00
author: Mike Conroy
layout: post
guid: http://mikeconroy.com/?p=49
permalink: /2013/03/java-sudoku-solver/
comments: true
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

# Usage
  
The program reads the sudoku from a text file called &#8220;Sudoku.txt&#8221;. Which should be formatted like so:

{% highlight java %}
860020000
000700059
000000000
000060800
040000000
005300007
000000000
020000600
007509000
{% endhighlight %}

Where the 0s are the blanks in the given puzzle. The program will then print the solution to the command line.
  
When input the puzzle above:

![Example Output](/assets/images/sudoku/example.png){:data-action="zoom" .centre-image}

Here is the source code:

{% highlight java %}
import java.io.File;

public class SudokuSolver
{
  public static void main(String[] args) throws Exception
  {
    Scanner fileScanner = new Scanner(new File("Sudoku.txt"));

    int[][] sudoku = new int[9][9]; //Will hold the puzzle in a 2D array.
    //We will use this variable to hold the next line of the puzzle, then parse
    //each digit on that line.
	String line = fileScanner.nextLine();

    //Loops round placing the digits into the correct place of the array.
	for (int y = 0; y < 9; y++)
	{
	  for (int x = 0; x < 9; x++)
	  {
        //Gets the digit converts it from a char to an in and places it in the array.
        sudoku[y][x] = Character.getNumericValue(line.charAt(x));
        //At the end of each line we load the next line, but check there is a next
        //line before trying to load it so the program does not crash.
	    if (x == 8 && fileScanner.hasNextLine())
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
    if(cellY > 8)
    {
      printSudoku(sudoku);
      System.out.println();
      //System.exit(1); // = This will end the program quicker as it does not have to
      //"go back up" through the levels of recursion, but means the main
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
        //When at the end of a row add 1 to the row and reset the "column" to 0.
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
        //Otherwise, starting at 1 through 9 we check if the number is "legal"
        //and if so place that number, and move on to the next cell.
        for(int checkNum = 1; checkNum < 10; checkNum++)
        {
          if(checkSquare(sudoku, cellX, cellY, checkNum)
             && checkRow(sudoku, cellY, checkNum)
             && checkCol(sudoku, cellX, checkNum))
          {
            sudoku[cellY][cellX] = checkNum;
            solve(sudoku, nextX, nextY);
          }
        }
        //If we get to here it means in it's current state the sudoku is impossible
        //which means that one of the numbers we "placed" earlier is incorrect.
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

    //First we work out which column the "square" belongs to.
    //We take the given x value and if it is below 3 then that means
    //the square we need is in the first column (out of 3). etc.
    if(reqX < 3)
    {
      colX = 0;
    }
    else if (reqX < 6)
    {
      colX = 3;
    }
    else
    {
      colX = 6;
    }

    //We do the same but for the rows. For example if the y value is 5 then
    //the related square would be on the second row.
    if(reqY < 3)
    {
      rowY = 0;
    }
    else if (reqY < 6)
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
    for(int y = rowY; y < rowY + 3; y++)
    {
      for(int x = colX; x < colX + 3; x++)
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
    for(int x = 0; x < 9; x++)
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
    for(int y = 0; y < 9; y++)
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
    for(int y = 0; y < 9; y++)
	{
	  for(int x = 0; x < 9; x++)
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
{% endhighlight %}
