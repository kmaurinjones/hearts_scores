# Project Overview
This repository contains a dataset of scores of the four of us playing the card game "Hearts", which I have turned into a machine learning project, predicting which player would win a game given recorded score data.

Details about the ruleset we used to play the game can be found here (this is helpful to understand the dataset and reasoning for adding certain features from the raw data):
https://www.familyeducation.com/entertainment-activities/games/indoor/how-play-hearts

## Data Collection
The raw data (located in the `hearts_scores - scores_anon.csv` file) was tracked by hand by the game players as games were played. All that was tracked was the score of each player (4 players, total) at the end of each hand of each game. When digitizing the data, games were each assigned a `game_id` integer (1:14), as to ensure that data in each game could be uniquely identified. As this dataset is not extensive of every game my family has ever played, the games included in this dataset are not ordered chronologically, nor was there any way to log this retroactively at the time of digitization, so the game_id value of each game is simply a relative and unique identifier.

## Columns of the Raw Dataset
- `game_id`: integer assigned to each game as to be able to uniquely identify each row of the dataset.
- `hand_id`: integer indicating the hand of the game during which row data took place.
- `player`: player to whom the row data corresponds. *After digitizing all scores, I replaced each player's real name with 'player x' as to maintain anonymity of my family members, but the respective changes are consistent throughout the entire dataset, and I have a separate copy of the original dataset against which I have made sure the name changes don't make a practical difference.*
- `received_cards_from`: the player from whom `player` received three cards after dealing each hand (see above hyperlink to game rules if not already familiar with this).
- `total_score`: score of `player` at the end of the indicated `hand_id` of the same row.

## Features I Have Created (Pre-ML)
- `points_per_hand`: number of points `player` got that hand.
- `percent_points_per_hand`: percentage of total score (of that game) each `player` got that hand.
- `queen_spades`: boolean (0 = no, 1 = yes) indicating whether `player` got the queen of spades that hand (see rules if this significance is unclear).
- `moon_shooter`: name of `player` who shot the moon that hand, if applicable, otherwise "none" (this is a rare and significant occurrence and is not guaranteed during play).
- `best_player_of_hand`: `player` who got the least points in that hand/did the "best" that hand.
- `best_player_of_game`: `player` who was `best_player_of_hand` the most frequently in each game (this is not necessarily the same as the `game_winner` player -- see below).
- `game_winner`: player who won the game. See rules for how to decide on who is selected as winner. As the objective of the game is generally to avoid points, once a given player had reached ≥100 points, the game is over, at which point the player with the least points is selected as the winner of that game.