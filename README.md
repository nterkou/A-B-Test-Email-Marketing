# A/B Test Analysis — Email Marketing Campaign

End-to-end A/B test analysis of an email marketing campaign, written for junior data scientists.
Covers EDA, statistical testing, effect sizing, and business value estimation.

## What's in the notebook

| Step | Description |
|------|-------------|
| 1 | Load & understand the data |
| 2 | Exploratory Data Analysis (EDA) — funnel, revenue distribution, event rates |
| 3 | Experiment validity checks (group balance, funnel logic) |
| 4 | KPI calculation — open rate, CTR, conversion rate, unsubscribe rate, revenue/user |
| 5 | Statistical significance — chi-square & Mann-Whitney U tests |
| 6 | Effect size — relative uplift per metric |
| 7 | Business value estimation — incremental revenue, LTV impact, cost-benefit projection |

## Dataset

`ab_test_email_campaign.csv` — synthetically generated dataset, one row per user, 10,000 rows total.

The data was generated with `numpy` using realistic probabilities per group:

| Event | Control | Treatment |
|-------|---------|-----------|
| Open rate | 25% | 30% |
| Click rate | 10% | 13% |
| Conversion rate | 10% | 12% |
| Unsubscribe rate | 2% | 4% |

Revenue was sampled from a uniform distribution (£20–£100) for users who converted.
The funnel is enforced: a user can only click if they opened, and only convert if they clicked.

| Column | Description |
|--------|-------------|
| `user_id` | Unique user ID |
| `group` | `control` or `treatment` |
| `opened_email` | 1 if user opened the email |
| `clicked_email` | 1 if user clicked a link |
| `converted` | 1 if user made a purchase |
| `unsubscribed` | 1 if user unsubscribed |
| `revenue` | Purchase value in £ (0 if no purchase) |

## Results

| Metric | Control | Treatment | Uplift | Significant? |
|--------|---------|-----------|--------|--------------|
| Conversion Rate | 0.12% | 0.46% | +285% | ✅ p=0.003 |
| Revenue / User | £0.067 | £0.239 | +258% | ✅ p=0.005 |
| Unsubscribe Rate | 1.89% | 4.01% | +112% | ✅ ⚠️ Guard-rail breach |

**Recommendation:** roll out with close monitoring of the unsubscribe rate.

## Requirements
pandas
matplotlib
seaborn
scipy
numpy

## Usage

```bash
pip install pandas matplotlib seaborn scipy numpy
jupyter notebook AB_Testing_Business_Simple.ipynb
```

> **Note:** The LTV parameters (`REPEAT_BUYS`, `CHURN_MONTH`) in Step 7 are illustrative.
> Calibrate them from real cohort data before using the business projection in production.