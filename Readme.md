## Notebooks

1. Create pitchers and batters - This notebook was the first one made, with the purpose of creating dataframes of each players stats

2. Daily Data Merge Worksheets - These worksheets were created to create my model training data. They used the pitcher and batter dataframes I had created along with lineups of each player starting in games for the day and thier final DraftKings Score to form model training data. This ended up only being used for pitchers as I decided to use a time series for batters

3. EDA Report - This is the notebook I used to conduct EDA

4. Create Pitcher Train Data - This concatenated all of the pitcher dataframes I had created for each day and saved them in formats I could use for my Neural Network

5. Pitcher Prediction Prep - This notebook prepares the current days starting pitchers to be input into my neural network

6. Neural Network - This notebook is in the cloud because my computer is unable to run tensorflow. I pull in the pitcher training data to train the model and then pull in my final pitcher csv to make predictions. I output these predictions as a csv to be put into my lineup generator. Link: https://colab.research.google.com/drive/1D06qTKDn7v8ko2yxvzFpABbMx7TWUKrS?usp=sharing

7. Make Lineups - This notebook creates a time series model for each batter and saves the predictions for each players next game. It then imports the pitcher predictions from the neural network and creates a dataframe of the predictions for the players that are listed as starters for the days games. It then uses a genetic algroithm to create 150 lineups and save them to the output folder.


## Lineup generation process

First I download the days starting lineups from baseball monster, and the salary data from draftkings. I then put the data through the pitcher prediction prep notebook, followed by running my neural network to get the pitcher predictions. Then I run the make lineups notebook before submitting the lineups for submission file to draftkings.

## Executive Summary

My goal with this project was to use modeling to attempt to get an edge in DraftKings daily fantasy baseball. Initially I had hoped to use player stats along with the stats of the opposing pitcher or batting lineup, to make regression models to predict the number of points batters and pitchers would score each game. Points are the scoring method used by draftkings which assign point values to different events in each game. The scoring system is described here: https://www.draftkings.com/help/rules/mlb?wpsrc=Organic%20Search&wpaffn=Google&wpkw=https%3A%2F%2Fwww.draftkings.com%2Fhelp%2Frules%2Fmlb&wpcn=help&wpscn=rules%2Fmlb.

I had expected to have difficulty in predicting batters due to the high variance that a batter can have game to game. It is not out of the ordinary for the best batter in the league to have zero hits in a game scoring 0 fantasy points. This concern was confirmed by my EDA where I saw very little correlation of DraftKings points with any features I had collected. I attempted to make a few models but none of them effectively predicted the test dataset. At this point I pivoted to using a time series model to predict batters. I did this because I wanted a model to predict close to a players mean score if there were no trends it could find in the data. I was interested in finding time based trends after reading this article on 538: https://fivethirtyeight.com/features/baseballs-hot-hand-is-real/
 
Normally hot hand are seen as a logical fallacy, but this article finds that pitchers have been shown to have hot and cold streaks. They also provide evidence that hot hands can exist among other players. I hope to create a model that predicts close to each player's mean while giving some weight to if they are on a hot or cold streak. Time series does not work well with pitchers in my model currently because starting pitchers play very few games in a season so the sample size is too small. The metric I am using to guage my time series is aic. It is not a very interpretable metric, but I am selecting the arima model with the lowest aic.

I wrote a regression model using a neural network to predict pitcher performance. Pitchers tend to be more consistent so I hoped it would work. My EDA showed some more correlation among pitching stats. The root mean squared error of my model is 11 vs the baseline of 12. My current neural network is at: https://colab.research.google.com/drive/1D06qTKDn7v8ko2yxvzFpABbMx7TWUKrS?usp=sharing


The next step I had was taking my predictions and creating my top lineups for submission. I used a genetic algorithm in order to do this. This involves creating random lineups and then resampling from the top lineups to keep making more, This allowed for me to make my top 150 lineups in a reasonable amount of time.

One of my limitations was the small amount of data I had. I only had stats from this season which definitely hurt my findings for pitcher data. There is also the natural difficulty of predicting baseball. Games are such a small sample size that they are very difficult to predict. 


## Variables of interest

I initially looked at a variety of stats to model the players. For batters I used multiple stats including on base percentage slugging percentage and batting average. I also used the opposing pitchers stats. Once I switched over to time series I was only looking at DraftKings points. While modeling pitchers I was only looking at the stats of the pitcher vs batters of each handedness.

## Conclusions

So far this process has allowed me to make a small profit. This was over a very short time span so it doesn't neccesarily suggest a consistently strong model. I know there are still problems likely preventing this from consistent success. I believe the solution to this is not in making stronger predictive models, but in improving my lineup generation.

## Next Steps

I am going to focus my efforts on improving my genetic algorithm. One thing I want to try is to have my algorithm limit the amount of lineups a single person can be in so I am not over reliant on one player. I also want to try making my algorithm avoid having lineups with opposing batters and hitters, as if a batter has a good game, the opposing pitcher probably doesn't. I will also look into other potentially useful lineup creation techniques.