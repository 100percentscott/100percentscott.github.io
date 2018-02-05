---
layout: post
title:  losing roulette
date:   2018-02-05 10:30:00
---

*Code for simulations can be found [here]()*

I have been intrigued by the idea of running a [martingale](https://en.wikipedia.org/wiki/Martingale_(probability_theory)) strategy in roulette.  The strategy is a guaranteed win in a game without a bet size limit.  But most games have a bet size limit (at least in roulette).  Despite knowing that the strategy is loser in practice, I have tried it at least twice.  On each occasion I found myself at some point happier to take the loss than stake a further bet.  So I though I would run a little simulation of the strategy to demonstrate why it is a loser.

![](https://media0.giphy.com/media/l2SpO2558KNLdARcQ/giphy.gif)


A european roulette wheel has 37 numbers. 18 black, 18 red, and one zero. We will be betting on black. The martingale strategy is as follows:
1. place an initial bet on black.
2. If you win, stop.
3. If you lose, double the previous bet size and bet on black again.
4. Repeat step 3 unitl you win, and stop.

Roulette returns 2x your bet when you bet on a colour.  So this strategy returns your initial bet plus a profit the size of your intial bet. <br>

I ran 10,000 simulated games to get a sense of what the distribution outcomes look like.
From the frequency table for the simulation you can see:
- you win every game. The expected value is +£10.
- you win 48% of games on the fist bet (~= 18/37)
- to win the game with the most turns (14), you would first lose £163,840, and then bet a final £81,920 to win back the losses and make a profit of £10
- this highlights the biggest drawback to the strategy -- you need to be willing (and able) to lose a large amount of money, and to continue losing until an eventual win

![](https://i.imgur.com/upLq737.png){:height="40%" width="40%"}

# **With Table Limits**

The martingale strategy fails for one of three reasons:
1. you run out of money to make the next bet and so cannot recover your losses
2. you are unwilling to make the needed bet (it gets too large for your comfort zone)
3. you reach the bet size limit and so cannot recover your losses (most tables have a limit)

These are all in some way the same failing -- you need to take a loss. So, let's assume that you have infinite money at hand, and are fully committed to the strategy, so 1 and 2 don't matter.  What happens to the outcomes and expected profit if you play on a table with a limit.

Like before, I ran 10,000 simulated games with a bet size limit of £1000. From the frequency table for the simulation you can see:
- you no longer win every game. You lose 0.88% of hands, losing £1,270 each time
- The expected value is -£1.26. Ie. you now expect to lose each game on average

![](https://i.imgur.com/mMqzCA4.png){:height="40%" width="40%"}

Now, let's say that you played those 1,000 games back to back -- after all, to put the strategy into practise and win more than just £10, you would need to play one game after another. We can visualise what your profit path over those games looks like.<br>
![png](https://i.imgur.com/6aATxi5.png)

The chart above is just one simlulation. We can run several of these simulations to get a sense of the distribution of paths. Below I have run 100 simulations of playing the martingale stratefy 1,000 times in a row. What is clear from the chart is that this strategy is a loser!<br>
![png](https://i.imgur.com/XBeWCOi.png)

If you are more risk averse, and set a lower bet size limit, the strategy is even worse. Below is the same simulation with a £100 bet size limit.<br>
![png](https://i.imgur.com/rhatdh1.png)
