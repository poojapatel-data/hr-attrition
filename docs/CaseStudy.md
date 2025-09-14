# Case Study — HR Employee Attrition (Excel)

## Objective
Quantify and explain employee attrition, identify the highest-risk segments, and estimate the cost impact so HR can target high-ROI retention actions.

## Dataset
- **Source:** Kaggle — IBM HR Analytics Attrition dataset  
  https://www.kaggle.com/datasets/pavansubhasht/ibm-hr-analytics-attrition-dataset
- **Scope:** Cross-sectional snapshot of employee demographics, job factors, and attrition label.
- **Rows:** ~**1470** employees (full dataset used)
- **Target:** **Attrition** (Yes/No)
- **Preparation:** Imported into Excel; standardized data types and labels; no deletions other than trivial whitespace/format fixes.
- **Engineered fields (in Excel):** `AgeGroup`, `IncomeGroup`, `CommuteRange`, `CareerStage`, `EmploymentStage`, `SatisfactionLevel`, `RecentPromotion`, `ManagerStability`, `RiskScore`.
- **Attribution & license:** Credit to the original dataset contributors on Kaggle; refer to the Kaggle page for terms. Used here for educational/portfolio analysis.

## Executive Summary (TL;DR)
- **Attrition rate = 16.1%** (237/1470).
- **OverTime** correlates strongly with attrition (**30.5%** vs **10.4%**).
- Highest-risk slices: **Sales**, **>25**, **Low Income**, **20+ km**.
- **Manager stability** has a material effect (32.3% unstable vs 12.6% stable).
- Estimated **attrition cost** ≈ **$4,062,773** (avg **$17,143** per case).

## Business Questions & Findings

### 1) Where is attrition highest?
**By Department**  
Top rate: **Sales = 20.6%**.  
Action: Drill to job roles in this department, enforce manager stability, and review overtime policy.

**By Job Role**  
(Use your “Attrition % by Job Role” chart. Add a screenshot under `images/`.)

### 2) Is OverTime driving attrition?
**By OverTime**  
- Yes: **30.5%**  
- No: **10.4%**

**OverTime × Department**  
Sales with OverTime shows **very high** attrition (**37.5%**); R&D with OverTime **27.3%**; HR with OverTime **29.4%**.  
Action: Cap consecutive OverTime cycles, rotate shifts, and pilot fatigue recovery windows in these teams.

### 3) Which lifecycle stages are risky?
- **Career Stage:** Early Career → **38.2%**  
- **Employment Stage:** New Hires → **34.9%**  
Action: Structured onboarding for New Hires; career-pathing & mentoring for Early Career.

### 4) Do pay and commute matter?
- **Income Group:** Low Income is highest risk (**21.8%**).  
- **Commute Range:** 20+ km has highest risk (**22.1%**).  
Action: Commute stipends/remote days; targeted retention bonuses for Low Income cohort.

### 5) What about experience and recognition?
- **Satisfaction Level:** Risk falls sharply from *Very Low* (**36.7%**) to *Very High* (**10.2%**).  
- **Manager Stability:** 32.3% (unstable) vs 12.6% (stable).  
- **Recent Promotion:** Promoted **17.0%**, Not promoted **14.7%** → no clear protective effect.  
Action: Train managers; implement recognition beyond promotions (coaching, growth projects).

## Estimated Financial Impact

- **Total attrition cost:** **$4,062,773**  
- **Avg per attrition:** **$17,143**  
- **Where it concentrates:** Sales and R&D (see dashboard).

## Recommendations

1. **OverTime discipline** in Sales and R&D (rota schedules, hard caps, recovery windows).
2. **Strengthen early tenure** programs (onboarding, buddy system, career-pathing) for New Hires/Early Career.
3. **Manager capability & stability** initiatives (training, 1:1 cadence, skip-levels).
4. **Targeted retention** for Low Income & long-commute employees (stipends, flexibility).
5. **Satisfaction uplift**: quick wins on workload balance, recognition, and growth opportunities.
6. **Monitor risk** with the `RiskScore` and track post-intervention attrition monthly.

## Visuals to Include (export from Excel)

- `images/dashboard.png` — Full dashboard
- `images/attrition_by_department.png`
- `images/overtime_by_department.png`
- `images/attrition_by_agegroup.png`
- `images/attrition_by_income_commute.png`
- `images/satisfaction_manager_promotion.png`

## Limitations & Next Steps

- Cross-sectional data; causality is not guaranteed.  
- Add a **time axis** to study tenure/seasonality effects.  
- Run a **logistic regression** or decision-tree in a notebook to validate drivers found here.
