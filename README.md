<p align="center">
 <img src="https://github.com/johnbaguinaga/Monte-Hall-Game-and-Probability/assets/106455858/67c7464c-ef61-4031-aacc-32c132ad324d" width="450" height="200">
</p>
  
  
# Monte Hall Game and Probability
 

## Introduction

During the 1960s & 1970s there was a prominent American television game show called *Let's make a deal* who's host was Monte Hall. As part of the show, usually participants or contestants would be shown 3 doors, each one having the possibility of containing a car. However, if the contestant guessed wrong, they received a goat instead of the car. 
  
As part of the game, you are allowed to choose one door. Then, before revealing what is behind the door the contestant chose, Monte Hall would reveal another door containing a goat behind it. He would then ask if the contestant would like to switch doors. So should the contestant stick with their first option or switch doors?
<p>&nbsp;</p> 
  
## Probability
  
Initially, the contestant makes a decision to pick a door, with a  &frac23; chance that the car is behind another door that the contestant did not choose. However, when the host decides to open one of the doors and then lets the contestant know that one of the doors that was not picked by the contestant does not have a car behind it, the hosts actions *add value* to the door that was *not chosen* to be revealed and eliminated, so the  &frac23; probability of winning is essentially placed on one door instead of two, making the unchosen and unrevealed door twice as likely to win the prize.

In order to demonstrate this, we will use *Python* and two libraries, *NumPy* and *Matplotlib*, to show the Monte Hall game, along with a simulator, using code.
<p>&nbsp;</p> 

## Code
  
*We're going to create the doors, along with the "prizes" randomly shuffled behind each door in a two dimensional array. One row represents the door, the other represents the prizes.*
```
import numpy as np
from matplotlib import pyplot as plt

def game_setup():
    doors = np.array([1,2,3])
    prizes = np.array([0,0,1])
    np.random.shuffle(prizes)
    dandp = np.vstack((doors,prizes))
    return dandp
```

<p>&nbsp;</p>
    
*Calling the function:*
```
game_setup()
```
*Output:*
```
array([[1, 2, 3],
       [0, 1, 0]])
```

<p>&nbsp;</p>
  
*Now we're going to make that asks user input and returns the door chosen by the user*
```
def choose_door():
    game_setup()
    while True:
        try:
            x = int(input("Enter a Door # (1-3): "))
        except ValueError:
            print("Error! input must be an integer 1-3.")
            continue
        if x < 1 or x > 3:
            print("Error! input must be an integer 1-3.")
            continue
        else:
            break
    print("You chose Door # {a}".format(a=x))
    door = game_setup()[0][x-1]
    return door
```

<p>&nbsp;</p>
 
*Calling the function:*
```
choose_door()
```
  
*Output:*
```
Enter a Door # (1-3): 1
You chose Door # 1
1
```

<p>&nbsp;</p>

*Next, we make a function that is going to ask the user whether they would like to stay with the original door they chose or if they would like to switch, along with checking for input errors*
```
def switch_stay():
    doorprize = dict(zip(game_setup()[0],game_setup()[1]))
    doorpick = choose_door()
    print('')
    doors = [1, 2, 3]
    while True:
        x = np.random.choice(doors)
        if doorprize[x] == 0 and x != doorpick:
            print("The host opens Door # "+str(x)+" and the prize for this door is a goat.")
            break
            
    while True:
        try:
             switchorstay = input("Would you like to switch to the unknown door or stay?(Enter 'switch' or 'stay'): ")
        except ValueError:
            print("Error! you must choose to switch or stay.")
            continue
        if switchorstay == 'switch':
            break
        if switchorstay == 'stay':
            break
        else:
            print("Error! you must choose to switch or stay.")
            continue

    if switchorstay == 'stay':
        print("You stayed with Door # {a}".format(a = doorpick))
        return doorpick
    if switchorstay == 'switch':
        for i in doors:
            if i != doorpick and i != x:
                doorpick = i
                break
        print("You switched to Door # {a}".format(a = doorpick))
        return doorpick
``` 

<p>&nbsp;</p>
  
*Calling the function:*
```
switch_stay()
```
  
*Output:*
```
The host opens Door # 2 and the prize for this door is a goat.
Would you like to switch to the unknown door or stay?(Enter 'switch' or 'stay'): 1
Error! you must choose to switch or stay.
Would you like to switch to the unknown door or stay?(Enter 'switch' or 'stay'): a
Error! you must choose to switch or stay.
Would you like to switch to the unknown door or stay?(Enter 'switch' or 'stay'): switc
Error! you must choose to switch or stay.
Would you like to switch to the unknown door or stay?(Enter 'switch' or 'stay'): switch
You switched to Door # 3
3
```

<p>&nbsp;</p>

