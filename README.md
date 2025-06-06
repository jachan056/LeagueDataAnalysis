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
