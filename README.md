# League Of Legends Role Carry Potential Analysis

(LOL) Role Carry Potential Analysis is a data science project that includes various forms of data analysis including exploratory data analysis, Bivariate Analysis, hypothesis testing, and much more. The goal of this project is to determine which role has more carry potential between mid-laners and bot-laners, also known as ADC, and then determine how that ultimately affects the outcome of matches.

Author: Ja-Chan Lu

## Introduction

### General Description:
The dataset this project explores is given by Oracle's Elixir which provides significant data on each match that took place in 2024. The dataset provides much insight on each match ranging from outcomes, to key statistics of individual players which help quantify the performance of each player and the team as a whole.

The term "carry potential" of a role is defined by the impact of that role's performance in the match which ultimately leads the team to victory. High carry potential means the role significantly impacted the outcome of the match, whereas low carry potential means the role's contribution to the outcome is not as significant.

The question I really want answered is which role out of the 5 roles given to teams in LOL have the most significant impact on the outcome of matches for their team. I will use various data analysis techniques to quantify their impact: Stats such as minion kills, damage done to other champions, number of kills, combat score (cs), etc. After answering which role has the most carry potential, I will use that data to build a prediction model to predict the outcome of numerous matches throughout the year, especially during big tournaments like Worlds (WLDs).

### Introduction to the Columns:
The dataset provides an extensive overview on game-related statistics on teams and players in their matches throughout the year. There are a total of 117,649 rows in the dataset and this is just a preview of some key columns included in the process of analysis.

- `gameid`: This column represents the specific matches played by players throughout the year. This allows for the separation of different matches played during 2024.

- `teamname`: This column represents the unique identifier for each team participating in any match in the 2024 season.

- `position`: This column represents the specific role played by each individual player in a match consisting of top-lane (top), mid-lane (mid), jungle (jng), support (sup), and bot-lane (ADC).

- `result`: This column represents the specific outcome of the match. 0 indicates that the player's team lost, while 1 indicates that the player's team won.

- `K/D Ratio`: This column represents the kill death ratio of a player. The higher the ratio means the player kills more enemy players before dying, which contributes heavily to a team's success as more kills means the player can be further strengthened and perform even better. 

- `assists`: This column represents the amount of times a player assisted/ contributed in the elimination of an enemy player without securing it themselves.

