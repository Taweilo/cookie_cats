# Cookie Cats

[Cookie Cats](https://www.facebook.com/cookiecatsgame) is a hugely popular mobile puzzle game developed by [Tactile Entertainment](http://tactile.dk). It's a classic "connect three"-style puzzle game where the player must connect tiles of the same color to clear the board and win the level. It also features singing cats. We're not kidding! Check out this short demo [here](https://youtu.be/GaP5f0jVTWE).

[![Cookie Cats Video](https://github.com/Taweilo/cookie_cats/blob/main/Image/cookie_cats_video.jpeg)](https://youtu.be/GaP5f0jVTWE)

As players progress through the levels of the game, they will occasionally encounter gates that force them to wait a non-trivial amount of time or make an in-app purchase to progress. In addition to driving in-app purchases, these gates serve the important purpose of giving players an enforced break from playing the game, hopefully resulting in the player's enjoyment of the game being increased and prolonged.

![CC Gates](https://github.com/Taweilo/cookie_cats/blob/main/Image/cc_gates.png)

But where should the gates be placed? Initially, the first gate was placed at level 30, but in this repository, we're going to analyze an A/B test where we moved the first gate in Cookie Cats from level 30 to level 40. In particular, we will look at the impact on player retention. But before we get to that, a key step before undertaking any analysis is understanding the data. So let's load it in and take a look!



### Repository structure

```
├── Image
├── Code_cookie_cats_ab_testing.ipynb                 <- code
├── README.md                                         <- readme
├── cookie_cats.csv                                   <- dataset
```

## 1. Business Understanding
The problem for the Red Wine industry is to import wine based on limited information. Applying the machine learning technique, we can a model for wine quality prediction, according to its chemical content. The merit of the machine learning method is cost-effective and simple (not much domain knowledge is required). Below is the number we make up for the profits evaluation:


## 2. Data Understanding

The dataset is from Kaggle: https://www.kaggle.com/code/mursideyarkin/mobile-games-ab-testing-with-cookie-cats (cookie_cats.csv). 

The dataset consists of data from 90,189 players who installed the game during the AB-test period. The variables included are:

- `userid`: A unique identifier for each player.
- `version`: Indicates whether the player was in the control group (`gate_30` - a gate at level 30) or the group with the moved gate (`gate_40` - a gate at level 40).
- `sum_gamerounds`: The number of game rounds played by each player during the first 14 days after installation.
- `retention_1`: Indicates if the player returned to play after 1 day of installing the game.
- `retention_7`: Indicates if the player returned to play after 7 days of installing the game.

Players were randomly assigned to either the `gate_30` or `gate_40` group upon installing the game. As a sanity check, we'll verify if there are approximately equal numbers of players in each AB group.

## 3. EDA
It looks like there is roughly the same number of players in each group. 

  | Version | Percentage |
  |---------|------------|
  | gate_40 | 50.44%     |
  | gate_30 | 49.56%     |

- The distribution of game rounds
  
![The distribution of game rounds](https://github.com/Taweilo/cookie_cats/blob/main/Image/The%20distribution%20of%20game%20rounds.png)

In the plot above we can see that some players install the game but then never play it (0 game rounds), some players just play a couple of game rounds in their first week, and some get hooked!

## 4. Testing
- 1-day retention by AB-group
  
  1. 1-day retention rate for each group
     
        | Version | 1-day retention rate    |
        |---------|----------|
        | gate_30 | 0.448 |
        | gate_40 | 0.442 |
  
  2. Bootstrapping to consider the uncertainty
  
  ![Bootstrapped Means Distribution for Each AB-group](https://github.com/Taweilo/cookie_cats/blob/main/Image/Bootstrapped%20Means%20Distribution%20for%20Each%20AB-group%20-1.png) 

  3. Compare the difference between the two groups
     
  ![diff](https://github.com/Taweilo/cookie_cats/blob/main/Image/%25%20Difference%20Between%20the%20Two%20AB-groups%20-%201.png)     
  
  4. Consider the probability: 0.966 of the chance that gate-30 has a higher 1-day-retention rate
     
- 7-day retention by AB-group
  
  1. 7-day retention rate for each group
     
        | Version | 7-day retention rate    |
        |---------|----------|
        | gate_30 | 0.190 |
        | gate_40 | 0.182 |
  
  2. Bootstrapping to consider the uncertainty
     
  ![Bootstrapped Means Distribution for Each AB-group](https://github.com/Taweilo/cookie_cats/blob/main/Image/Bootstrapped%20Means%20Distribution%20for%20Each%20AB-group%20-%207.png) 
     
  3. Compare the difference between the two groups
     
  ![diff](https://github.com/Taweilo/cookie_cats/blob/main/Image/%25%20Difference%20Between%20the%20Two%20AB-groups%20-%207.png)     
  
  4. Consider the probability: 0.998 of the chance that gate-30 has a higher 7-day-retention rate
     
## 5. Conclusion
The bootstrap result tells us that there is strong evidence that 7-day retention is higher when the gate is at level 30 than when it is at level 40. The conclusion is: If we want to keep retention high — both 1-day and 7-day retention — we should not move the gate from level 30 to level 40. There are, of course, other metrics we could look at, like the number of game rounds played or how many in-game purchases are made by the two AB-groups. But retention is one of the most important metrics. If we don't retain our player base, it doesn't matter how much money they spend in-game.

## 6. Recommendation
So, why is retention higher when the gate is positioned earlier? One could expect the opposite: The later the obstacle, the longer people are going to engage with the game. But this is not what the data tells us. The theory of hedonic adaptation can give one explanation for this. In short, hedonic adaptation is the tendency for people to get less and less enjoyment out of a fun activity over time if that activity is undertaken continuously. By forcing players to take a break when they reach a gate, their enjoyment of the game is prolonged. But when the gate is moved to level 40, fewer players make it far enough, and they are more likely to quit the game because they simply got bored of it.

 

