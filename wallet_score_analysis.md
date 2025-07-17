# analysis.md

## 📈 Credit Score Distribution

The rule-based credit scores were generated in the range of 0 to 1000. Here's a breakdown of score distribution:

| Score Range | Wallet Count | % of Wallets |
|-------------|---------------|---------------|
| 0–100       | X             | Y%            |
| 100–200     | X             | Y%            |
| 200–300     | X             | Y%            |
| 300–400     | X             | Y%            |
| 400–500     | X             | Y%            |
| 500–600     | X             | Y%            |
| 600–700     | X             | Y%            |
| 700–800     | X             | Y%            |
| 800–900     | X             | Y%            |
| 900–1000    | X             | Y%            |

*Replace X and Y% with actual values if available.*

---

## 🧰 Behavior of Wallets in Lower Score Range (0–300)
- **High liquidation counts**: These wallets experienced multiple liquidations.
- **Low repayment ratio**: These wallets borrowed more than they repaid.
- **Low deposits**: Financial activity on the protocol was minimal.
- **High borrow-to-deposit ratio**: Indicates risky borrowing behavior.

---

## 🥇 Behavior of Wallets in Higher Score Range (700–1000)
- **Consistently repaying loans** with high repay-to-borrow ratios
- **High total deposits and redeem activity**, showing responsible usage
- **Few or zero liquidations**, indicating healthy risk management
- **High number of total transactions**, indicating active and engaged usage

---

## ⚠️ Outlier Insights (via Boxplots)
- Outliers were primarily observed in:
  - `total_borrow` and `total_repay`: some whales had large-scale activity
  - `liquidation_count`: some wallets were repeatedly liquidated
- These outliers affect average behavior and reinforce the need for **robust scaling and weighting** in scoring

---

## 🚀 Recommendations
- Use scoring in downstream credit risk models or loan limit calculations
- Periodically re-score wallets as behavior evolves
- Integrate scoring into dashboards for monitoring user behavior over time

