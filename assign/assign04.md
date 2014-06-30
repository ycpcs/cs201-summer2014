---
layout: default
title: "Assignment 4: Klondike (Solitaire)"
---

Milestone 1 due **Thursday, July 3rd**

Milestone 2 due **Tuesday, July 15th**

Getting Started
===============

This assignment will use your code from [Lab 10](../labs/lab10.html) as a starting point.

Download [CS201\_Assign04.zip](CS201_Assign04.zip) and import it into your Eclipse workspace (**File&rarr;Import&rarr;General&rarr;Existing projects into workspace&rarr;Archive file**.) You should see a project called **CS201\_Assign04** in the Package Explorer.

Right click on **StartAssignment.java** and choose **Run As&rarr;Java Application**. In the console window, type **yes** when prompted. When the program completes, right click on the project (**CS201\_Assign04**) and choose **Refresh**. You should see your code from [Lab 10](../labs/lab10.html).

Note that there are two milestones.

Your Task
=========

Your task is to implement the card game called [Klondike](http://en.wikipedia.org/wiki/Klondike_(solitaire\)). You may be familiar with the game from the [classic Windows game "Solitaire"](http://en.wikipedia.org/wiki/Solitaire_(Windows\)).

You can import my solution into Eclipse in order to see how the game should work:

> [CS201\_Assign04\_Solution.zip](CS201_Assign04_Solution.zip)

Note that this solution has no source code other than **Main.java**, the class containing the **main** method. You are welcome to use the **Main.java** from the solution as a starting point for your program, but you are not required to.

Also, see [the transcript of the game](assign04transcript.html) (with user input in **bold**). It shows how the gameplay proceeds.

<div class="callout"> This is a substantial project. Do not wait until the last minute to start it! </div>

Rules of the game
=================

A game of Klondike consists of

-   the main deck, which is a pile of cards with the top card turned over
-   seven tableau piles of cards
-   four foundation piles of cards

A tableau pile consists of 0 or more hidden cards at the bottom of the pile. If a tableau pile is non-empty, then it has at least one exposed card on the top of the pile. A tableau pile may have more than one exposed card. Note that a tableau pile never contains a hidden card placed on top of an exposed card.

At the beginning of the game, the first tableau pile has one card, the second has two cards, etc.

A foundation pile contains cards of the same suit, arranged in order from Ace at the bottom of the pile to King at the top of the pile. (In Klondike, Aces are low.) There are four foundation piles, one for each suit.

On each turn, a player may either

-   draw another card from the main deck
-   move one or more cards

Drawing a card from the main deck means removing the current top card and placing it in a waste pile. The new top card on the main deck is then exposed. If the main deck is empty, then all of the cards are transferred from the waste pile back to the main deck. (Following the transfer of cards from the waste pile back to the main deck, they should appear in the order in which they originally occurred.)

Moving a card transfers one or more cards from either the main deck or a tableau pile to a tableau pile or a foundation pile. Moves must be done following the rules of the game, which are as follows:

-   Only the top card may be removed from the main deck.
-   Only exposed cards may be moved. (Hidden cards may not be moved.)
-   The cards moved are placed on top of whatever pile they are moved to.
-   When multiple cards are moved (from a tableau pile), the cards cannot be removed from the "middle" of the pile. Instead, a chosen card and all cards on top of it must be moved.
-   The colors of the cards in a tableau pile must alternate red and black. Clubs and Spades are black suits, and Diamonds and Hearts are red suits.
-   When a card or cards are moved onto an empty tableau pile, the new bottom card must be a King.

Following a move, the top card of the pile the card or cards were moved from is exposed (if the pile is not empty.)

Progam requirements
===================

Your program should shuffle the main deck, deal cards into the tableau piles, and then allow the user to play the game by repeatedly drawing the next card from the main deck, or moving exposed cards. Before each turn, the program should print a representation of the game state showing

-   how many cards are in the main deck,
-   which card is on top of the main deck
-   the top card in each foundation pile
-   all hidden and exposed cards in each tableau pile (print "xx" for hidden cards)

User input must be validated. If the user enters invalid input, the game state should be printed again and the user reprompted to enter valid input.

**All of your classes and methods must be documented with javadoc comments.** A [javadoc comment](http://www.oracle.com/technetwork/java/javase/documentation/index-137868.html) describes the purpose of a class or method. For methods, it also describes important details about the method such as what parameter values it takes, what kind of value it returns, and which exceptions (if any) it can throw.

**Your methods must contain appropriate comments.** I expect to see comments describing important sections of code: for example, to determine when a move is legal, to move cards, the check to see if the user has won the game, etc.

All comments should be well-written and professional.

Milestones
==========

There are two milestones.

**Milestone 1**: The program must create the initial tableau piles, and allow the player to either draw a card from the main deck or move a card. If the player chooses a move, the program must check the validity of the move. However, the program does not need to carry out the draw or move: that is the task in Milestone 2.

**Milestone 2**: Allow the player to play a complete game. When a legal move is chosen, the move should be carried out by moving cards between piles as appropriate according to the rules of the game. The player should detect when the player has won and print a message as appropriate.

Hints
=====

These hints describe the approach I used. You may follow this approach, or you may use your own design.

**Important consideration**:

> In good object-oriented design, it is important to separate the *user interface* classes from the *model classes*.
>
> A model class is one that represents a concept in the problem domain of the program. In the case of Klondike, the model classes would be Game, Deck, Card, Suit, Rank, etc.
>
> A user interface class is one that allows the user to interact with the program.
>
> One important way you can tell if you have separated the user interface from the model classes in a program that has a textual interface is that you will not have any calls to user input or output methods (e.g., **System.out.println**, **nextInt** on a **Scanner**, etc.) in the methods of the model classes.
>
> The **Main.java** provided in the solution code contains all of the user input and output code.

toString methods
----------------

You can add a **toString** method to classes where you want to provide a way to convert objects into strings for printing.

<div class="callout"> To use the card suit characters (♣,♦,♥,♠), you will need to change the text encoding of your Java source files to UTF-8. See <a href="http://stackoverflow.com/questions/200691/how-to-use-special-chars-in-java-eclipse">this StackOverflow question</a> for details. </div>

The **toString** method is defined in the **java.lang.Object** class as follows:

{% highlight java %}
public String toString()
{% endhighlight %}

I defined the **toString** method of the **Card** class as

{% highlight java %}
public String toString() {
    return rank.toString() + " of " + suit.toString();
}
{% endhighlight %}

I defined the **toString** method of the **Rank** enumeration as

{% highlight java %}
public String toString() {
    if (this == TWO) {
        return "2";
    } else if (this == THREE) {
        return "3";
    }
    // ... etc ...
{% endhighlight %}

Similarly, the **toString** method in the **Suit** enumeration can be defined as

{% highlight java %}
public String toString() {
    if (this == CLUBS) {
        return "♣";
    } else if (this == DIAMONDS) {
        return "♦";
    }
    // ... etc ...
{% endhighlight %}

Defining **toString** methods makes it easy to include concise representations of card objects in the program output.

CardLocation
------------

An instance of the **CardLocation** class represents one of the cards the player can choose to move. Its data consists of the index of one of the piles, and the index of a card within the chosen pile.

Game class
----------

Write a class called **Game** representing the current state of the game. This class can have methods to determine which moves are legal, and to carry out those moves.

Here are some of the methods I added to my **Game** class:

-   public Deck getMainDeck()
-   public Deck getPile(int index)
-   public boolean isFinished()
-   public boolean isValidTakeLocation(CardLocation takeLocation)
-   public boolean isValidMove(CardLocation takeLocation, int placePileIndex)
-   public void moveCards(CardLocation takeLocation, int placePileIndex)
-   public void drawNextCard()

You can see my implementation of **Main.java** to see how these methods are used.

The most interesting methods are **isValidTakeLocation** and **isValidMove**. **isValidTakeLocation** determines if the card selected by the user can be legally moved. **isValidMove** determines if it is legal to move the card selected by the user to a particular pile.

The **moveCards** method moves the cards selected by the user to a particular pile.

Deck class
----------

You can use instances of the **Deck** class to represent the piles. Since the piles are numbered (0 = main deck, 1-7 = tableau piles, 8-11 = foundation piles), an array of references to **Deck** objects is a good way to store the **Deck** objects representing the piles.

You can also use a **Deck** object to represent the waste pile.

If you use the **Deck** class to implement your piles, you will want to move the code in the constructor which adds the 52 cards to a separate method. The **Deck** representing the main deck should start out with 52 (shuffled) cards. You can use the **drawCard** method on the main deck to deal cards to the seven tableau piles.

Here are some of the methods I added to my **Deck** class:

-   public void add(Card card)
-   public Card getTopCard()
-   public void setExposeIndex(int index)
-   public int getExposeIndex()
-   public int indexOfTopCard()
-   public ArrayList&lt;Card&gt; removeCards(int index)
-   public void placeCards(ArrayList&lt;Card&gt; cardsToPlace)

The "expose index" of a deck is the index of the first exposed card in the deck. For example, if a deck has 6 cards and the expose index is 3, then the cards with indices 3, 4, and 5 are exposed.

The **removeCards** and **placeCards** methods are used to move cards from one pile to another. **removeCards** removes all cards starting at the one whose index is given. **placeCards** places a sequence of cards on top of a deck.

Grading
=======

Milestone 1:

-   Initializing and printing the initial state: 50
-   Allow player to choose a move or draw: 10
-   If a move is chosen, check whether it is legal: 30
-   Good coding style: 5
-   Good comments: 5

Milestone 2:

-   Player can move cards (for legal moves): 30
-   Support drawing next card from main deck (adding current top card to waste pile): 20
-   Waste pile is recycled when the main deck becomes empty: 10
-   Game loop (player can make progress my making a series of moves): 25
-   Checking end of game condition: 5
-   Good coding style: 5
-   Good comments: 5

Credit may be deducted for poor programming style (inconsistent indentation, poorly-chosen variable/method names, failure to make fields private, unnecessary use of static fields, etc.)

There is one extra credit option for Milestone 2:

-   Implement a graphical user interface (GUI): up to 50 points

The GUI implementation will be similar to [Lab 6](../labs/lab06.html) and [Assignment 3](assign03.html). The GUI should be able to use a **Game** object in order to represent the game state, check and carry out legal moves, etc.

> <div class="callout"><b>Important</b>: Do not start the GUI unless your program satisfies all of the requirements described above.</div>

Submitting
==========

When you are done, submit the lab to the Marmoset server using either of the methods below.

> **Important**: after you submit, log into the submission server and verify that the correct files were uploaded. You are responsible for ensuring that you upload the correct files. I may assign a grade of 0 for an incorrectly submitted assignment.

From Eclipse
------------

If you have the [Simple Marmoset Uploader Plugin](../resources.html) installed, select the project (**CS201\_Assign04**) in the package explorer and then press the blue up arrow button in the toolbar. Enter your Marmoset username and password when prompted. There are two inboxes, **assign04\_ms1** and **assign04\_ms2**, corresponding to the two milestones for the assignment: make sure you choose the one that is appropriate.

From a web browser
------------------

Save the project (**CS201\_Assign04**) to a zip file by right-clicking it and choosing

> **Export...&rarr;Archive File**

Upload the saved zip file to the Marmoset server as **assign04\_ms1** (Milestone 1) or **assign04\_ms2** (Milestone 2). The server URL is

> <https://cs.ycp.edu/marmoset/>
