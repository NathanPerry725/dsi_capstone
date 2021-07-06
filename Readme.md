
## Executive Summary

My goal with this project was to use modeling to attempt to get an edge in DraftKings daily fantasy baseball. Initially I had hoped to use player stats along with the stats of the opposing pitcher or batting lineup, to make regression models to predict the number of points batters and pitchers would score each game. Points are the scoring method used by draftkings which assign point values to different events in each game. The scoring system is described here: https://www.draftkings.com/help/rules/mlb?wpsrc=Organic%20Search&wpaffn=Google&wpkw=https%3A%2F%2Fwww.draftkings.com%2Fhelp%2Frules%2Fmlb&wpcn=help&wpscn=rules%2Fmlb.

I had expected to have difficulty in predicting batters due to the high variance that a batter can have game to game. It is not out of the ordinary for the best batter in the league to have zero hits in a game scoring 0 fantasy points. This concern was confirmed by my EDA where I saw very little correlation of DraftKings points with any features I had collected. I attempted to make a few models but none of them effectively predicted the test dataset. At this point I pivoted to using a time series model to predict batters. I did this because I wanted a model to predict close to a players mean score if there were no trends it could find in the data. I was interested in finding time based trends after reading this article on 538: https://fivethirtyeight.com/features/baseballs-hot-hand-is-real/
 
Normally hot hand are seen as a logical fallacy, but this article finds that pitchers have been shown to have hot and cold streaks. They also provide evidence that hot hands can exist among other players. I hope to create a model that predicts close to each player's mean while giving some weight to if they are on a hot or cold streak. Time series does not work well with pitchers in my model currently because starting pitchers play very few games in a season so the sample size is too small. The metric I am using to guage my time series is aic. It is not a very interpretable metric, but I am selecting the arima model with the lowest aic.

I was attempting to write a regression model to predict pitcher performance. Pitchers tend to be more consistent so I hoped it would work. My EDA showed some more correlation among pitching stats. I wrote a Linear Regression, Random Forest and Neural Network model to predict. Initially I was getting strong scores but I discovered that it was because of the specific random state I used to split, and upon using other random states my model was overfit. I am still going to try to optimize this model but for the time being I am just using the mean score for each pitcher. My current neural network is at: https://colab.research.google.com/drive/1D06qTKDn7v8ko2yxvzFpABbMx7TWUKrS#scrollTo=G1j2-ellRKY4

The next step I had was taking my predictions and creating my top lineups for submission. I used a genetic algorithm in order to do this. This involves creating random lineups and then resampling from the top lineups to keep making more, This allowed for me to make my top 150 lineups in a reasonable amount of time.

One of my limitations was the small amount of data I had. I only had stats from this season which definitely hurt my findings for pitcher data. There is also the natural difficulty of predicting baseball. Games are such a small sample size that they are very difficult to predict. 


## Variables of interest

I initially looked at a variety of stats to model the players. For batters I used multiple stats including on base percentage slugging percentage and batting average. I also used the opposing pitchers stats. Once I switched over to time series I was only looking at DraftKings points. While modeling pitchers I was only looking at the stats of the pitcher.

## Deliverable Format & Submission



## Suggested Ways to Get Started

- Review your initial proposal topic and feedback, and revise accordingly. 
- Spend time with your data and verify that it can help you accomplish the goals you set out to pursue. 
- If not, document how you intend to either change those goals. 
- Alternatively, go find some additional data and/or try another source.

---

## Useful Resources

- [Exploratory Data Analysis](http://insightdatascience.com/blog/eda-and-graphics-eli-bressert.html)
- [Best practices for data documentation](https://www.dataone.org/all-best-practices)

---

## Project Feedback + Evaluation

[Attached here is a complete rubric for this project.](./capstone-part-02-rubric.md)

Your instructors will score each of your technical requirements using the scale below:

Score  | Expectations
--- | ---
**0** | _Incomplete._
**1** | _Does not meet expectations._
**2** | _Meets expectations, good job!_

## PROGRESS REPORT
**Student Check-in:**

|WHAT’S GOING WELL/STRUGGLES|DEVELOPMENT PLAN|INSTRUCTOR FEEDBACK|
|---------------------------|----------------|-------------------|
|                           |                |                   |
