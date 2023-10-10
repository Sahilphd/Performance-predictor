Blackprint Technologies
-

The goal of this take-home interview is to evaluate your experience as a developer,
and ability to develop functional and well-engineered software. You have four hours
from the start of this assignment to submit working code for as many features as possible.

Intro
-

Go, an ancient Chinese game, is one of the oldest board games still played 
at a very serious professional level today.
It is played on boards of varying sizes, with various different scoring rules, 
but the fumdamentals of the game remain the same. For this take-home assigment,
your job will be to program a command-line, two player game of go on a 5x5 board.

Listed below are all of the features necessary for a complete, playable command-line
game of go. It is required that you implement them incrementally instead of using a 
waterfall approach, as you will be judged by all of the features you've implemented by the 
end of the interview even if the entire program isn't finished. 
Please implement each new feature as a branch, and then merge with the main branch after it 
has been implemented. We will check your commit history to ensure that the features have been implemented sequentially.


Rules
-

**Setup**

Go is a game played by two players, white and black, who continuously place stones in an
attempt to enclose territory. The squares on the board can be represented by a chess-like notation,
where the horizontal position of a square can be represented by capital letters A through E,
where a is the leftmost position and e is the rightmost value. The vertical position can be represented 
by numbers 1 through 5. Your implementation will represent an empty square with a '.', a white stone with 
'w', and a black stone with the letter 'b'. Your program will start off by printing an empty board,
and then prompting the first player to enter their move. (Black will always move first.) 
You CANNOT assume that users will always enter valid moves-if given an invalid input you should ask the
player to move again without updating the board.

**Example: (assume anything right of the colon is user input)**



``````Game started
1 . . . . .
2 . . . . .
3 . . . . .
4 . . . . .
5 . . . . .
  A B C D E


Turn 1- Black to move: A5


1 . . . . .
2 . . . . .
3 . . . . .
4 . . . . .
5 b . . . .
  A B C D E

Turn 1- White to move: C3

1 . . . . .
2 . . . . .
3 . . w . .
4 . . . . .
5 b . . . .
  A B C D E



Turn 2- Black to move: C2

1 . . . . .
2 . . b . .
3 . . w . .
4 . . . . .
5 b . . . .
  A B C D E
``````


**Capturing**
The empty intersections directly adjacent to a stone are called "liberties". In order
to remain on the board, a stone needs to have at least one 'liberty'. If its liberty becomes
plugged by an empty stone, the stone becomes captured. There are a few examples shown below:

```
1 . . . . .
2 w . b . .
3 . b w b .
4 . . . . .
5 w . . . .
  A B C D E

Turn 3- Black to move: C4

1 . . . . .
2 w . b . .
3 . b . b .
4 . . b . .
5 w . . . .
  A B C D E

Example 2

1 . w . . .
2 w . w . .
3 . w w b .
4 . b b . b
5 w . . . w
  A B C D E

Turn 13- Black to move: d5

1 . w . . .
2 w . w . .
3 . w w b .
4 . b b . b
5 w . . b .
  A B C D E
```
**Sharing liberties**
A stone cannot be taken by stones of it's own color. When stones of the same color touch,
they become part of a group and share their liberties. A group cannot be taken until all of 
its shared liberties are taken. 


**Example:**

```
1 b b b . .
2 w w . . .
3 b b b b .
4 . . b . .
5 w . . . .
  A B C D E

Turn 15- White to move: c2
 
1 b b b . .
2 w w w . .
3 b b b b .
4 . . b . .
5 w . . . .
  A B C D E
 
Turn 16- Black to move: d2
    

1 b b b . .
2 . . . d .
3 b b b b .
4 . . b . .
5 w . . . .
  A B C D E
```

A stone cannot be played in a spot where it would have no liberties, unless by doing so it could immediately 
capture another stone and in the process open up another liberty.

```
1 . . . . .
2 . . w b .
3 . w . w b
4 . b w b .
5 . . w . .


Turn 23- Black to move: c3

1 . . . . .
2 . . w b .
3 . w b . b
4 . b w b .
5 . . w . .
  A B C D E

```
**Endgame**
A game of go ends when both players decide that they have no moves 
left that help their position and decide to pass. Modify your input to accept a 
string value of "pass" as a valid move.
When a player passes, they place no stones and it becomes the other players turn.
If the other player passes afterwards, the game is over. In that case, your program should 
score the game by whoever has the most stones, print the winner and both player's scores,
and then exit.


**Bonus**:
To prevent a never-ending game, players cannot make a move that would repeat a
previously occuring position. 


**Bonus #2**:
Few serious go players consider 5x5 go anything more than a curiousity. Extend your
program to take a board size 'N' as your programs first argument, and start a game
on an NxN board with all of the same behavior as your 5x5 implementation.
(You can assume that N is between 0 and 27, exclusive)
