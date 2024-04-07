# Cookie Cats

[Cookie Cats](https://www.facebook.com/cookiecatsgame) is a hugely popular mobile puzzle game developed by [Tactile Entertainment](http://tactile.dk). It's a classic "connect three"-style puzzle game where the player must connect tiles of the same color to clear the board and win the level. It also features singing cats. We're not kidding! Check out this short demo [here](https://youtu.be/GaP5f0jVTWE).

[![Cookie Cats Video](https://github.com/Taweilo/cookie_cats/blob/main/Image/cookie_cats_video.jpeg)](https://youtu.be/GaP5f0jVTWE)

As players progress through the levels of the game, they will occasionally encounter gates that force them to wait a non-trivial amount of time or make an in-app purchase to progress. In addition to driving in-app purchases, these gates serve the important purpose of giving players an enforced break from playing the game, hopefully resulting in the player's enjoyment of the game being increased and prolonged.

![CC Gates](https://github.com/Taweilo/cookie_cats/blob/main/Image/cc_gates.png)

But where should the gates be placed? Initially, the first gate was placed at level 30, but in this repository, we're going to analyze an A/B test where we moved the first gate in Cookie Cats from level 30 to level 40. In particular, we will look at the impact on player retention. But before we get to that, a key step before undertaking any analysis is understanding the data. So let's load it in and take a look!



### Repository structure

```
├── Image
├── LICENSE.txt                                    <- license
├── Red Wine Classification Project.ipynb          <- code
├── WineQT.csv                                     <- dataset
```

## 1. Business Understanding
The problem for the Red Wine industry is to import wine based on limited information. Applying the machine learning technique, we can a model for wine quality prediction, according to its chemical content. The merit of the machine learning method is cost-effective and simple (not much domain knowledge is required). Below is the number we make up for the profits evaluation:


## 2. Data Understanding

Dataset is from Kaggle: https://www.kaggle.com/code/mursideyarkin/mobile-games-ab-testing-with-cookie-cats (also please see WineQT.csv attached). 

The dataset consists of data from 90,189 players who installed the game during the AB-test period. The variables included are:

- `userid`: A unique identifier for each player.
- `version`: Indicates whether the player was in the control group (`gate_30` - a gate at level 30) or the group with the moved gate (`gate_40` - a gate at level 40).
- `sum_gamerounds`: The number of game rounds played by each player during the first 14 days after installation.
- `retention_1`: Indicates if the player returned to play after 1 day of installing the game.
- `retention_7`: Indicates if the player returned to play after 7 days of installing the game.

Players were randomly assigned to either the `gate_30` or `gate_40` group upon installing the game. As a sanity check, we'll verify if there are approximately equal numbers of players in each AB group.

## 3. EDA



## 4. Modeling
* SVC
* Logistic regression
* KNN
* Decision Tree
* Random Forest
* Random Forest with Tuning
* Adaboost

## 5. Evaluation
 <img src="https://github.com/Taweilo/Red_Wine_Quality_Classification_Model/blob/main/Image/5.1 Evaluation.jpg" width="500" >
From the summary table, we can observe that AUC is not necessary to associate with high profits.

## 6. Recommendation
* Business Value: <br>
From the below graph, we can easily compare the business value between the ml model (RF classifier) and the non-ml model: by considering the relationship between the true positive rate and expected profits on the two models. 
1. RF classifier performance is better than the non-ml model.
2. True positive rate has a positive relationship with expected profits because more good wine in the population yields more profits. Detail check with the information below the graph.
3. Under the extreme case where the true positive rate is 0, meaning no good wine in the population, the non-ml model suffers a loss but the ml model can still make a profit. It's because ml model can predict red wine quality and discriminate the price. However, the non-ml model only produces one and only offer which is $75. Buy high sell low incurs a loss. 
  <img src="https://github.com/Taweilo/Red_Wine_Quality_Classification_Model/blob/main/Image/6.1 Business%20value.jpg" width="600" >

 

