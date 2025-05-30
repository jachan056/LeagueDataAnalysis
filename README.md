# League Of Legends Role Carry Potential Analysis

(LOL) Role Carry Potential Analysis is a data science project that includes various forms of data analysis including exploratory data analysis, Bivariate Analysis, hypothesis testing, and much more. The goal of this project is to determine which role has more carry potential between mid-laners and bot-laners, also known as ADC, and then determine how that ultimately affects the outcome of matches.

Author: Ja-Chan Lu

# Introduction

## General Description:
The dataset this project explores is given by Oracle's Elixir which provides significant data on each match that took place in 2024. The dataset provides much insight on each match ranging from outcomes, to key statistics of individual players which help quantify the performance of each player and the team as a whole.

The term "carry potential" of a role is defined by the impact of that role's performance inthe match which ultimately leads the team to victory. High carry potential means the role significantly impacted the outcome of the match, whereas low carry potential means the role's contribution to the outcome is not as significant.

The question I really want answered is which role out of the 5 roles given to teams in LOL have the most significant impact on the outcome of matches for their team. I will use various data analysis techniques to quantify their impact: Stats such as minion kills, damage done to other champions, number of kills, combat score (cs), etc. After answering which role has the most carry potential, I will use that data to build a prediction model to predict the outcome of numerous matches throughout the year, especially during big tournaments like Worlds (WLDs).

## Introduction to the Columns:
