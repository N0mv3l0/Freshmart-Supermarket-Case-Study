# FreshMart Supermarkets | Business Analysis Case Study

## Understanding the Gap Between Footfall and Sales Growth

## Project Overview

FreshMart Supermarkets is a fictional South African grocery retailer operating 42 stores across Gauteng, Western Cape and KwaZulu-Natal.

The business raised a concern: customer footfall was reportedly increasing, but sales were not growing at the same pace. Management suspected that customers were spending less per shopping trip.

As the Business Analyst, I investigated this problem using transaction, store and stockout data for the 2025 calendar year.

The objective was to understand changes in basket value and shopping behaviour, identify possible operational and competitive factors, and recommend practical actions that could help FreshMart improve its performance.

## Business Problem

The central business question was:

**Are customers making more shopping trips but spending less per visit, and what factors could explain this pattern?**

To investigate this, I examined:

- Average basket value (ZAR).
- Average number of items per basket.
- Recorded transaction volumes.
- Monthly and half-year performance trends.
- Basket-value distribution and shopping patterns.
- Loyalty versus non-loyalty transactions.
- Store and province performance.
- Competitor opening dates.
- Recorded stockout incidents.

## Dataset Overview

The analysis used three related datasets:

| Dataset | Description | Records |
|---|---|---:|
| Transactions | Individual till transactions and basket information | 64,330 |
| Stores | Store details, location, format and competitor information | 42 |
| Stockouts | Recorded product availability incidents | 119 |

**Analysis period:** 1 January 2025 to 31 December 2025.

The tables were linked using `store_id`.

### Important data considerations

- The transaction dataset is a representative sample, not a complete record of all FreshMart sales.
- Recorded transaction counts should not be interpreted as actual store footfall.
- Blank `customer_id` values represent non-loyalty shoppers.
- Missing competitor opening dates are expected for stores marked as having no nearby competitor.
- Stockout information relates to recorded events and should not automatically be interpreted as proof that a particular transaction was affected.

## Tools and Technologies

The following tools and libraries were used:

- **Databricks:** Data ingestion and analysis environment.
- **Python:** Data analysis and preparation.
- **Pandas:** Data cleaning, transformation, grouping and aggregation.
- **NumPy:** Numerical operations and derived calculations.
- **Matplotlib:** Data visualisation and dashboard development.

## Project Workflow

### 1. Data ingestion and exploration

Loaded the three datasets from Databricks:

- Transactions
- Stores
- Stockouts

Performed initial exploration to understand the dataset structure, row counts, column names, data types and available variables.

### 2. Data cleaning and preparation

Performed data-quality checks and prepared the datasets for analysis.

Key activities included:

- Converting transaction and stockout dates into datetime formats.
- Converting basket values into numeric values.
- Standardising column names and data types.
- Checking missing values and duplicate records.
- Checking unique transaction, store and stockout identifiers.
- Validating store IDs before joining datasets.
- Identifying and handling missing values appropriately.
- Creating derived analytical fields.

### 3. Data integration

Combined the three datasets to create an analysis-ready dataset.

- Joined Transactions and Stores using `store_id`.
- Aggregated stockout events to store-day level.
- Joined the stockout summary using `store_id` and transaction date.
- Validated the resulting dataset to ensure that transaction records were preserved.

**Final analysis dataset:** 64,330 rows and 29 columns.

Validation confirmed:
- 64,330 unique transactions.
- Zero duplicate transaction IDs.
- Zero missing store names after the store join.
- Transaction date coverage from January to December 2025.

### 4. Exploratory Data Analysis

Explored transaction patterns across different dimensions, including:

- Monthly transaction volumes.
- Average and total recorded basket value.
- Store performance.
- Province and store-format comparisons.
- Loyalty and non-loyalty shopping behaviour.
- Weekday and weekend patterns.
- Payment methods.
- Basket-value bands.

### 5. Hypothesis investigation

Investigated possible explanations for declining basket spending.

**Hypothesis 1: Customers are spending less per shopping trip.**

Compared average basket value, average items per basket and recorded transaction volumes between the first and second halves of 2025.

**Hypothesis 2: Nearby competitors may be affecting store performance.**

Compared average basket value before and after recorded competitor opening dates for stores with nearby competitors.

**Hypothesis 3: Stockouts may be associated with lower basket spending.**

Compared transaction basket metrics on store-days with recorded stockout incidents against other store-days.

**Hypothesis 4: Customer and shopping patterns may help explain the decline.**

Examined loyalty status, basket-value distribution, shopping days and payment methods to identify differences in transaction behaviour.

## Key Findings

### 1. First-half versus second-half performance

The comparison between the first and second halves of 2025 revealed:

| Performance metric | Change |
|---|---:|
| Recorded transactions | +6.79% |
| Total recorded basket value | -3.86% |
| Average basket value | -9.97% |
| Average items per basket | -10.56% |

**Business insight:**

The number of recorded transactions increased in the second half of the year, while total recorded basket value declined. Average basket value and average items per basket also decreased.

This pattern is consistent with customers making smaller purchases, although the transaction sample alone cannot confirm the chain-wide footfall or turnover position.

