# SC1015-Mini-Project

## Introduction

"Counter-Strike: Global Offensive (CS:GO) is a popular first-person shooter game that has gained immense popularity worldwide. The game involves two teams, terrorists and counter-terrorists, competing against each other in a series of rounds to achieve **VICTORY**. After every round, players are rewarded money based on their performance to buy equipments such as weapons, armour etc. As the game has evolved over time, so has the interest in analyzing and understanding the gameplay mechanics.

![image](https://github.com/fattycuty/DSAI-Mini-Project/blob/main/sc1015_image/csgothumbnail.png "Source: https://store.steampowered.com/app/730/CounterStrike_Global_Offensive/")

As players who wish to attain the highest rank in CS:GO (Global Elite), we want to use this as a way to develop better strategies and win more efficiently.

## Motivation

Our goal is to use data visualisation techniques and machine learning algorithms to analyze the gameplay patterns of different teams and players. By identifying the key factors that contribute to a team's success or failure, we hope to gain useful insights for players like us to develop better strategies so we can win more games!

Dataset is from: https://www.kaggle.com/datasets/skihikingkevin/csgo-matchmaking-damage

As the dataset files are huge, please download them to run the notebook.

Place the files in these locations:

1. Project Folder

![image](https://i.imgur.com/QLsTmrn.png)

2. dataset folder

![image](https://i.imgur.com/37OcU4Y.png)

3. maps folder

![image](https://i.imgur.com/10FeZaK.png)

## 1) Data Cleaning
We intially use 3 datasets, esea_meta_demos.part1, esea_master_dmg_demos.part1 and esea_master_kills_demos.part1. Each shows per round results, every damage taken encounter and all kills respectively. We also used the map_data to get the x,y coordinates of each map so that we can map it later on.

We add some columns to the dataset such as round_duration for a better time indicator, loser_side, t_win and ct_win for easier data manipulation going forward. We also remove all matches that does not have a complete set of rounds. Lastly, we merged the columns to make one big dataframe called cleaned_df that contains all the previous 3 datasets. From there, we decompose it to show only per round results, called round_end_stats_df, which now contains more information per round than the initial esea_meta_demos.part1 dataset.

## 2) Exploratory Data Analysis
EDA can be a powerful tool for gaining insights into the CSGO data and using those insights to improve gameplay, balance the game mechanics, and optimize strategies.

By using the tool ipywidgets, we are able to make data visualisation user interactive and filtered to specific categories ( `Map` , `Weapon` , `Side` ) for better exploration of the CS:GO data. Interactive plots and charts allow users to filter the data by map, and/or weapon, and/or side, and explore the relationship between different variables in real-time.

```
from ipywidgets import interact, interactive, fixed, interact_manual

interact(plotheat, Map = maps, Team = sides, Weapon = weapons)
```

<br />


  * Most used weapon
  
  ![image](https://github.com/fattycuty/DSAI-Mini-Project/blob/main/sc1015_image/img4.png)
  * Likely side to win as time progresses

![image](https://github.com/fattycuty/DSAI-Mini-Project/blob/main/sc1015_image/img5.png)
  * Better bomb site to plant the bomb

![image](https://github.com/fattycuty/DSAI-Mini-Project/blob/main/sc1015_image/img3.png)
  * Heat map of kills

![image](https://github.com/fattycuty/DSAI-Mini-Project/blob/main/sc1015_image/img1.png)
  ![image](https://github.com/fattycuty/DSAI-Mini-Project/blob/main/sc1015_image/img2.png)

## 3) Model Building & Machine Learning

We noticed from our experience that there are multiple significant factors that can affect the outcome of a round, such as whether `bomb is planted` or `equipment value`. With these data we can build machine learning models that predicts the outcome of rounds, and with these valuable insights, make better decisions in our future games, such as whether to save or spend our money each round on better equipment.

As the we will be doing binary classification (Win or Lose) we decided to use the following as machine learning models

### Models used:
  * Random Forest

A random forest is a machine learning algorithm that uses an ensemble of decision trees to make predictions. It is trained using bagging, which involves randomly sampling the training data with replacement to create new datasets for each decision tree. The algorithm predicts the outcome by taking the average or mean of the output from the individual trees. Random forests reduce overfitting and increase precision compared to decision trees.

Cross-validation is used to determine an optimal `n_esimators` value

```
from ipywidgets import interact, interactive, fixed, interact_manual

interact(plotheat, Map = maps, Team = sides, Weapon = weapons)
```

|   Dataset :   |  Classification Accuracy | 
|---------------|--------------------------|
|     Train     |        0.7261375         |
|     Test      |        0.72475           |
  * Logistic Regression

Logistic regression is a machine learning algorithm that allows us to explore the relationship between two variables by using mathematical equations. It helps to predict the value of one variable based on the other, with a limited number of possible outcomes, such as "yes" or "no". This makes this algorithm suitable in this case where a `win` or `loss` is predicted.

|   Dataset :   |  Classification Accuracy | 
|---------------|--------------------------|
|     Train     |        0.7065125         |
|     Test      |        0.70825           |
  * K-nearest Neighbour

K-nearest neighbor (KNN) is a machine learning algorithm that compares the new observation with all the existing observations in the dataset to find the k-nearest neighbors. The value of k is a user-defined parameter that determines the number of nearest neighbors to be considered. Once the nearest neighbors are identified, the KNN algorithm classifies the new observation based on the majority class of the k-nearest neighbors.

Cross-validation is used to determine an optimal `n_neighbors` value

```
from sklearn.model_selection import cross_val_score
from sklearn.preprocessing import StandardScaler

k_values = [i for i in range (1,101)]
scores = []

scaler = StandardScaler()
eq_diff_ct = scaler.fit_transform(eq_diff_ct)

for k in k_values:
    knn = KNeighborsClassifier(n_neighbors=k)
    score = cross_val_score(knn, eq_diff_ct, side_win_ct.values.ravel(), cv=5)
    scores.append(np.mean(score))
    
sb.lineplot(x = k_values, y = scores, marker = 'o')
plt.xlabel("K Values")
plt.ylabel("Accuracy Score")
```

<br />

|   Dataset :   |  Classification Accuracy | 
|---------------|--------------------------|
|     Train     |        0.7136625         |
|     Test      |        0.71005           |

### Comparing models

As shown, there a correlation which would make sense as when equipment value difference is positive (Your team has better equipment than your enemies) you tend to beat them in firepower and win the round. Random Forest Classifier has the highest accuracy compared to the other 2 models.

## Final remarks

Overall, CS:GO is a complex game with many crucial variables affecting the outcome of a match that cannot be quantified, including player technical skill, team coordination, and game mechanics. While machine learning models can help to identify patterns and trends in this data, they may struggle to account for all other factors that can affect the outcome of a match.

While data science and machine learning can provide valuable insights into developing strategies in CS:GO, they should be used in conjunction with other methods of analysis and individual skills development in order to achieve our objective.

## Contributors
[Hazim](https://github.com/fattycuty) -  Data Scraping, Data Preparation, Exploratory Data Analysis, Feature Engineering<br>
[Jian Feng](https://github.com/Marcushjf) - Machine Learning, Core Analysis, Data-Driven Insights<br>
