# Monte-Hall-Game-Simulator
 

## Introduction

During the 1960s & 1970s there was a prominent American television game show called *Let's make a deal* who's host was Monte Hall. As part of the show, usually participants or contestants would be shown 3 doors, each one having the possibility of containing a car. However, if the contestant guessed wrong, they received a goat instead of the car. 
  
As part of the game, you are allowed to choose one door. Then, before revealing what is behind the door the contestant chose, Monte Hall would reveal another door containing a goat behind it. He would then ask if the contestant would like to switch doors. So should the contestant stick with their first option or switch doors?
<p>&nbsp;</p> 
  
## Probability
  
Initially, the contestant makes a decision to pick a door, with a  &frac23; chance that the car is behind another door that the contestant did not choose. However, when the host decides to open one of the doors and then lets the contestant know that one of the doors that was not picked by the contestant does not have a car behind it, the hosts actions *add value* to the door that was *not chosen* to be revealed and eliminated, so the  &frac23; probability of winning is essentially placed on one door instead of two, making the unchosen and unrevealed door twice as likely to win the prize.

In order to demonstrate this, we will use *Python* and two libraries, *NumPy* and *Matplotlib*, to show the Monte Hall game, along with a simulator, using code.
<p>&nbsp;</p> 

## Code
  
