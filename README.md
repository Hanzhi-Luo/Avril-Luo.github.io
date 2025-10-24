# Avril-Luo.github.io
MLB Batting Analysis (Data Bootcamp Midterm Project)
Overview

This project explores how different batting statistics in Major League Baseball (MLB) relate to both player value and team performance.
I used the pybaseball API to pull MLB data from 2023 to 2025, cleaned it, averaged stats across seasons, and visualized how metrics like OPS and wOBA connect to overall success.

Since the official standings API wasn’t working, I made a simple “fake win percentage” based on each team’s normalized OPS.
It’s not a real win–loss record, but it works surprisingly well for showing which teams hit better on average.

Key Questions

Do players with higher OPS or wOBA also have higher WAR (Wins Above Replacement)?

Which team-level batting metrics are most tied to winning (or our fake version of it)?

Are these relationships consistent across seasons?

Data Source

All data came from the pybaseball library (FanGraphs + Baseball Reference).
Pulled using:

from pybaseball import batting_stats
bat = batting_stats(2023, 2025)


Each row in the dataset represents a player’s season stats.
I averaged them by player and by team to get multi-season trends.

Main features used:

OPS – On-base Plus Slugging

wOBA – Weighted On-base Average

SLG, HR, Barrel%, HardHit% – power/contact indicators

WAR – overall player value

Methods
1. Player-Level Analysis

Combined 2023–2025 data and averaged stats per player.

Plotted OPS vs WAR and wOBA vs WAR.

Calculated correlations and a heatmap between main hitting metrics.

2. Team-Level Analysis

Averaged player data by team.

Created a fake_win_pct = OPS / OPS.max() to simulate performance.

Visualized OPS and wOBA vs fake win%, plus a correlation heatmap.

3. Tools

pandas for cleaning and grouping

matplotlib + seaborn for charts

pybaseball for data retrieval

Results
Player-Level

OPS and wOBA showed strong positive relationships with WAR (correlations ≈ 0.8).

Metrics like Barrel% and HardHit% also mattered, but less strongly (~0.5–0.6).

Heatmap confirmed these three—OPS, wOBA, and SLG—cluster tightly with WAR.

Team-Level

When averaged by team, OPS and wOBA again had the strongest link to performance.

Both correlated with the fake win% around 0.8–0.85.

Teams with higher OPS generally had better “win” proxies.

Discussion

Even without real standings, the patterns make sense:
teams that hit for both power and on-base ability tend to do better overall.
OPS and wOBA are clearly the simplest and most reliable measures of offensive quality.

Limitations

Real standings weren’t available, so fake win% is just a normalized OPS ratio.

No pitching or defensive data included—those obviously affect wins too.

Correlation doesn’t prove causation, just association.

Next Steps

If the API starts returning real win–loss records again, I’d like to re-run the analysis and compare how close my fake metric comes to actual results.
Adding pitching data (ERA, FIP, etc.) could also make the model more realistic.

How to Run

Requirements

pybaseball >= 2.2.0  
pandas  
matplotlib  
seaborn


Steps

Open the notebook or Colab file.

Run the installation cell:

!pip install pybaseball pandas matplotlib seaborn


Execute cells top to bottom to load data, clean it, and generate charts.

Folder Structure
mlb_batting_analysis/
│
├── midterm_for_data_bootcamp.ipynb   # main notebook
├── midterm_for_data_bootcamp.py      # script version
├── data/
│   └── mlb_batting_2023_2025.csv
└── README.md

Example Insights

Aaron Judge and Bobby Witt Jr. were among the top hitters by WAR (2023–2025).

Team-level OPS correlated with the fake win% at 0.84.

Player-level OPS correlated with WAR at 0.79.

References

pybaseball GitHub

FanGraphs Baseball Glossary

Baseball Reference