### 2. Loyalty versus non-loyalty shoppers

The overall average basket values were:

| Customer group | Average basket value |
|---|---:|
| Loyalty transactions | R294.12 |
| Non-loyalty transactions | R259.79 |

Loyalty transactions had a higher average basket value in the dataset.

This is a descriptive comparison and does not establish that loyalty membership causes higher spending.

### 3. Stockout analysis

The stockout comparison revealed:

| Metric | Average basket value |
|---|---:|
| Transactions on recorded stockout days | R232.24 |
| Transactions on other store-days | R275.49 |
| Difference | -R43.25 |

There were 606 transactions matched to recorded stockout days.

Additional observations:
- The recorded stockout events affected the Household Cleaning category.
- All recorded incidents shared the operational note: "Replenishment gap - weekend delivery missed".

**Business insight:**

Transactions on recorded stockout days had a lower average basket value than transactions on other store-days. This is an association and does not prove that stockouts caused the difference.

### 4. Competitor analysis

The Stores dataset identified:

- 12 stores with a nearby competitor.
- 30 stores without a nearby competitor.

All 12 stores marked as having a nearby competitor had recorded opening dates.

The analysis used a before-and-after comparison to investigate changes in average basket value around competitor opening dates.

The comparison should be interpreted cautiously because other factors may also influence store performance.

## Matplotlib Dashboard

A business performance dashboard was developed using Matplotlib to communicate the main findings visually.

The dashboard includes four visualisations:

1. **Average Basket Value by Month:** Tracks changes in average customer spending throughout 2025.
2. **Recorded Transactions by Month:** Shows monthly changes in recorded transaction volumes.
3. **Monthly Share by Basket-Value Band:** Examines the distribution of low-, medium- and high-value baskets over time.
4. **Average Basket Value by Stockout Status:** Compares basket spending on recorded stockout days and other store-days.

The dashboard was designed to make the analysis easier to understand and communicate to business stakeholders.

## Business Recommendations

Based on the patterns identified, the following actions are proposed for FreshMart management.

### 1. Investigate declining basket spending

Review pricing, promotions and basket composition to understand why average basket value and items per basket declined.

**Suggested KPIs:**
- Average basket value.
- Average items per basket.
- Percentage of low-value baskets.

### 2. Improve stock availability

Review weekend delivery schedules and replenishment processes, particularly for Household Cleaning products at affected stores.

**Suggested KPIs:**
- Number of stockout incidents.
- Total stockout duration.
- Repeat stockout incidents by store.

### 3. Investigate competitor-affected stores

Review the performance of stores where basket values declined after a nearby competitor opened.

**Suggested KPIs:**
- Average basket value by store.
- Average items per basket.
- Recorded transaction volumes.

### 4. Strengthen customer loyalty initiatives

Use the loyalty analysis to identify customer groups that may benefit from targeted promotions and relevant offers.

**Suggested KPIs:**
- Average basket value by loyalty status.
- Average items per basket by loyalty status.
- Monthly transaction trends by customer group.

### 5. Monitor store-level performance

Use regular store-level reporting to identify locations experiencing declining basket values or recurring operational issues.

## Limitations

The following limitations should be considered when interpreting the findings:

- The transaction dataset is a sample and does not represent every FreshMart sale.
- Recorded transaction volumes are not equivalent to actual customer footfall.
- The dataset covers 2025 only, so a year-on-year comparison cannot be independently calculated.
- Stockout events relate to Household Cleaning, and the available transaction data does not identify the product categories within individual baskets.
- Competitor before-and-after comparisons do not independently establish causation.
- Differences in basket value may also reflect changes in customer or shopping-trip mix.

Further analysis using complete sales, footfall, product-level, pricing and promotion data would strengthen the investigation.

## Conclusion

The FreshMart case study demonstrates how business analysis can turn an ambiguous business concern into a measurable investigation.

The analysis identified a clear difference between the first and second halves of 2025: recorded transaction volumes increased, while average basket value and average items per basket declined.

The stockout comparison also highlighted a potential operational issue worth investigating, particularly around weekend replenishment.

The findings provide FreshMart management with practical areas to investigate further, test improvements and monitor performance.

**The key business message is that increasing shopping activity does not necessarily translate into higher value per transaction. FreshMart should focus not only on attracting customers, but also on understanding and improving the value of each shopping trip.**

---

## Project Files

Suggested repository structure:

```text
FreshMart-Business-Analysis/
│
├── README.md
│
├── notebooks/
│   └── Freshmart_EDA.ipynb
│
├── dashboard/
│   └── FreshMart_Business_Performance_Dashboard_2025.pdf
│
└── images/
    └── freshmart_dashboard_2025.png
```

*Note: Add the dashboard image and PDF to these folders if you choose to use this structure.*

## Skills Demonstrated

- Business problem definition
- Exploratory Data Analysis (EDA)
- Data cleaning and preparation
- Data integration and joins
- Data validation and quality checks
- Data aggregation and segmentation
- Hypothesis investigation
- Business insight generation
- Data visualisation with Matplotlib
- Evidence-based recommendations
- Business storytelling and communication

**Tools:** Python | Pandas | NumPy | Matplotlib | Databricks
