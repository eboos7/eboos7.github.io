---
title: Life Through A Probabilistic Lens
date: 2023-05-21 08:35:01 +/-TTTT
tags: math     # TAG names should always be lowercase
math: true

---

Most people sit in math class and spout complaints of the sort - Why am I learning this? I am never going to use it in real life.

This article is my rebuttal to that type of thinking.

## Random Walk

Flipping a coin has two potential outcomes. Heads or tails. 

Flipping one coin, recording the result, and then flipping another has four potential outcomes. Heads then Tails; Heads then Heads; Tails then Heads; Tails then Tails.

If we flip two coins in a row in real life, our result will follow one of these branches, called [sample paths](https://math.stackexchange.com/questions/1472068/what-is-a-sample-path-of-a-stochastic-process). Notice that the probability of following any of the four sample paths is ~ $\frac{1}{4}$.

![Coin Flip](/assets/img/probabalistic-lens/coinflip.png){: width="700" height="400" }
_Coin Flip Probability Tree_

Our outcome is the result of [random walk](https://en.wikipedia.org/wiki/Random_walk) - a series of sequential, independent events. 

Consider rolling a dice twice. What is the probability that we roll a number from 1-4 both times? ~ $\frac{4}{6}$

For our picture, let's say the event of rolling 1-4 is O and the event of rolling 5-6 is S.

![Dice Roll](/assets/img/probabalistic-lens/diceroll.png){: width="700" height="400" }
_Dice Roll Probability Tree_

Just like our coin example, our outcome will be the result of independent sequential events, but NOT all outcomes are equal in probability. There is a higher probability that we will roll a number from 1-4 twice than from 5-6. $\frac{4}{9}$ vs $\frac{1}{9}$

To generalize this further, what if we want to consider a more complex scenario? We need more complex tools than simple random walk.

## Monte Carlo Simulations

Monte Carlo (MC) simulations are commonly used in the [investment world](https://www.investopedia.com/terms/m/montecarlosimulation.asp) to predict portfolio risk/outcomes. Employing MC methods gives insights into not only the expected outcome of our portfolio simulations, but also the ups and downs in-between the end result.

To delve into the technical workings of MC simulations you can read [here](https://math.stackexchange.com/questions/1472068/what-is-a-sample-path-of-a-stochastic-process) and [here](https://nicobesser.medium.com/brownian-motion-and-monte-carlo-simulation-of-daily-stock-price-eb86cd3c236f). Basically, MC simulations use a method called [brownian motion](https://en.wikipedia.org/wiki/Brownian_motion) to follow a random walk in a controlled scenario. So the big picture process is the same as our simple coin/dice examples just with numerical results.

![MonteCarlo](/assets/img/probabalistic-lens/montecarlo.png){: width="700" height="400" }
_Monte Carlo Simulation With 50 Steps_

At the heart of these simulations, is the acceptance that alternative histories (sample paths) could have been taken. Averaging all our sample paths will give us the [expected value](https://en.wikipedia.org/wiki/Expected_value) over a certain period of time. In the simulation above, the expectation would be roughly $100. So after 50 intervals of time pass, we expect the stock price to be $100, or close to it. Notice that expectation is not guaranteed, it is simply the most probable outcome.

Now let's apply the same MC tools to model real life outcomes with logic not numbers. 

## How "rich" are you based on the average of lives you could have led?

Here, the word rich is not restricted to monetary wealth. You can be rich in happiness, rich in family, rich in health, rich in etc.

Every day you wake up and enter a probabilistic decision tree (traversing one of your life's sample paths). Certain actions raise or lower your current ___ richness, similar to how stock prices fluctuate on a daily basis. 

The trick is being able to identify, or guesstimate, what actions have a high probability of affecting your ____ richness.

A Family Richness Monte Carlo visualization,

![FamilyMonteCarlo](/assets/img/probabalistic-lens/familymontecarlo.svg){: width="700" height="400" }
_Family Monte Carlo Simulation_

A Health Richness Monte Carlo visualization,

![HealthMonteCarlo](/assets/img/probabalistic-lens/familymontecarlo.svg){: width="700" height="400" }
_Health Monte Carlo Simulation_

Your real life expectation is open to manipulation for better or worse. 

How are you managing the odds?