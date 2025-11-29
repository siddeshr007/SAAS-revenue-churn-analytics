# SaaS Revenue & Churn Dashboard – Case Study

## 1. Business Context

A mid-sized B2B SaaS company sells subscription plans at three tiers 
(**Basic, Standard, Premium**) across four regions 
(**APAC, Europe, LATAM, North America**). 

Leadership is concerned that churn may be increasing and that revenue is too
concentrated in a small subset of customers. They have requested a dashboard 
that summarises revenue, churn, and customer growth so they can prioritise 
retention and growth initiatives.

This case study uses a simulated dataset to demonstrate how a Business Analyst
could approach this problem end to end.

---

## 2. Objectives

The analysis and dashboard were designed to answer:

1. **How many customers do we have, and how many are active vs churned?**
2. **How much Monthly Recurring Revenue (MRR) do we generate, and which plans
   contribute the most?**
3. **Which plans and regions have the highest churn rates?**
4. **How are customer signups distributed over the year (seasonality)?**
5. **Where should the company focus to reduce churn and protect revenue?**

---

## 3. Dataset & Methodology

### 3.1 Dataset

- Source: `data/saas_customers.xlsx` (simulated dataset).
- Grain: one row per customer.
- Key fields:
  - `customer_id`
  - `signup_month`
  - `plan_type` (Basic, Standard, Premium)
  - `region` (APAC, Europe, LATAM, North America)
  - `acquisition_channel` (Ads, Organic, Referral, Partner)
  - `status` (Active, Churned)
  - `monthly_fee`
  - `tenure_months`
  - `churned_after_months` (for churned customers)

### 3.2 Tools

- **Excel** – dataset design and generation.
- **Tableau Public** – dashboard creation and visual analysis.
- **Markdown + GitHub** – documentation (BRD, case study, README).

### 3.3 Approach

1. **Designed the dataset** structure to reflect a realistic SaaS subscription model.
2. **Populated** sample data for 150 customers with randomised signup dates, plans,
   regions, fees, statuses, and tenures.
3. **Defined KPIs** in Tableau:
   - Total Customers, Active Customers, Churned Customers
   - Churn Rate (overall & by plan)
   - Active MRR (overall & by plan)
   - Customers by Region
   - Customer Signups by Month
4. **Developed a dashboard** with:
   - KPI banner
   - MRR by Plan
   - Churn Rate by Plan
   - Customers by Region
   - Signups by Month
   - Region filter
5. **Interpreted** the patterns and translated them into business insights 
   and recommendations.

---

## 4. Headline Metrics (at time of snapshot)

- **Total Customers:** 150  
- **Active Customers:** 111  
- **Churned Customers:** 39  
- **Overall Churn Rate:** ~26%  
- **Active MRR:** \$8,075  

**MRR by Plan Type (Active Customers)**

- Basic: **\$1,101**
- Standard: **\$2,418**
- Premium: **\$4,556**

**Churn Rate by Plan Type (approx.)**

- Basic: **19.6%**
- Premium: **22.9%**
- Standard: **33.9%**

**Customers by Region**

- APAC: **36**
- Europe: **33**
- LATAM: **39**
- North America: **42**

**Customer Signups by Month (count of new customers)**

| Month     | Signups |
|-----------|---------|
| January   | 8       |
| February  | 15      |
| March     | 12      |
| April     | 10      |
| May       | 10      |
| June      | 10      |
| July      | 12      |
| August    | 17      |
| September | 15      |
| October   | 15      |
| November  | 17      |
| December  | 9       |

---

## 5. Key Insights

1. **Revenue is concentrated in higher-tier plans.**  
   Premium customers generate around **\$4.6k of active MRR**, almost four times 
   Basic (**\$1.1k**) and significantly more than Standard (**\$2.4k**). 
   This indicates that protecting and expanding Premium subscriptions is critical 
   to revenue.

2. **Overall churn is high and a significant risk.**  
   Out of 150 customers, **39 have churned**, corresponding to a churn rate of 
   roughly **26%**. If this pattern persists, a large portion of future recurring
   revenue will be at risk.

3. **Standard plan shows the weakest retention performance.**  
   Churn rate by plan is approximately **19.6% for Basic**, **22.9% for Premium**, 
   and a much higher **33.9% for Standard**. Standard customers appear least 
   satisfied or least well-matched to the product and may need targeted interventions.

4. **Customer base is balanced across regions.**  
   Customer counts are relatively even (APAC 36, Europe 33, LATAM 39, 
   North America 42). This means churn or growth in any single region can 
   materially affect overall performance; no single region dominates the base.

5. **Clear seasonality in signups.**  
   Signups peak in **February, August, and November (15–17 customers each)**, 
   while **January and December** are relatively weak. This suggests a seasonality 
   pattern that marketing can exploit, aligning campaigns with higher-response months 
   and boosting activity in slower periods.

---

## 6. Recommendations

Based on the insights above, the following actions are recommended:

### 6.1 Stabilise the Standard Plan

- Conduct a focused review of the **Standard** plan:
  - Pricing vs. value delivered.
  - Feature set compared to Basic and Premium.
  - Onboarding and support experience.
- Introduce **targeted retention offers** for Standard customers at high churn risk
  (e.g., tenure 1–3 months):
  - Time-limited discounts,
  - Feature trials or upgrade paths to Premium,
  - Proactive customer success outreach.

### 6.2 Protect High-Value Premium Revenue

- Offer **loyalty rewards or annual contracts** for Premium customers to secure 
  recurring revenue and reduce the chance of churn.
- Monitor **NPS / satisfaction** for Premium customers closely; small losses in
  this segment have disproportionate revenue impact.

### 6.3 Use Seasonality in Marketing Planning

- Increase marketing spend and sales focus in **February, August, and November** 
  when signups are historically strongest, to maximise growth.
- Design **special offers or campaigns** for **January and December**, where demand 
  is weaker, to smooth acquisition across the year.

### 6.4 Region-Focused Monitoring

- While regions are balanced in customer count, the dashboard should be used to:
  - Monitor **churn rate by region** over time (next iteration).
  - Identify any region-specific issues such as localisation, support hours, or
    payment methods.
- Run **retention experiments** in the worst-performing region first and replicate 
  successful tactics elsewhere.

---

## 7. Limitations

- The dataset is **simulated** and not based on a real company; absolute values 
  should be treated as illustrative.
- Churn is modelled as a **current status**, not a detailed time series event 
  (e.g., monthly churn flows).
- Customer acquisition channel is present in the data but not deeply analysed in 
  this first version of the dashboard.

---

## 8. Next Steps

- Extend the dataset and dashboard with **cohort-style retention** views 
  (churn by signup month).
- Incorporate **acquisition channel** into the analysis to compare churn and LTV by 
  channel (Ads vs Organic vs Referral vs Partner).
- If real data is available, validate the patterns and refine thresholds for 
  churn alerts and retention campaigns.

---

## 9. Files & Artefacts

- Tableau dashboard: `tableau/saas_revenue_churn.twbx`
- Dataset: `data/saas_customers.xlsx`
- BRD: `docs/BRD_saas_revenue_churn_dashboard.md`
- Case study (this file): `docs/case_study_saas_revenue_churn.md`
