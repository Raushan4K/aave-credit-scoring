# README.md

## Project: Credit Scoring System on Aave V2 Wallets

This project builds a **rule-based credit scoring system** to assign scores between **0 and 1000** to wallets interacting with the **Aave V2 protocol**, based on their behavior. The goal is to reward healthy financial behavior and penalize risky patterns using Aave on-chain transaction data.

---

## Project Domain

- **Domain:** Decentralized Finance (DeFi)
- **Platform:** Aave V2 protocol
- **Data Source:** Historical transactions (e.g. deposit, borrow, repay, liquidation)

---

## Problem Statement

> Build a credit scoring mechanism for wallets based on their activity on Aave V2. Each wallet must receive a score between 0–1000, where 1000 implies high financial health.

---

## Why Rule-Based and Not ML?

We tested several machine learning models (Linear Regression, Ridge, Random Forest, Gradient Boosting, SVR). However, **all models performed poorly** (R^2 ≈ -0.01 to -0.13).

Reasons for avoiding ML:

- Small dataset size
- Low variability in behavioral features
- Target variable (`credit_score`) was engineered, not ground truth

Hence, we **switched to a customizable rule-based scoring system** using domain knowledge and financial behavior logic.

---

## Features Used

- `total_deposit`: Total amount deposited
- `total_borrow`: Total borrowed
- `total_repay`: Total repaid amount
- `repay_to_borrow_ratio`: Ratio of repayment to borrow
- `total_transactions`: Overall activity
- `total_redeem`: Total redeem activity
- `liquidation_count`: Number of times the wallet was liquidated

---

## Scoring Logic (Rule-Based)

```python
score_raw = (
    (total_deposit_scaled * 0.25) +
    (total_repay_scaled * 0.25) +
    (repay_to_borrow_ratio_scaled * 0.20) +
    (total_transactions_scaled * 0.10) +
    (total_redeem_scaled * 0.10) -
    (liquidation_count_scaled * 0.40)
)
```

- **Positive behaviors** (deposits, repayments, redeem, high repay ratio) are rewarded.
- **Risky behavior** (liquidations) is penalized heavily.
- Final score is scaled to **0–1000** using MinMax normalization.

---

## Architecture & Pipeline

1. **Data Ingestion**: Load cleaned Aave wallet-level transaction data
2. **Feature Engineering**: Create aggregated features per wallet
3. **Preprocessing**: Handle missing/infinite values, scale numeric features
4. **Scoring**: Apply weighted rule-based formula
5. **Visualization**: Generate score distribution, correlations, and outlier detection
6. **Analysis**: Behavior insights across credit score buckets

---

## Visualizations

- Score distribution histogram
- Correlation heatmap of features
- Boxplots to identify outliers
- Predicted vs. actual plots (for ML models - all underfitted)

---

## Deliverables

- `credit_score_generator.py` - full scoring logic
- `README.md` - project summary, logic, architecture
- `analysis.md` - scoring results and wallet behavior analysis

---

## Future Work

- Improve scoring using unsupervised clustering (e.g., KMeans)
- Try hybrid approach with rule-based + anomaly detection
- Expand feature space with time-series and DeFi protocol interactions

