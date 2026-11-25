# Mapping player styles at Worlds 2024

Do players still look alike after accounting for their jobs on a team? I analyzed tournament-wide statistics for **81 players on 16 teams** at the 2024 League of Legends World Championship. I used topological data analysis to study similarities that would be hard to see in a leaderboard sorted by one metric.

[Python notebook with executed outputs](Worlds_2024_Analysis.ipynb) · [One-page project brief](Worlds_2024_Topological_Analysis.pdf)

![Mapper graph of player performance profiles, showing one large connected component and two smaller ones](Worlds_2024_Mapper.png)

## From player statistics to team profiles

I standardized KDA, gold per minute, damage per minute, creep score per minute, kill participation and vision score per minute **within each position**. A support player's resource use was therefore compared with other supports. To represent a team, I selected its most-played player in each of the five positions and concatenated the six measures in a fixed role order. This produced a 30-dimensional vector per team.

## What the topology showed

I used a one-dimensional PCA projection as the lens for Mapper and clustered similar players within overlapping intervals. Two nodes are linked when they share a player. In the selected configuration, **33 of 36 nodes** were in one connected component. The graph had 70 edges across three components. For those settings, most groups of player profiles could be connected through intermediate groups.

I also computed Vietoris–Rips persistent homology on the original distance spaces. This tracks how components and loops appear and disappear as the distance threshold changes. The player cloud had 43 features in first homology (H1) and the team cloud had two. These are features of point clouds of different sizes and dimensions, so their counts alone do not rank the complexity of players and teams.

## Did those features add information?

I encoded persistence diagrams using persistence images and Betti curves, then compared team models using the original roster statistics, topological features, and both together. In a leave-one-team-out comparison, the hybrid logistic model assigned **14 of 16 teams** to the correct high- or low-mean-win-rate group. The topology-only model assigned 10 of 16 correctly.

The features summarize the full tournament, and some preprocessing used all 16 teams. These scores describe this tournament retrospectively. An out-of-sample forecasting test would need pre-match inputs, chronological splits and preprocessing fitted on training data alone.

## Running the notebook

You can read the saved figures and outputs directly on GitHub. To rerun the analysis, place an authorized copy of `player_statistics_cleaned_final.csv` beside the notebook and run the cells in order. The notebook documents the input schema and package requirements. The CSV is not bundled. Figures and interactive Mapper graphs are written to `figures/` and `outputs/`.

Individual project by [Patricio Flores Uribe](https://github.com/PatoFloresU).
