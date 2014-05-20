---
layout: default
title: "Assignment 1: Reversi"
---

Milestone 1 due **Tuesday, May 27th** by 11:59 PM

Milestone 2 due **Tuesday, June 3rd** by 11:59 PM

Getting Started
===============

Download [CS201\_Assign01.zip](CS201_Assign01.zip) and import it into your Eclipse workspace (**File** → **Import...** → **General** → **Existing Projects into Workspace** → **Select archive file**).

You should see a project called **CS201\_Assign01** in the Package Explorer.

Your will add your code to the file **Reversi.java**.

Your Task
=========

Your task is to implement a two-player version of the game [Reversi](http://en.wikipedia.org/wiki/Reversi), also known as Othello.

The "full" game of Reversi is played on an 8x8 grid. Your program will use a smaller 6x6 grid. The rows of the game board are numbered 1-6, and the columns of the game board have letters a-f.

Rules
-----

There are two players. The players take turns placing game pieces on the board. One player places black pieces, and the other places white pieces. Each time a player places a piece, any of the opponent's pieces that lie horizontally, vertically, or diagonally between the placed piece and another of the player's pieces are "captured", and change color to match the player's color. On each turn, a player must capture at least one of the opponent's pieces. If the player cannot capture any of the opponent's pieces, then her turn is skipped.

The board starts out in the following configuration:


<pre>
  abcdef
1 ......
2 ......
3 ..○●..
4 ..●○..
5 ......
6 ......
</pre>

The black player takes the first turn. Let's say that the black player places a piece at row 5, column d. This will have the effect of capturing the white piece at row 4, column d, since it is directly between the placed piece at 5d and the existing black piece at 3d. The board then looks like this:

<pre>
  abcdef
1 ......
2 ......
3 ..○●..
4 ..●●..
5 ...●..
6 ......
</pre>

Next, the white player takes a turn. Let's say that the white player places a piece at 5c. This will capture the black piece at 4c, resulting in the following board:

<pre>
  abcdef
1 ......
2 ......
3 ..○●..
4 ..○●..
5 ..○●..
6 ......
</pre>

The game proceeds until neither player can play a piece. The winner is the player with the most pieces at the end of the game. (A tie occurs if both players end up with the same number of pieces.)

Milestone 1
===========

For milestone 1, your program should allow the first player (black) to take a single turn.

-   print the game board
-   prompt the first player (black) to enter a row and column, and check to see whether that row or column corresponds to a legal move; if not, prompt the player to enter a different row/column, continuing until the player has entered a valid move
-   change the color of the captured piece(s)
-   print the final game board

Here is an example session (user input in **bold**):

<pre>
  abcdef
1 ......
2 ......
3 ..○●..
4 ..●○..
5 ......
6 ......

Black's turn
Row? (1-6) <b>4</b>
Column? (a-f) <b>e</b>

  abcdef
1 ......
2 ......
3 ..○●..
4 ..●●●.
5 ......
6 ......
</pre>

Another example session (user input in **bold**):


<pre>
  abcdef
1 ......
2 ......
3 ..○●..
4 ..●○..
5 ......
6 ......

Black's turn
Row? (1-6) <b>2</b>
Column? (a-f) <b>d</b>
Not a legal move!
Row? (1-6) <b>4</b>
Column? (a-f) <b>b</b>
Not a legal move!
Row? (1-6) <b>3</b>
Column? (a-f) <b>b</b>

  abcdef
1 ......
2 ......
3 .●●●..
4 ..●○..
5 ......
6 ......
</pre>

Milestone 1 hints
-----------------

*First and foremost*: implement the program incrementally. Make sure each feature works before attempting the next feature.

**Creating the board**: The **BOARD\_HEIGHT** and **BOARD\_WIDTH** constants specify the height and width of the game board.

Represent the board as a two-dimensional array of **int** values:

    int[][] board = new int[BOARD_HEIGHT][BOARD_WIDTH];

You can pass an array to a static method in Java in much the same way an array can be passed to a function in C.

Each element of the array represents one position on the game board. A 0 value indicates an empty position. You should store the constant values **BLACK** and **WHITE** (both of which are non-zero) to indicate positions indicated by black and white pieces, respectively.

You will need to set the group of 4 black and white pieces in the center of the board.

**Printing the board**: You can use the [Unicode](http://en.wikipedia.org/wiki/Unicode) black circle (●) and white circle (○) characters to represent black and white pieces on the board. You can print these characters as follows:

    System.out.println("\u25CF"); // print black circle
    System.out.println("\u25CB"); // print white circle

You should use a method to print the board, e.g.:

    private static void printBoard(int[][] board) {
        ...
    }

Note: if the circle characters appear as question marks in the Eclipse console, then you need to change the text encoding:

-   Right-click **Reversi.java**, choose **Run As -\> Run Configurations...**
-   Click the **Common** tab
-   Under "Encoding", click on **Other**, then choose **UTF-8**

**Getting user input**: Your **main** method should create a **Scanner** object to allow the program to get user input from the keyboard:

    Scanner keyboard = new Scanner(System.in);

You will need to pass the scanner to any static methods which need to get user input.

You can read the row number using the **nextInt** method on the scanner:

    int row;
    row = keyboard.nextInt();

Note that the rows are numbered 1-6, but the rows of the board array have indices 0-5, so you will need to subtract 1 to convert from row number to row index.

You can read the column by calling the **next** method, which returns a **String**, and then using the **charAt** method to get the first character of the string (which will be the letter entered by the user):

    String s;
    s = keyboard.next();
    char col = s.charAt(0);

You will need to ensure that the column entered is 'a', 'b', 'c', 'd', 'e', or 'f'. For example:

    if (col >= 'a' && col <= 'f') {
        // valid column
    } else {
        // invalid column
    }

You can convert the letter to a column index for the board array by subtracting the character code 'a' from it:

    int col_index = col - 'a';

**Checking that the move is legal**. This will be one of the more complicated parts of the assignment.

The easy part is checking to see if the row and column are in the legal range: any row other than 1-6 and any column other than a-f should be rejected.

Another easy part is checking to see if the row and column specifies a position that does not have a piece on it yet. It is not legal to place a piece on top of an existing piece.

The hard part is seeing if the move is *legal*. A legal move captures at least one of the opponent's pieces. In my implementation of the program, I used the following method:

    private static boolean traverse(
      int[][] board, int row, int col, int player, int dy, int dx, int mode) {
        ...
    }

This method works as follows. It assumes that a piece belonging to **player** (which is either **BLACK** or **WHITE**) will be placed at the given **row** and **col**. It then traverses on the board in the direction specified by **dy** and **dx** to see if one or more of the opponent's pieces lie between the piece being placed and another of the player's pieces. If so, it returns **true**. If not, it returns **false**. Note that the idea is only to check to see if any of the opponent's piece's *would be captured*, not to capture any pieces.

You can check to see if a move is legal by calling **traverse** in each of the eight possible directions in which the opponent's pieces can be captured: up, up+right, right, down+right, etc. If pieces can be captured in at least one direction, then the move is legal.

**Capturing pieces.** If you implement the **traverse** method as described above, you can use it to capture pieces. The idea is to use the **mode** parameter: when the constant value **CHECK** is passed, the method does not capture pieces, but when the constant value **CAPTURE** is passed, it captures pieces by changing the opponent's pieces to the player's until one of the player's pieces is encountered.

Milestone 2
===========

For milestone 2, your program should allow two players to alternate turns. The game should end when neither player has a legal move available. When the game finishes, the program should print a count of how many pieces each player has. The player with more pieces is the winner. Note that a tie is possible if both players have the same number of pieces.

[Click here for an example transcript of a complete game](assign01transcript.html).

Note that all of the milestone 1 requirements are still in effect: for example, if the player enters an invalid move, she should be prompted to enter a different move.

Milestone 2 hints
-----------------

**Alternating turns**: Use a variable to keep track of which player's turn it is. Initially, this variable should be set to **BLACK**. At the end of a turn, it is changed to the other player.

**Checking if a player has any legal moves**. Before prompting a player to choose a move, the program should check to see if there are any legal moves available. Assuming that you have a function to check whether a given it is legal for a player to move an a given position, you just need to call this function for all of the positions on the board and count how many times this function indicates that a legal move is possible.

Grading
=======

The grade for each milestone is out of 100 points.

Milestone 1:

-   Printing the initial board: 10
-   Allowing player to enter a move: 10
-   Checking whether the entered move is valid: 20
-   Allowing the player to re-enter row/column after an invalid move: 20
-   Capturing piece(s): 20
-   Printing the final board: 10
-   Coding style: 10

Milestone 2:

-   Milestone 1 features: 20
-   Allowing players to alternate turns: 20
-   Checking whether player has any legal moves, skipping player's turn if not: 20
-   Ending game when neither player has a legal move: 20
-   Printing the final piece counts, determining winner: 10
-   Coding style: 10

Coding style points are awarded for programs that have meaningful variable and method names, are properly indented, and have descriptive comments.

Submitting
==========

Use the [Simple Marmoset Uploader](../resources.html) plugin to submit the assignment.

There are two inboxes, **assign01\_ms1** and **assign01\_ms2**, corresponding to the two milestones for the assignment.
