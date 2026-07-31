# Solution: iRage AlgoArena 2026 (March 23rd to 12th April)

## Ranked 1st out of 800+ candidates, won a cash price of Rs 200k

## The Challenge
* Predict the short-horizon percentage return of an asset's price using an anonymized dataset of 445 time-series features.
* Evaluated purely on the R-squared (R2) score under strict real-world generalization constraints.

## What Failed
* Tree-based residual hunting overfit the noise quickly.
* Complex deep learning models lacked the required signal strength.
* Standard 10-fold bagging and ensembling smoothed out our prediction variance way too much, which heavily penalized the R2 score.

## irage phase 0- The Initial Research Notebook
* This was the initial version of the research notebook which gave me a lot of insights that helped me a lot in the later phases of the competition to get more edge.

## What Succeeded: 
* **Dynamic Target Protection:** Forced a normal target distribution (Kurtosis = 3.0) on the training data to calculate safe, dynamic clipping boundaries.
* **Autoregressive Engineering:** Built simple Lag 1, Lag 2, and Lag 3 momentum features based on past returns.
* **Asymmetric Winsorization:** Clipped extreme feature outliers (0.1% to 99.9%) and targets (1.19% to 98.8%) to shield the model from black swan events.
* **Core Model:** Trained a highly stable, beta-neutral 2-component Partial Least Squares (PLS) regression.
* **Symbolic Modulators:** Stacked three custom non-linear feature interactions (a linear combination, a 2-D ReLU energy product, and a 5-D Omega stack) using offline-tuned multipliers.
* **Asymmetric Post-Processing:** Scaled the positive prediction tail by exactly 1.1x to perfectly match the raw target amplitude.
* **Robust Offline Evaluation:** Implemented a custom evaluation metric that directly replicated the competition's final scoring criteria, eliminating the risk of leaderboard shake-up.
