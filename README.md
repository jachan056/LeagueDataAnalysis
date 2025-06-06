# League Of Legends Role Carry Potential Analysis

(LOL) Role Carry Potential Analysis is a data science project that includes various forms of data analysis including exploratory data analysis, Bivariate Analysis, hypothesis testing, and much more. The goal of this project is to determine which role has more carry potential between mid-laners and bot-laners, also known as ADC, and then determine how that ultimately affects the outcome of matches.

Author: Ja-Chan Lu

## Introduction

### General Description:
The dataset this project explores is given by Oracle's Elixir which provides significant data on each match that took place in 2024. The dataset provides much insight on each match ranging from outcomes, to key statistics of individual players which help quantify the performance of each player and the team as a whole.

The term "carry potential" of a role is defined by the impact of that role's performance inthe match which ultimately leads the team to victory. High carry potential means the role significantly impacted the outcome of the match, whereas low carry potential means the role's contribution to the outcome is not as significant.

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
