# MLB Batting Analysis (Data Bootcamp Midterm Project)

## Overview
This project explores how different **batting statistics** in Major League Baseball (MLB) relate to both **player value** and **team performance**.  
The data is pulled using the `pybaseball` library from **2023 to 2025**, then cleaned, averaged, and visualized to understand how metrics like OPS and wOBA connect to overall success.

Since the official standings API wasn’t returning results, a simple “**fake win percentage**” was created using normalized OPS as a proxy for team success.


## Key Questions
1. Do players with higher **OPS** or **wOBA** tend to have higher **WAR** (Wins Above Replacement)?  
2. Which team-level batting stats are most related to winning (even with our fake metric)?  
3. Are these relationships consistent across seasons?


## Data Source
Data was pulled from the **`pybaseball`** package, which scrapes FanGraphs and Baseball Reference.

```python
from pybaseball import batting_stats
bat = batting_stats(2023, 2025)
````

Each row represents a player’s seasonal stats.
I averaged them across seasons (by player and by team) to get more stable trends.

**Main columns used:**

* `OPS` – On-base Plus Slugging
* `wOBA` – Weighted On-base Average
* `SLG`, `HR`, `Barrel%`, `HardHit%` – power/contact indicators
* `WAR` – overall player value


## Methods

### 1. Player-Level Analysis

* Combined 2023–2025 data and averaged each player’s stats.
* Plotted **OPS vs WAR** and **wOBA vs WAR** to see which metrics align best with value.
* Generated a correlation heatmap between main hitting metrics.

### 2. Team-Level Analysis

* Averaged stats by team.
* Built a **fake win percentage** using normalized OPS (`OPS / OPS.max()`).
* Visualized team OPS/wOBA vs fake win%, plus a correlation heatmap.

### 3. Tools

* `pandas` – data cleaning, grouping
* `matplotlib` & `seaborn` – visualization
* `pybaseball` – data collection


## Results

### Player-Level

* **OPS** and **wOBA** both show strong positive relationships with **WAR** (corr ≈ 0.8).
* `Barrel%` and `HardHit%` are moderately correlated (~0.5–0.6).
* The heatmap confirms OPS and wOBA are the clearest offensive predictors of WAR.

### Team-Level

* **Team OPS** and **wOBA** strongly align with the fake win% (corr ≈ 0.85).
* Teams with higher average OPS also have higher simulated success.

---

## Discussion

Even without official standings, the pattern holds:
teams that get on base more and hit for power win more often.
OPS and wOBA remain the simplest and most reliable indicators of team offense.

**Limitations**

* Fake win% is based only on hitting — no pitching or defense.
* Missing official win/loss data means results are approximate.
* Correlation ≠ causation.

**Next Steps**
Once standings data works again, re-run the analysis using actual win%.
Could also integrate pitching stats (ERA, FIP, etc.) for a fuller model.


## How to Run

### Requirements

```
pybaseball >= 2.2.0
pandas
matplotlib
seaborn
```

### Steps

1. Open the notebook or Colab.
2. Install dependencies:

   ```python
   !pip install pybaseball pandas matplotlib seaborn
   ```
3. Run the notebook top to bottom to pull data and generate charts.


## Folder Structure

```
mlb_batting_analysis/
│
├── midterm_for_data_bootcamp.ipynb   # main notebook
└── README.md
```

## Example Insights

* Aaron Judge and Bobby Witt Jr. appear among the top hitters by WAR (2023–2025).
* Team-level OPS correlates with fake win% at **0.84**.
* Player-level OPS correlates with WAR at **0.79**.


## References

* [pybaseball GitHub](https://github.com/jldbc/pybaseball)
* [FanGraphs Glossary](https://library.fangraphs.com/statistics/)
* [Baseball Reference](https://www.baseball-reference.com/)


