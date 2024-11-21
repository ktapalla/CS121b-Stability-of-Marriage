# README - COSI 121b The Stability of Marriage PS

The code provided in this repository contains the solutions to the Stability of Marriage Problem Set for COSI 121b - Structure and Interpretations of Computer Programs. A general description of the assignment and its relevant problems will be provided below. 

## Installation and Execution 

Get the files from GitHub and in your terminal/console move into the folder of the project. Run the following line to open the program in DrRacket: 

``` bash 
drracket marry-code.rkt 
```

This will open up your DrRacket application where you will be able to run the program. Click the button labeled "Run" at the top right of the DrRacket Application window, which will allow the user to type the appropriate commands on the REPL.

Note: The instructions above assume that the user already has Racket and DrRacket installed on their device and the executable command of ``` drracket ``` added to their ``` $PATH ``` as an executable command. If the user does not have this done already, they can follow the steps at the following link to do so: 

https://docs.racket-lang.org/pollen/Installation.html 

Following the first four bullets under the section '1.2 Installation' will be enough. 

If the user would rather not open the program through the terminal, then they can also just make sure that they have DrRacket installed and open the ``` marry-code.rtk ``` file on the application directly. 


## Assignment Instructions 

### Background Information/Premise 
Let's assume, for the sake of an argument, that you are a village matchmaker given the task of marrying 100 men and 100 women. Each of the men has ranked the women from 1 to 100 in the order of his preference; in turn, each woman has similarly ranked the 100 men. As a matchmaker, it is clear that in producing 100 couples, you will not be able to give each person his first choice: for example, if Alan is the first choice of all women, only one will get him, and all other women will be left with their second (or worse) choices. 

Rather than insist that everyone get their first choice, you are instead charged with creating 100 stable marriages. A set of marriages is said to be stable if there exists no man *m* and woman *w* such that *m* likes *w* better than his wife, and *w* likes *m* better than her husband. The notion is called "stability" as *m*'s and *w*'s marriages are unstable, since *m* and *w* could optimize their sorry lot in life by leaving their mates and running off together. 

### The Algorithm 

We first describe in English an algorithm to find stable marriages. Each person has a preference list of members of the opposite sex. The first time a person proposes, it is to their number one choice, the second time to their number two choice, and so on. We will assume, without loss of non-sexist generality, that men always propose to women (although there is no reason that it couldn't happen the other way around: see Problem 7), and that proposals occur in rounds. At any moment in time, each person is either engaged or unengaged, and initially everyone is unengaged. (Assuming heterosexual alliances only, we can further- in the interest of mathematical simplicity- assert that the number of engaged men equals precisely the number of engaged women.) 

At the start of a round, each unengaged man is ordered by you, the matchmaker, to propose to the woman he loves most but has yet to whom he has not proposed. Each woman responds according to her status as given in the following case analysis: 

* Unengaged, Received no proposals - Sit tight, life is bound to improve 
* Unengaged, Received one proposal - Accept the proposal (the man and woman are now engaged) 
* Unengaged, Received multiple proposals - Accept the proposal you like the best based on your preference list, rejecting any other suitors 
* Engaged, Received no proposals - Declare your eternal and undying love to your intended partner 
* Engaged, Received one proposal - If you like the man who proposed more than your current partner, dump your fiance and reengage yourself to this more inviting gentleman. You and the proposer are now engaged; Mr. Dumped is not unengaged. Otherwise, say "I'm flattered but I'm not interested," and declare your undying love for your intended partner. 
* Engaged, Received multiple proposals - Choose the proposal you like best by looking at your preference list, and act as if you are currently engaged and this gentleman has proposed (see one bullet above). 

At the end of a round and the ensuing musical chairs, some men are engaged and others are not. If everyone is engaged, stop: the current pairs are the marriages that the matchmaker seeks. Otherwise, do another round. 

Of course, no assurances are made that the marriages produced are stable, or even that everyone is engaged in the end. For example, is it possible that a man proposes 100 times, exhausting his proposal list, and gets rejected every time? We'll address these questions later on; for the moment, we assume that the method works correctly. 

### Problem 1

Write the following procedures: 

* ``` (courtship <unengaged_proposers> <proposers> <proposees>) ``` - An implementation of the Stable Marriage algorithm describes above, where a subset of the proposers (namely, the unengaged proposers) propose marriages to the proposees. Note that while for the moment we assume that < proposers > is a list of men and < proposees > is a list of women, we are not assuming that men-procedures are structurally different from women-procedures, i.e., they are both produced by ``` make-person ```. 
* ``` (couple? <person1> <person2>) ``` - A predicate telling whether two people are engaged to each other 
* ``` (currently-unengaged <list>) ``` - A procedure returning a list of the people appearing as elements of < list > who are not engaged 
* ``` (send <list> <message>) ``` - Sends a given message to each person in the list, for example ``` (send list-of0men 'propose) ```
* ```(i-like-more? <person1> <person2>) ``` - A predicate telling whether the first argument is liked more than the second argument by a particular person/procedure. Note: this procedure has to be defined in the correct lexical context to be able to access and manipulate the proper data structures. 

### Problem 2 

Complete the part of ``` make-person ``` that handles the message i-love-you. 

### Problem 3 

Add dialogue to the algorithm, so that (say) proposals, acceptances, and engagement breakings are printed at the terminal as the stable marriage algorithm continues. 

### Problems 4-7

N/A - Written problems 
