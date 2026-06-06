**NCAA MBB Bracket Prediction**

**Overview**

Each matchup is resolved with a win-probability model driven by the difference in team strength. Team strength is summarized by adjusted efficiency margin (AdjEM = AdjO − AdjDef). The tournament is then simulated 100,000 times via Monte Carlo methods to estimate each team's probability of advancing through every round, from the Round of 64 to the title.

**Methodology**

Win probability follows a logistic function on the efficiency-margin gap between two teams:

​**P(win) = 1 / 1 + exp( - (E₁ - E₂ / σ)**

where:

E₁, E₂ are the two teams' adjusted efficiency margins (AdjEM = AdjO − AdjDef).
σ is a scaling parameter that controls how sharply a margin gap maps to win probability. The model uses σ = 10, consistent with published estimates from KenPom-based models.

The full bracket is advanced round by round: each game is simulated using these probabilities, winners feed into the next round's matchups, and the process repeats across 100,000 simulated tournaments. Round-by-round advancement frequencies become each team's estimated odds.
Data
FileDescriptionstats_MOH.csvTeam efficiency ratings (team, adj_off, adj_def); AdjEM computed as adj_off − adj_defbracket_MOH.csvBracket structure (region, seed, slot, team) for all 64 teams
The two files are merged on team and arranged by region and slot to build the bracket.

**Output**

A full table of all 64 teams with their efficiency ratings (AdjO, AdjDef, AdjEM).
Game-by-game win probabilities.
Monte Carlo advancement odds for each team by round.

**Usage**

r# From R / RStudio
install.packages(c("tidyverse", "knitr", "kableExtra"))
Knitting the file loads the data, computes win probabilities for every matchup, runs the 100,000-simulation Monte Carlo, and renders the results as an HTML report.
Tech Stack
R · R Markdown · tidyverse · knitr · kableExtra

**Notes**

σ is the main lever for calibration; lower values make outcomes more deterministic, higher values flatten probabilities toward 50/50.
The model is rating-driven and does not account for injuries, matchup-specific dynamics, or in-tournament news.

**Author**

Evan Heffelfinger
