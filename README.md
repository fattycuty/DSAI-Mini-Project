# SC1015-Mini-Project

## Introduction

"Counter-Strike: Global Offensive (CS:GO) is a popular first-person shooter game that has gained immense popularity worldwide. The game involves two teams, terrorists and counter-terrorists, competing against each other in a series of rounds to achieve **VICTORY**. As the game has evolved over time, so has the interest in analyzing and understanding the gameplay mechanics.

As players who wish to attain the highest rank in CS:GO (GLobal Elite), we want to use this as a way to develop better strategies and win more efficiently.

## Motivation

Our goal is to use data visualisation techniques and machine learning algorithms to analyze the gameplay patterns of different teams and players. By identifying the key factors that contribute to a team's success or failure, we hope to gain useful insights for players like us to develop better strategies so we can win more games!

Dataset is from: https://www.kaggle.com/datasets/skihikingkevin/csgo-matchmaking-damage
As the dataset files are huge, please download them and place it in /dataset/xxx.csv and /maps/xxx.png

## 1) Data cleaning

## 2) Exploratory Data Analysis
EDA can be a powerful tool for gaining insights into the CSGO data and using those insights to improve gameplay, balance the game mechanics, and optimize strategies.
By using the tool ipywidgets, we are able to make data visualisation user interactive and filtered to specific categories ( `Map` , `Weapon` , `Side` ) for better exploration of the CS:GO data. Interactive plots and charts allow users to filter the data by map, and/or weapon, and/or side, and explore the relationship between different variables in real-time.
  * Most used weapon
  * Likely side to win as time progresses
  * Better bomb site to plant the bomb
  * Heat map of kills

## 3) Model Building & Machine Learning

We noticed from our experience that there are multiple significant factors that can affect the outcome of a round, such as whether `bomb is planted` or `equipment value`. With these data we can build machine learning models that predicts the outcome of rounds, and with these valuable insights, make better decisions in our future games.
### Models used:
  * Random Forest
  * Logistic Regression
  * K-nearest Neighbour

## Conclusion

Overall, CS:GO is a complex game with many crucial variables affecting the outcome of a match that cannot be quantified, including player technical skill, team coordination, and game mechanics. While machine learning models can help to identify patterns and trends in this data, they may struggle to account for all other factors that can affect the outcome of a match.

While data science and machine learning can provide valuable insights into developing strategies in CS:GO, they should be used in conjunction with other methods of analysis and individual skills development in order to achieve our objective.
