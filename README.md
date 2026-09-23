# Customer Churn Analysis (Power BI)

A data analytics portfolio project: why are customers leaving Databel, a telecom
provider, and where should the business focus retention efforts? Built end-to-end
in Power BI, using DAX measures, calculated columns, and a 5-page dashboard, on the
DataCamp case study dataset *"Analyzing Customer Churn in Power BI."*

[![Overview page](<Power BI/screenshots/page1_overview.png>)

## Key Findings

- Overall churn rate: **26.86%** (roughly 1 in 4 customers have churned: 1,796 of 6,687).
- **Contract type is the strongest driver found:** Month-to-Month customers churn
at **46.29%**, versus 11.29% for One Year and 2.78% for Two Year contracts.
- **Nearly half of churn is competitive:** 44.82% of churned customers cite a
competitor as the reason: a "better offer elsewhere" problem more than a
product-quality one.
- **California is a major outlier:** 63.24% churn, more than double the 26.48%
average across all other states.
- **Senior customers (65+) churn at 38.46%**, notably higher than customers aged
30–64 (24.54%) or under 30 (23.00%).

---

## Main Question

Why are Databel's customers churning, and which customer segments should
retention efforts prioritize?

**Key questions answered:**

1. What is the overall churn rate, and which segments drive it most?
2. Which churn reasons and churn categories explain the majority of losses?
3. Are demographic groups (age, gender, group-contract status) more prone to churning?
4. Does contract type or payment method predict churn risk?
5. Do usage patterns (plan type, extra charges, customer service calls) correlate with churn?
6. Are there geographic outliers worth flagging?

---

## Data Source

Dataset: **Databel**, a fictitious telecom provider, from DataCamp's case study
*"Analyzing Customer Churn in Power BI."* 29 columns, one row per customer,
single point-in-time snapshot.

| Field group | Columns |
|---|---|
| Customer status | Customer ID, Churn Label, Churn Reason, Churn Category |
| Demographics | Gender, Age, Under 30, Senior |
| Contract information | Contract Type, Payment Method, State, Phone Number, Group, Number of Customers in a Group |
| Subscription & usage | Account Length, Local Calls, Local Mins, Intl Calls, Intl Mins, Intl Active, Intl Plan, Extra International Charges, Customer Service Calls, Avg Monthly GB Download, Unlimited Data Plan, Extra Data Charges, Device Protection & Online Backup, Monthly Charges, Total Charges |

The dataset is DataCamp course material and isn't redistributed in this repo. What
the data looks like, reconstructed by hand to match the real schema (not exported
from the original file):

| Customer ID | Churn Label | Age | Gender | Contract Type | Payment Method | Monthly Charge |
|---|---|---|---|---|---|---|
| CUST-0001 | Yes | 42 | Male | Month-to-Month | Credit Card | $53.85 |
| CUST-0002 | Yes | 29 | Female | Month-to-Month | Paper Check | $70.70 |
| CUST-0003 | No | 61 | Female | One Year | Direct Debit | $29.85 |
| CUST-0004 | No | 34 | Male | Two Year | Credit Card | $89.10 |
| CUST-0005 | No | 71 | Female | Month-to-Month | Direct Debit | $19.95 |

Full dataset and column definitions: [DataCamp - Analyzing Customer Churn in Power BI](https://app.datacamp.com/learn/courses/case-study-analyzing-customer-churn-in-power-bi).
A full 29-column illustrative sample (10 hand-built rows, matching the real schema)
is in [`data_sample/databel_sample_illustrative.csv`](data_sample/databel_sample_illustrative.csv).
See [How It Was Built](#how-it-was-built) for the dashboard, which is the deliverable.

---

## How It Was Built

1. **Explore**: data check, churn rate/reason measures, column groupings via the metadata sheet.
2. **Analyze**: DAX measures (Churn Rate, Competitor Churn %, binned segments) and
calculated columns (e.g. merging Under 30 / Senior flags into one Age Segment field).
3. **Visualize**: Power BI Desktop, 5 report pages, each built around a specific business question.
4. **Consolidate**: condensed from an original 10-page exploratory workbook into
5 focused, stakeholder-ready pages.

**Tools:** Power BI Desktop · DAX

---

## Dashboard Walkthrough

### Page 1: Overview

[![Overview page](https://github.com/Hakim-elazzouzi/customer-churn-analysis-powerbi/raw/main/screenshots/page1_overview.png)](https://github.com/Hakim-elazzouzi/customer-churn-analysis-powerbi/blob/main/screenshots/page1_overview.png)

Headline churn rate, top churn reasons, churn category split, contract type mix,
and churn rate by state: the at-a-glance summary the other pages build on.

### Page 2: Customer Demographics

[![Customer Demographics page](https://github.com/Hakim-elazzouzi/customer-churn-analysis-powerbi/raw/main/screenshots/page2_customer_demographics.png)](https://github.com/Hakim-elazzouzi/customer-churn-analysis-powerbi/blob/main/screenshots/page2_customer_demographics.png)

Churn by age group, gender, and group-contract status. Age is modeled as a
single 3-category field (Under 30 / 30–64 / Senior) rather than two overlapping
Yes/No flags, so the segment comparison reads cleanly.

### Page 3: Contract & Payment

[![Contract and Payment page](https://github.com/Hakim-elazzouzi/customer-churn-analysis-powerbi/raw/main/screenshots/page3_contract_and_payment.png)](https://github.com/Hakim-elazzouzi/customer-churn-analysis-powerbi/blob/main/screenshots/page3_contract_and_payment.png)

Churn by contract type and payment method, plus account tenure against churn,
the clearest single predictor in the dataset.

### Page 4: Usage & Charges

[![Usage and Charges page](https://github.com/Hakim-elazzouzi/customer-churn-analysis-powerbi/raw/main/screenshots/page4_usage_and_charges.png)](https://github.com/Hakim-elazzouzi/customer-churn-analysis-powerbi/blob/main/screenshots/page4_usage_and_charges.png)

Churn against plan type (international/unlimited data), extra charges, and
customer service call volume, a proxy for customer frustration before they leave.

### Page 5: Insights

[![Insights page](https://github.com/Hakim-elazzouzi/customer-churn-analysis-powerbi/raw/main/screenshots/page5_insights.png)](https://github.com/Hakim-elazzouzi/customer-churn-analysis-powerbi/blob/main/screenshots/page5_insights.png)

The 4 headline findings, callout-style, each paired with a small supporting
visual rather than a full chart to interpret.

---

## Notable Detail: A Caught and Corrected Measure

An early version of the Competitor Churn % card showed an impossible **1.00**
instead of a percentage. Traced to the DAX measure's `DIVIDE` logic and the
card's number formatting; corrected to the expected **44.82%**, which now
matches the Churn Category breakdown on Page 1 exactly.

## Known Data Limitations

- Single point-in-time snapshot: no trend or time-series analysis is possible.
- Some segments (e.g. high customer-service-call counts) have small sample
sizes, which can produce noisy or extreme churn rates; those figures should be
read directionally, not as precise values.
- Findings are descriptive (what happened, how it breaks down), not predictive or causal.

---

## Repository Structure

```
customer-churn-analysis-powerbi/
├── README.md
├── LICENSE
├── data_sample/
│   └── databel_sample_illustrative.csv
└── Power BI/
    ├── powerbi/
    │   └── Databel_Final_Dashboard.pbix
    └── screenshots/
        ├── page1_overview.png
        ├── page2_customer_demographics.png
        ├── page3_contract_and_payment.png
        ├── page4_usage_and_charges.png
        └── page5_insights.png
```

---

**Data:** DataCamp case study, Databel (fictitious): course material, not redistributed
**Code:** MIT License (see [LICENSE](LICENSE))
**Certified:** DataCamp, *Case Study: Analyzing Customer Churn in Power BI* (Aug 2026)
