# SaaS Revenue & Churn Dashboard – Business Requirements Document (BRD)

## 1. Background & Context

A mid-sized B2B SaaS company has grown its subscription base over the last year. 
Leadership receives ad-hoc Excel reports from different teams, which are hard to 
reconcile and make it difficult to answer basic questions about recurring revenue,
customer growth, and churn.

To support better decision making, the company wants a single, reliable dashboard
showing how Monthly Recurring Revenue (MRR), customers, and churn are trending and
how they vary by plan type and region.

---

## 2. Business Problem

The company does not have:

- A unified view of **MRR and active customers**.
- Clear visibility into **which plans and regions drive revenue vs. churn**.
- A way to **monitor customer signups and churn over time** to spot trends and risks.

As a result, leadership cannot confidently answer questions such as:

- Are we growing or shrinking our recurring revenue?
- Which subscription plans are performing well or poorly?
- Where should we focus retention and marketing efforts?

---

## 3. Objectives

The dashboard should:

1. Provide a **single source of truth** for key subscription KPIs.
2. Show **MRR, active customers, and churn** at a glance.
3. Highlight **differences by plan type and region**.
4. Reveal **signup patterns over time** to support marketing planning.
5. Enable non-technical stakeholders to self-serve answers to basic revenue and churn questions.

---

## 4. Scope

### In Scope

- High-level subscription KPIs for the current customer base:
  - Total customers, Active customers, Churned customers
  - Churn rate
  - Active MRR
- Segmentation by:
  - Plan type: **Basic, Standard, Premium**
  - Region: **APAC, Europe, LATAM, North America**
- Time-based view of **customer signups by month**.
- Region-level filter to adjust the view.

### Out of Scope

- Customer-level profitability or cost analysis.
- Marketing attribution modelling.
- Detailed cohort analysis (e.g., retention by signup month).
- Predictive churn modelling.

---

## 5. Stakeholders & Users

- **VP of Product** – understands how plan structure impacts revenue and churn.
- **Head of Sales** – monitors customer growth and regional performance.
- **Customer Success Manager** – identifies high-churn segments to target with
  retention programs.
- **Executive Leadership** – reviews headline KPIs and high-level trends.

---

## 6. KPIs & Definitions

All KPIs are calculated at the **customer level** based on a simulated SaaS dataset.

1. **Total Customers**
   - Definition: Count of all customers in the dataset.
   - Calculation: `COUNTD(customer_id)`

2. **Active Customers**
   - Definition: Customers whose current status is `Active`.
   - Calculation: `COUNTD(customer_id WHERE status = "Active")`

3. **Churned Customers**
   - Definition: Customers whose status is `Churned` (subscription ended).
   - Calculation: `COUNTD(customer_id WHERE status = "Churned")`

4. **Churn Rate (overall)**
   - Definition: Share of customers who are currently churned.
   - Calculation (simplified point-in-time view):  
     `Churn Rate = Churned Customers / Total Customers`

5. **Active MRR**
   - Definition: Total monthly recurring revenue from active customers, using each
     customer’s plan-specific monthly fee.
   - Calculation: `SUM(monthly_fee WHERE status = "Active")`

6. **MRR by Plan Type**
   - Definition: Active MRR aggregated by subscription plan (Basic, Standard, Premium).
   - Calculation: `SUM(Active MRR) grouped by plan_type`

7. **Churn Rate by Plan Type**
   - Definition: Churn rate for each plan type.
   - Calculation (simplified):  
     `Churn Rate by Plan = Churned customers on plan / Total customers on plan`

8. **Customers by Region**
   - Definition: Distinct customer count per region.
   - Calculation: `COUNTD(customer_id) grouped by region`

9. **Customer Signups by Month**
   - Definition: Number of new customers whose signup month falls in each calendar month.
   - Calculation: `COUNTD(customer_id) grouped by signup_month`

---

## 7. Data Sources & Assumptions

- **Data Source:**  
  `data/saas_customers.xlsx` – simulated customer-level dataset created specifically
  for this case study.

- **Grain:**  
  One row per customer.

- **Key Columns:**
  - `customer_id`
  - `signup_month`
  - `plan_type` (Basic, Standard, Premium)
  - `region` (APAC, Europe, LATAM, North America)
  - `acquisition_channel` (Ads, Organic, Referral, Partner)
  - `status` (Active, Churned)
  - `monthly_fee`
  - `tenure_months`
  - `churned_after_months` (populated only for churned customers)

- **Assumptions:**
  - Monthly fee is a good proxy for MRR per customer.
  - Current `status` reflects whether the customer is considered active or churned.
  - Churn is represented as a **state** (Active vs Churned), not as a time series event.
  - Dataset is synthetic and used for analytical demonstration only.

---

## 8. Dashboard Requirements

### 8.1 Layout

- **Top KPI bar** with:
  - Total Customers
  - Active Customers
  - Churned Customers
  - Churn Rate
  - Active MRR

- **Middle row** with:
  - Left: MRR by Plan Type
  - Right: Customer Churn Rate by Plan Type

- **Bottom row** with:
  - Left: Customers by Region (Active vs Churned)
  - Right: Customer Signups by Month

### 8.2 Views

1. **Monthly Recurring Revenue by Plan Type**
   - Bar chart.
   - X-axis: `plan_type`
   - Y-axis: `SUM(Active MRR)`
   - Labels: currency labels on each bar.

2. **Customer Churn Rate by Plan Type**
   - Bar chart.
   - X-axis: `plan_type`
   - Y-axis: `Churn Rate by Plan` (percentage).
   - Percentage labels on each bar.

3. **Customers by Region (Active vs Churned)**
   - Stacked bar chart.
   - X-axis: `region`
   - Y-axis: `COUNTD(customer_id)`
   - Color: `status` (Active vs Churned).
   - Y-axis title: “Number of Customers”.

4. **Customer Signups by Month**
   - Vertical bar chart.
   - X-axis: `signup_month` (Month).
   - Y-axis: `COUNTD(customer_id)`.
   - Y-axis title: “Number of Customers”.

---

## 9. Filters & Interactivity

- **Region Filter**
  - Type: multi-select list.
  - Applies to: MRR by Plan, Churn Rate by Plan, Customers by Region, Signups by Month.
  - Default: all regions selected.

- **Tooltips**
  - Clean, business-friendly tooltips showing:
    - Plan type / Region / Month
    - Metric value (MRR, churn rate, or number of customers)

- **Interaction Behaviour**
  - Dashboard should recalculate charts as filters change without noticeable delay.

---

## 10. Non-functional Requirements

- The dashboard should load and update in **a few seconds** on a typical analyst laptop.
- Layout should be optimized for **desktop/laptop** viewing.
- Colours and fonts should be consistent and easy to read.

---

## 11. Deliverables

- `tableau/saas_revenue_churn.twbx` – Tableau dashboard.
- `data/saas_customers.xlsx` – simulated SaaS dataset.
- `docs/BRD_saas_revenue_churn_dashboard.md` – this document.
- `docs/case_study_saas_revenue_churn.md` – written case study with findings and recommendations.
- `README.md` – project overview for GitHub.

---

## 12. Success Criteria

This dashboard will be considered successful if:

- Stakeholders can answer core questions (e.g., “Which plan has the highest churn?”)
  in **under one minute** using the dashboard.
- Churn drivers by plan type and high-level signup seasonality are clearly visible.
- The artefacts (BRD, Tableau dashboard, case study) can be used as a standalone
  analytical story in a business analytics portfolio.
