# Cookie Cats: Gate Placement A/B Test Analysis

Analysis of a real A/B test run by Tactile Entertainment on their mobile puzzle game, Cookie Cats. The test examined whether moving the game's first progression gate from level 30 to level 40 affects player retention.

## Business Question
Does moving the first gate later in the game (level 30 → level 40) help or hurt player retention?

## Dataset
- **Source:** [Mobile Games A/B Testing - Cookie Cats](https://www.kaggle.com/mursideyarkin/mobile-games-ab-testing-cookie-cats) (Kaggle)
- **Size:** 90,189 players who installed the game during the test window
- **Columns:** `userid`, `version` (gate_30 / gate_40), `sum_gamerounds`, `retention_1`, `retention_7`

## Method
1. Loaded and cleaned the data (removed one extreme outlier — a player with 49,854 rounds played)
2. Queried the data with **SQL** (SQLite) to compare group-level stats
3. Ran **chi-square tests of independence** to check whether retention differences between groups were statistically significant
4. **Segmented** players into Low / Medium / High engagement tiers to check whether the effect was consistent across player types
5. Visualized findings with matplotlib/seaborn

## Key Findings
- **1-day retention:** No statistically significant difference between groups (p = 0.075)
- **7-day retention:** Significantly lower for gate_40 (p = 0.0016)
- The negative effect of gate_40 was **not uniform** — it was strongest among high-engagement players, while low-engagement players were largely unaffected

## Recommendation
Keep the gate at level 30. Moving it to level 40 appears to reduce long-term (7-day) retention, particularly among the most engaged players — the segment most valuable to retain.

## Limitations
- Retention only; doesn't account for monetization or session length
- Single time-period snapshot, so findings may not generalize to current player behavior
- Engagement segments were defined by tercile split on rounds played, a simplification of "engagement"

## Tools
Python (pandas, SciPy, matplotlib, seaborn), SQL (SQLite)

## Files
- `analysis.ipynb` — full analysis notebook
- `cookie_cats.csv` — raw dataset
- `retention_charts.png` — summary visualization