*Once all the individual game pieces have been finished, we're going to create the entire Monte Hall game itself within a function*
```
def mhgame():
    print("Welcome to Let's Make a Deal!")
    doorprize = dict(zip(game_setup()[0],game_setup()[1]))
    doorpick = choose_door()
    print('')
    doors = [1, 2, 3]
    while True:
        x = np.random.choice(doors)
        if doorprize[x] == 0 and x != doorpick:
            print("The host opens Door # "+str(x)+" and the prize for this door is a goat.")
            break
            
    while True:
        try:
             switchorstay = input("Would you like to switch to the other unknown door or stay?(Enter 'switch' or 'stay'): ")
        except ValueError:
            print("Error! you must choose to switch or stay.")
            continue
        if switchorstay == 'switch':
            break
        if switchorstay == 'stay':
            break
        else:
            print("Error! you must choose to switch or stay.")
            continue

    if switchorstay == 'stay':
        print("You stayed with Door # {a}".format(a = doorpick))
    if switchorstay == 'switch':
        for i in doors:
            if i != doorpick and i != x:
                doorpick = i
                break
        print("You switched to Door # {a}".format(a = doorpick))
    if doorprize[doorpick] == 1:
        print("Congratulations, you won the car!")
    else:
        print("You won the goat.")
```

<p>&nbsp;</p>

*Calling the function:*
```
mhgame()
```
  
*Output:*
```
Welcome to Let's Make a Deal!
Enter a Door # (1-3): 2
You chose Door # 2

The host opens Door # 1 and the prize for this door is a goat.
Would you like to switch to the other unknown door or stay?(Enter 'switch' or 'stay'): stay
You stayed with Door # 2
You won the goat
```

<p>&nbsp;</p>

*Let's try the game another time...*
  
<p>&nbsp;</p>

*Calling the function:*
```
mhgame()
```

*Output:*
```
Welcome to Let's Make a Deal!
Enter a Door # (1-3): 3
You chose Door # 3

The host opens Door # 1 and the prize for this door is a goat.
Would you like to switch to the other unknown door or stay?(Enter 'switch' or 'stay'): switch
You switched to Door # 2
Congratulations, you won the car!
```

<p>&nbsp;</p>

*Since we know the game works, now we can automate it to run on its own by having a door chosen at random without user input. We also include a feature where the automated user will switch doors, depending on whether we use true or false*
```
def automhgame():
    doors = np.array([1,2,3])
    prizes = np.array([0,0,1])
    np.random.shuffle(prizes)
    dandp = np.vstack((doors,prizes))

    doorprize = dict(zip(doors,prizes))
    doors = [1, 2, 3]
    doorpick = np.random.choice(doors)
    while True:
        x = np.random.choice(doors)
        if doorprize[x] == 0 and x != doorpick:
            break
       
    switch = True

    if switch == 1:
        for i in doors:
            if i != doorpick and i != x:
                doorpick = i
                break

    if doorprize[doorpick] == 1:
        return 1
    else:
        return 0
```

<p>&nbsp;</p>

*Calling the function:*
```
automhgame()
automhgame()
automhgame()
```
  
*Output:*
```
1
0
1
```

<p>&nbsp;</p>
  
  
*Finally, by running a chosen number of simulations, we can use the automated game output within an ndarray to plot the outcomes of each game and create a distribution of the "winners".*  
  
<p>&nbsp;</p>

*When the default switch is true:*
```
num_trials=100
a = []
for i in range(num_trials):
    for j in range(num_trials):
        a.append(automhgame())
x = (np.asarray(a))
x = np.reshape(x,(num_trials,num_trials))

winners = np.sum(x,axis = 1)

plt.hist(winners, bins = 15, range = (min(winners),max(winners)))
plt.title("Winners")
plt.show()

print("mean of winners: ", np.mean(winners))
print("median of winners: ", np.median(winners))
```

<p>&nbsp;</p>

*Output:*

```
mean of winners:  66.01
median of winners:  65.0
```

![trial1](https://user-images.githubusercontent.com/106455858/223843153-0ac17860-774e-4166-9655-750d8832c253.png)

<p>&nbsp;</p>

*Then we set the switch door option to "False" in our automated user input as part of our trials. The result is much different:*
```
mean of winners:  32.44
median of winners:  32.0
```
  
![winnersnoswitch](https://user-images.githubusercontent.com/106455858/223844332-b6acce49-ca20-4191-9093-dbe082154c92.png)

## Conclusion

Ultimately, we were able to show that, by understanding elementary probability, we decided on a different course of action which had substantial effects on our simulated game. When we defaulted and let the automated user in our game switch doors, the mean of our one-hundred 100 trials, was about 66. In other words, if we run the game and switch every single time we have the opportunity to do so, we have a 66% chance of winning. 
  
However, when we set the automated user to stay with the door (Switch = False), our mean dropped to about 33, which meant that the automated user only won 33% of the trials played if they decided to stay with the door they had originally chosen.  
  
In conclusion, intuition alone would have you believe the door choice did not matter. After closer examination and our understanding of simple probability, we learn that switching the door is the optimal strategy and should be done *every* time when playing this game. Although our example was basic, it delivers a valuable lesson in that probability is an incredibly important concept to decision-making and it's something that must be kept in mind when trying to make the most optimal choices given some uncertainties. 
