# Hot Hand: Phenomenon or Fallacy?
In week 6 of the University of Michigan's Foundations of Sports Analytics: Data, Representation, and Models in Sports we have introduced the concept of “hot hand” in sports and learned to test the existence of “hot hand” with both summary statistics and regression analysis using a 2016-2017 NBA shot log dataset. In this assignment, we performed similar analyses using shot log information in the 2014-2015 NBA season. The shot log dataset that I explored contains information on the outcome of each individual shot attempted by each player.

## I. Data Preparation and Exploration
Import the “Shotlog_14_15.csv” data file as “Shotlog_1415” into Jupyter Notebook. Import “Player_Stats_1415.csv” data file as “Player_Stats” into Jupyter Notebook.

1. Descriptions of the datasets and selected variables
a)    In the dataset “Shotlog_14_15,” each observation represents an attempt of a shot. In the dataset “Player_Stats_14_15,” each observation represents a player.
b)   The “average_hit” variable in both dataframes indicate the average success rate of a player making a shot over the season. It is defined and calculated the same way in both dataframes.
c)    The variable “home_away” indicates whether the team that the player belongs to played at home or away.
d)    The variable “result” indicates whether the team that the player belongs to won or lost the game. The variable “final_margin” represents the difference in final score between the team the player belongs to and their opponent’s.
e)    The variable “shot_number” is the order of the shot the given player attempted at the given game.
f)    “game_clock” is the countdown clock for each quarter. The game clock starts at 12 minutes. “shot_clock” refers to the display of a countdown clock of the time within which the team possessing the ball must attempt a field goal. The shot clock starts at 24 seconds.

2. Convert the “date” variable to a date type variable and calculate summary statistics for the “shot_clock” variable.

3. Create a lagged variable “lag_shot_hit” to indicate the result of the previous shot by the same player at the same game.
Hint: In this dataset, the variable “match” may not be able to uniquely identify each game; you can use “game_id” instead. You can sort the data by shot number for each player to create the lagged variable. 

4. Create a variable “error” to indicate the prediction error for each shot and a variable “lagerror” for the prediction error for the previous shot. The “error” variable is defined as the difference between the outcome of the current shot and the average success rate (“average_hit”) and the “lagerror” variable is defined as the difference between the outcome of the previous shot and the average success rate.

5. Calculate summary statistics for the “error” and “lagerror” variables. 

## II. Conditional Probability and Autocorrelation
1. Create a dummy variable “conse_shot” that indicates a player made consecutive shots. 

2. Create a dataframe “Player_Prob” for the probability of making the previous shot and the joint probability for making both the previous and current shots. Name the probability of making the previous shot “average_lag_hit” and the probability of making both shots “conse_shot_hit.” 

3. In the “Player_Prob” dataframe, calculate the conditional probability “conditional_prob” for a player to make a shot given that he made the previous shot. 

4. Merge the “Player_Prob” dataframe into the “Player_Stats” dataframe.

5. Calculate summary statistics for the probability for a player to make a shot (“average_hit”) and the conditional probability for a player to make a shot given that he made the previous one (“conditional_prob”) and the probability of players making consecutive shots (“conse_shot_hit”).

6. Perform a t-test for the statistical significance on the difference between conditional probability and unconditional probability of making a shot.

7.Calculate the first order autocorrelation coefficient on making a shot (correlation coefficient between making the current shot and the previous shot) for the entire shotlog dataset.

8. Calculate the first order autocorrelation coefficient on making a shot for each player. Display the top ten players with the highest first order autocorrelation coefficient.

## III. Regression Analysis  
In this section, you will run several regressions to investigate the “hot hand.” In all the regressions, the dependent variable is “error” and the independent variable of interest is “lagerror.” 

1. Reg1: Run a linear least squares regression using the entire shotlog dataframe. Include the following control variables:
- Shot distance
- Number of dribbles
- Touch time
- Type of shot (“points” variable)
- Quarter of the game (as a categorical variable)
- Home or away game
- Shoot_player
- Closest defender
- Closest defender distance

2. Reg2: Run a weighted least squares regression using the entire shotlog dataframe. Include the same set of control variables as in Reg1. The regression should be weighted by the number of shot per game (weight=1/shot_per_game).

3. Reg3_player: Run linear least squares regressions on individual players. Include the following control variables:
- Shot distance
- Number of dribbles
- Touch time
- Type of shot (“points” variable)
- Quarter of the game (as a categorical variable)
- Home or away game
- Closest defender distance

4. Reg4_wls_player: Run weighted least squares regressions on individual players. Include the same set of control variables as in Reg3. The regression should be weighted by the number of shot per game (weight=1/shot_per_game).
