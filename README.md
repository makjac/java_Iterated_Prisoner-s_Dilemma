
![Image Banner](baner.gif)
# Iterated Prisoner's Dilemma with one-step memory

The project undertakes the analysis of the iterated prisoner's dilemma with single-step memory. The main task is to create 32 strategies and then play a tournament where each strategy will compete against each other for 10 rounds. I will then analyze the data obtained and answer three questions: how do the polite strategies (those that start with C) perform? How do strategies that respond to an opponent's betrayal in the past perform? and how do those that respond to betrayal with cooperation perform?

Author:
- [Maksymilan Jackowski](https://github.com/makjac)

## Introduction

Imagine two people being interrogated. Both interrogators are suspected of committing some crime. There comes a moment when the detective asks them a question: who did the crime? Each interrogator has 2 choices: the first (cooperation), they can choose not to confess and remain silent to the question they are asked, or the second option (defect) they can blame it on their opponent. Each interrogator does not know what decision his opponent will make.

There are four possibilities for the interrogation to end:

- The player co-opts as his opponent does. Then both will get a 2-year prison sentence,

- The player cooperates, but his opponent betrays. The player is sentenced to 10 years in prison, and the opponent goes free immediately,

- the player betrays and his opponent cooperates. Then the player immediately goes free, and his opponent is sentenced to 10 years in prison,

- both cheat. As a result, both are sentenced to 5 years in prison.

![Image 1](img1.png)

This is a single prisoner's dilemma problem. In its iterated variant, players play several such dilemmas, and their final score is the sum of years earned for all rounds played. The more years of imprisonment obtained the worse.
## One-step memory

For IPD with one step memory, each strategy can be specified by the response (C or D) a player will take according to the last round played. Furthermore, the game requires the specification of the initial move  of  the  players.  In  each  round  of  game  between  two  players,  there  are  four  possible  outcomes  
((“my  move”      “opponent’s  move”)=DD,  DC,  CD,CC)  with  the  immediate  payoffs  P,  T,  S  and  R, respectively. In the context of one step memory, a player can recall his opponent's and his own strategy in  the  past  one  round.  They  can  have  responses  in  terms  of  strategy  ࣭Sp, St, Ss and Sr  for  the  DD, DC,  CD  and  CC  in  the  previous  step  respectively.  Together  with  the  initial  move S0,  we  can  encode  the strategy of IPD with one step memory by the following notation: S0|SpStSsSr. For example, GT is C|DDDC  and  Pavlov  is  C|CDDC.  Since  a  strategy  is  denoted  by S0|SpStSsSr which  have  five  bits and each slot encoded by either C or D, therefore, there are a total of 32 possible strategies in the strategy space Ms IPD with one step memory. 
## One-step memory results

After performing the calculations, the program presents the result as a heatmap. Where each row of the heatmap represents a player's tactic (for example, the first row is AllC: CCCCC), and each column represents an opponent's tactic. Each cell crosses two tactics with each other and the color it contains represents the player's total score from the 10 rounds taken between the two strategies. The darker the color, the worse it is for the player, because it tells you that he got more years of jail time in that particular skirmish.

![Image 2](mainResault.png)

The program also Saves the result as a matrix to a file named "mainData.txt". I further analyzed the data using Excel.

- How are kind strategies (those that start with C) doing?

Polite strategies collectively earned 21927 years of jail time, averaging 1370 years per strategy. Polite tactics collectively earned 20638 years, which averages them 1289 years per single tactic.

Polite strategies perform worse than malicious strategies. The reason for this may be that when such a polite tactic is measured against a malicious one, the polite strategy gets 10 years in prison to boot.

![Image 3](question1.png)

- How do strategies that respond to an opponent's betrayal in the past fare? And how do those that respond to betrayal with cooperation?

Strategies that respond to an opponent's betrayal with treachery do much better than those that respond to betrayal with cooperation. This is because some strategies take advantage of the naivety of tactics that respond with cooperation by always betraying them.

![Image 4](question2.png)

In the chart, I have presented how the development of each strategy looks like.

![Image 5](IPD.svg)

## Random One-step memory

To add randomness, I decided to give tactics a choice. As for the 4 possible situations (dd, dc, cd, cc) the strategy has 4 possible answers (P, T, S, R), so now I added 4 more possible answers. So now For 4 possible events, the strategy has 8 possible responses (for DD response P1 and P2, for DC response T1 and T2, for CD response S1 and S2, for CC response R1 and R2). This change increases the number of possible tactics from 32 to as many as 512 possibilities. Which answer a player chooses (for example P1 or P2) will depend on the "chance" parameter. The player first draws a real number x from the range 0 < x < 1. If the number drawn is less than the "chance" parameter, the player will choose an answer with index 1, and if the number x is greater than the "chance" parameter, the player will choose an answer with index 2.

## Random One-step memory results

![Image 6](generationfrom0to100.gif)