- `damageshare`: This column represents the proportion in which the player contributes to team damage (How much % of the team's damage did the specific player deal throughout the match).

- `damagetochampions`: This column represents the total damage a player inflicts to the enemy throughout the match, and high damage means significant contribution to team victory because high damage usually correlates with high elimination count.

- `total cs`: This column represents the count of how many minions a player has killed throughout the match. High CS means more experience and gold in which the gold can be spent on items to strengthen a player's ability to kill and increase experience points, which also strengthens a player.

- `earnedgold`: This column represents how much gold a player earned throughout the match and a higher count means the player is more likely able to purchase items in the shop that provide extra stats/abilities to increase their power and strength to kill enemies.

- `Champion`: This column represents which champion each player chose to play during the match.

## Data Cleaning and Exploratory Data Analysis
### Data Cleaning
The first step into the data cleaning process, only the relevant columns were kept which were the ones shown above. In the dataset, each match that took place is represented by 12 rows where 10 of them represent the players that played in the match and the last 2 rows being overall team statistics. During the cleaning process, only 4 rows were kept which were the 2 mid-laners and 2 bot-laners as those were the positions I was most interested in analyzing. 

Additionally, a new column was added, which was the K/D ratio column by dividing the amount of kills and amount of deaths of each player. The higher the ratio, the better performing the player is because the player is eliminating more players than dying, which contributes heavily to the team's success. Eliminating more means the player gains more expereince points and gold which can be used to strenghten the character to perform even better. When calculating K/D ratios, some players that had 0 deaths resulted in infinity as the calculated kill-death ratio, which is impossible. To combat this, during the calculation process, instead of 0 deaths are replaced with 1 deaths to prevent any non-realistic values. The resulting ratio is also the same as the amount of kills the player got in the match.

Head of cleaned dataframe:| gameid               | position | teamname     | result | kills | deaths | assists | damagetochampions | damageshare | total cs | earnedgold | K/D ratio |
|:---------------------|:---------|:-------------|-------:|------:|-------:|--------:|------------------:|------------:|---------:|-----------:|----------:|
| 10660-10660_game_1   | mid      | LNG Esports  |      0 |     0 |      2 |       0 |             10005 |     0.239355 |      270 |       6620 |         0 |
| 10660-10660_game_1   | bot      | LNG Esports  |      0 |     2 |      4 |       0 |             10892 |     0.260563 |      311 |       8101 |       0.4 |
| 10660-10660_game_1   | mid      | Rare Atom    |      1 |     4 |      0 |       7 |             14917 |     0.261963 |      329 |      10480 |         4 |
| 10660-10660_game_1   | bot      | Rare Atom    |      1 |     7 |      1 |       5 |             19516 |     0.342725 |      303 |      10898 |       3.5 |
| 10660-10660_game_2   | mid      | LNG Esports  |      0 |     1 |      4 |       2 |             11376 |     0.209038 |      219 |       5681 |       0.2 |

### Univariate Analysis:
Univariate Analysis was performed on the earned gold statistic by players. 

<iframe
  src="figures/gold-distribution.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
The graph shows a relatively normal distribution based on its shape. The shape of the graph indicates a large cluster towards the bin between 5000 and 10,000 gold range, and most players in the 2024 season usually earn around 8000-9000 gold in their matches based on the tallest rectangle sectioned in the graph. 

### Bivariate Analysis:
Bivariate Analysis was done on the columns damagetochampions and to earned gold.
<iframe
  src="figures/goldvsdamage.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The scatterplot is done to comapre the values of 2 columns (damagetochampions and earnedgold). Based on the graph shown, there is a strong positive lienar association, which means as damage to other champions increases, earned gold will increase as well.

### Intresting Aggregates:

| position   |   kills |   deaths |   assists |   damagetochampions |   damageshare |   total cs |   earnedgold |   K/D ratio |
|:-----------|--------:|---------:|----------:|--------------------:|--------------:|-----------:|-------------:|------------:|
| bot        | 3.8     |  2.8     |   5.4     |             17734.2 |      0.215082 |    246.6   |       8067   |     1.16    |
| mid        | 3.94358 |  2.70564 |   6.04136 |             21810.6 |      0.270174 |    277.613 |       9233.6 |     1.57217 |

For the aggregate, the dataframe is grouped by position, then the mean function is applied to get the mean of the columns: K/D ratio, assists, damagetochampions, total cs, and earned gold for the mid-laner position and bot-laner/ADC position. The results show that on average, mid-laners have a much higher K/D ratio, which means they are doing more killing, whihc in turn contributes to both indivdual and team success. Mid-laners on average, lead in K/D ratios, 
assists, damage to champions, total cs, and earned gold. Mid-laners ultimately seem to be 
contributing more than the ADC position.

## Assessment of Missingness

### NMAR Analysis:
A column that could be NMAR would be the pentakill column which represents when a single player eliminates the entire enemy team by themself. The data is missing not at random due to the fact that no player during that match was able to achieve such a feat. Additionally, you can not use other columns to infer the amount of pentakills as no statistic is able to directly predict whether a player eliminated the entire enemy team by themself, making the column NMAR.

### Missingness Dependency: 
The first test is done on the goldat25 and match duration columns to test whether goldat25's missingness depends on gamelength (match duration) column.

**Null Hypothesis**: The mean match duration is equal for matches with and without data for goldat25.

**Alternative Hypothesis**: The mean match duration is longer for matches with data for goldat25.

**Test Statistic**: The test statistic utilized will be difference in mean duration for matches with and without data for theri entries in the goldat25 column. 

The empirical distribution of the test statistic and observed statistic during the permutation testing resulted in such a plot:
<iframe
  src="figures/gold25vsduration.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The observed mean difference was calculated to be approximately 179.98. The p-value is derived to be 0 after conducting the permutation tests. Since the p-value was way less than 0.05, the original signifiance level, we can reject the null hypothesis. Thus, this indicates that the missingness in goldat25 column depends on the gamelength (match duration) column.

The second test is done on the goldat25 and result column to test whether goldat25's missingness depends on the result of a match (win/lose) (result) column.

**Null Hypothesis**: There is an equal distribution for amount of wins/losses for matches with and without data for goldat25.

**Alternative Hypothesis**: Values in goldat25 are more likely to be recorded for players who ended up winning the match (1 as their value in the result column). 

**Test Statistic**: The test statistic utilized will be difference in means of the result columns for rows with data in goldat25 and for rows with no data in goldat25. 

The empirical distribution of the test statistic and observed statistic during the permutation testing resulted in such a plot:
<iframe
  src="figures/gold25vsresult.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The observed mean difference was calculated to be approximately 0.00051. The p-value is derived to be 0.444 after conducting the permutation tests. Since the p-value was way more than 0.05, the original signifiance level, we fail to reject the null hypothesis. Thus, this indicates that the missingness in goldat25 column does not depend on the result column (whether the match was won or lost).

## Hypothesis Testing
In the hypothesis test, I want to determine if there is a significant difference between the probabilities of mid-laners having the highest damageshare in their match or bot-laners having the highest damageshare in their match. This is important in answering the overall research question because finding out which position has a the higher damageshare allows us to use the damageshares of that position and then predict whether a team wins or loses based on the performance of their mid-laner in the match.

**Null Hypothesis**: There is an equal probability for mid-laners/bot-laners achieving the highest damage share in their match.

**Alternative Hypothesis**: There is an unequal probability for mid-laners/bot-laners achieving the highest damage share in their match as in the bot-lane (ADC) has the more favorable probability over the other. 

**Test Statistic**: Absolute mean difference between mid-laners' damage shares and bot-laners' damage shares because the absolute mean difference best measures the difference in their damage shares to be able to display how much 1 contributes to team success over the other. 

**Significance Level**: 5% or 0.05 because of the standard/default level of significance always being 0.05. 

The level of significance chosen was 0.05, and the p-value ended up being 0.0008 which was way below the level of significance. This means that the null hypothesis can be rejected, therefore bot-laners have a higher probability of getting a higher damage share in a given match compared to mid-laners. This means that to predict which team wins a given match, the bot-laner position should be looked at, especially their damange share statistic.

## Framing a Prediction Problem:
Previously, it was determined that the bot-laners have the highest carry potential due to their tendency to be the highest damage share out of all the positions in the game. With this in mind, would it be possible to predict whether a team wins or loses a match based on the damage share proportion and other statistics of their bot-laner? This is going to be a classification problem, utilizing a binary classification where 1 means the team won, and 0 means the team lost. The response variable that is being predicted is the values in result where 1 = win match and 0 = lose match. The reason why the variable was chosen was because the model was meant to predict the result of the match, meaning the values in result does the job perfectly. It's very simple as well having only 2 disctinct values to represent a win or loss. The result column consistently records data because every possible match always has an end result. To measure the success of the model, the metric utilized would be accuracy because of the relatively even distribution of wins and losses. Had the result column had an imbalanced win percentage instead of an even 50/50 split of wins and losses, the f1-score model would have been superior for the lack of balance in the model. During the initial model, the variables utilized to build the model will include damage share and K/D ratio. These variables are spefically picked because they evaluate the performance of a player in a match well, and these statistics are also representative of a winning/losing player based on its magnitude. Additionally, no encoding is required on the columns as the data being utilized are all quantitative data.   

## Baseline Model:
In the baseline model, a binary classifier is utilized along with 2 features (damage share and K/D ratio of individual bot-laners). Both of these features are considered quantitative data. The StandardScaler Transformer was utilized in order to transform the features into standard scale, which allows for the data to be considered/utilized on the same scale. When fitting the model, it resulted in many numbers between 0 and 1, which was supposed to represent the win/loss result. To combat this, a 0.5 margin was drawn on the data, meaning that all predicted values above 0.5 counted as a win while values below 0.5 counted as a loss. After fitting the model, the accuracy score came out to be 0.7988, which meant the 79.88% of the data was correctly predicted by the model. In order to improve the accuracy on the model, some additional measures will be taken such as adding a train-test split, additional features, and much more. 

## Final Model


## Fairness Analysis
...
