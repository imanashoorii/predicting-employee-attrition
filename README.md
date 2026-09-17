# Predicting Employee Attrition - An HR Data Analytics Case Study

An end-to-end data analytics case study that identifies why employees leave a company and delivers actionable, data-backed recommendations for HR. Built following Google's **Ask → Prepare → Process → Analyze → Share** framework.

📊 **[View the full presentation](./HR_Attrition_Case_Study.pptx)**

---

## Business Task

Understand why employees leave the company and identify the factors driving attrition, so HR can design targeted, preventive retention programs.

- **Audience:** HR leadership (non-technical)
- **Success criteria:** Identify at least 3 key drivers of attrition and deliver 2-3 concrete, actionable recommendations

## Dataset

- **Source:** [HR Data for Analytics - Kaggle](https://www.kaggle.com/jacksonchou/hr-data-for-analytics)
- **Size:** 14,999 employee records, 10 features
- **Target variable:** `left` (1 = employee exited, 0 = employee stayed)
- **Features:** satisfaction level, last performance evaluation, number of projects, average monthly hours, tenure, work accidents, promotions in the last 5 years, department, salary bracket

> ⚠️ This is a public/simulated dataset, not a real company's HR system. The findings demonstrate the analytical method rather than describing any specific organization.

## Methodology

| Phase | What was done |
|---|---|
| **Ask** | Defined the business task, audience, and success metric before touching the data |
| **Prepare** | Assessed the dataset against the ROCCC framework (Reliable, Original, Comprehensive, Current, Cited) |
| **Process** | Removed 3,008 duplicate records (20% of the dataset), renamed ambiguous columns, cast `salary` as an ordered category |
| **Analyze** | Exploratory data analysis (grouped comparisons, correlation analysis) plus a logistic regression model to predict at-risk employees |
| **Share** | Findings and recommendations packaged into a stakeholder-ready presentation |

Cleaning the data mattered: the raw attrition rate was **23.8%**, but 20% of records were exact duplicates. After removing them, the true baseline attrition rate is **16.6%**.

## Key Findings

**1. Pay determines who stays.** Employees in the low salary bracket leave at **20.5%**, versus **4.8%** for high earners - more than a 4x gap. Employees without a promotion in the last 5 years leave at 16.8% vs. 3.9% for those promoted.

**2. Workload has a sweet spot, not a straight line.** Attrition follows a U-shaped curve across number of concurrent projects: employees with 2 projects (54.2%) or 6-7 projects (up to 100%) leave far more than those with a balanced 3-5 projects (1-15%).

**3. Job satisfaction is the single strongest signal.** It shows the strongest correlation with attrition of any variable in the dataset (r = -0.35) - stronger than pay, tenure, or workload alone. Satisfaction bottoms out around year 3-4 of tenure, coinciding with a near-total absence of promotions (only 2.1% of employees were promoted in the last 5 years).

## Predictive Model

A **logistic regression** model was trained (class-balanced, 75/25 train-test split) to flag employees likely to leave.

| Metric | Baseline model | Class-balanced model |
|---|---|---|
| Accuracy | 83.4% | 77.8% |
| Recall (catching true leavers) | 18.5% | **81.9%** |
| F1 Score | 0.27 | 0.55 |

The model was deliberately tuned for **recall over raw accuracy**: for this use case, missing an employee who is about to leave is far more costly than a false alarm. Because the model is linear, it doesn't fully capture the U-shaped workload effect found in EDA - a good candidate for a follow-up tree-based model (see Next Steps).

## Recommendations

1. **Balance workload** - standardize a range of 3–5 concurrent projects per employee, with quarterly workload reviews to catch over- and under-loaded staff.
2. **Close the pay gap** - review compensation for the low salary bracket, prioritizing high performers most at risk of leaving for better-paying offers.
3. **Build visible career paths** - introduce promotion checkpoints at year 2 and 3 of tenure, ahead of the observed satisfaction dip.

## Limitations

- No external salary benchmark - pay is only known as Low/Medium/High, not against market rates
- No manager-level data - workload can't be attributed to specific managers or teams
- Logistic regression assumes linear effects and underrepresents non-linear patterns like the U-shaped workload relationship
- Tuning for recall increases false positives - roughly 1 in 3 flagged employees will not actually leave

## Tech Stack

- **Python** - pandas, matplotlib, seaborn, scikit-learn
- **Jupyter Notebook** for analysis
- **PowerPoint** for the final stakeholder presentation

## Repository Structure

```
├── HR_Attrition_Case_Study.csv
├── HR_Attrition_Case_Study.ipynb   # full analysis: cleaning, EDA, modeling
├── HR_Attrition_Case_Study.pptx    # final stakeholder presentation
└── README.md
```

## Next Steps

- Test tree-based models (Random Forest, Gradient Boosting) to capture non-linear relationships such as the workload U-curve
- Incorporate external salary benchmarking data
- Validate findings against a second, independent HR dataset

---

**Author:** Iman Ashoori
Data Analytics project · September 2026