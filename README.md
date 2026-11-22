# miguel.martinez.github.io
# S&P 500 Big-Move Detection

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/miguelmartinezm-gwu/miguel.martinez.github.io/blob/main/DataMiningFinalProject_Corrected_Improved_Rev_11_21_2026.ipynb)

Random Forest classifier predicting whether the next trading day's SPY return
will exceed ±1% ("Big Move"), using Yahoo Finance price data and FRED macro
series. Built for CSCI 6443 (Data Mining), GWU, Fall 2026.

## How to use

1. Click **Open in Colab** above.
2. **Runtime → Run all**. No local setup and no API keys required — Yahoo
   Finance and FRED are both queried anonymously.
3. Scroll to the final cell (the orchestrator, bottom of Section 08) for the
   current day's Big-Move probability and the Section 10 condor/no-condor
   guardrail decision.

> Section 09 (Persistent Evaluation Log) mounts Google Drive to store a
> running CSV of past predictions. The first time you run it, Colab will ask
> you to authorize Drive access — accept it, or comment out that cell if you
> only want a one-off read.

## Structure

| Section | What it does |
|---|---|
| Disclaimer Cell | What this model is / is not — read this first |
| 00 - Setup | Imports, warnings config |
| 01 - Data Ingestion (Yahoo Finance) | Pulls SPY + FRED, 5yr and 10yr windows |
| 02 - Feature Engineering (Yahoo Finance) | Builds the 25-feature set (momentum, realized vol, VIX, FRED macro) |
| 03 - Walk-Forward Model Comparison (5yr vs 10yr vs 10yr-ex-COVID) | Compares 4 model families across 3 dataset windows |
| 04 - Final Model + Threshold Selection | Random Forest, 25 features, threshold tuned via Youden's J |
| 05 - PURGED WALK-FORWARD CV | Robustness check (purged/embargoed CV) on the winning dataset |
| 06 - FEATURE IMPORTANCE | Feature importances + master results table across all experiments |
| 07 - Retrospective Case Study (Oct 29-30 2026) | Re-tests a known large move against the final model |
| 08 - Live Recommendation Engine | Daily prediction + SPY holdings concentration pie chart + earnings/macro calendar flags |
| 09 - Persistent Evaluation Log | Logs and grades each day's prediction over time (Drive-backed CSV) |
| 10 - Condor Decision Framework | Automated condor/no-condor guardrail, consumes Section 08's output directly |
| 11 - Does a Big Down Day Predict Tomorrow's Direction? | Tests directional continuation/reversion — finds no exploitable edge |
| 12 - Appendix Diagnostics + Rebuilt Visuals | Leakage audit, fold-regime diagnostics, supporting charts |

## Key result

Random Forest, 10-year training window with the 2020 COVID window excluded,
threshold selected via Youden's J on the ROC curve. Walk-forward validated
(folds 2-8): Balanced Accuracy 0.666 ± 0.053, Recall 0.699 ± 0.175, Precision
0.400 ± 0.062.

See `SP500_Term_Paper.docx` in this repo for the full methodology, math
(Youden's J derivation, supervised vs. unsupervised framing), robustness
testing, and limitations.

## Disclaimer

Research/educational project only. **Not investment advice, not a
directional predictor, and not validated for live capital.** See the
Disclaimer Cell at the top of the notebook for the full "what this model is
and is not" statement before using any output below it.
