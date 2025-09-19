# Case Study — HR Employee Attrition

## Objective
To understand where and why employees leave by quantifying attrition levels, identifying the most affected segments, and uncovering the key drivers (e.g., overtime, tenure stage, satisfaction, income, commute). The analysis translates these findings into the financial impact of churn and clear priorities for targeted, high-ROI retention actions and workforce planning.

<br>

## Dataset & Preparation

- **Source:** IBM HR Analytics Attrition (Kaggle; anonymized)
- **Scope:** Cross-sectional snapshot of employee demographics, job factors, and attrition label.
- **Engineered in Excel:**  
  `AgeGroup`, `IncomeGroup`, `CommuteRange`, `CareerStage`, `EmploymentStage`,  
  `SatisfactionIndex → SatisfactionLevel`, `PromotionBand`, `RecentPromotion`, `ManagerStability`,  
  `OverTimeFlag`, `AttritionFlag`, `RiskScore`, `RiskTier`
- **Modeling:** Power Query (clean/types) → Pivots/Charts → Dashboard KPIs (slice-aware)

<br>

## Executive Summary

- **Headcount:** **1470** • **Attritions:** **237** • **Attrition Rate:** **16.1%**
- **OverTime** is a strong signal: **30.5% (OT=Yes)** vs **10.4% (OT=No)** → **OverTime risk delta ~20 pp**
- **Department:** Highest **Sales (20.6%)**; lowest **R&D (13.8%)**
- **Job Role:** Highest **Sales Representative (≈39.8%)**
- **Lifecycle:** **Early Career (38.2%)**, **New Hires (34.9%)**, **Age <25 (39.2%)**
- **Rewards & Commute:** **Low Income (21.8%)** and **20+ km commute (22.1%)**
- **Total Attrition Cost:** **$4,062,773** • **Avg. Replacement Cost per Attrition:** **$17,143**
- **Economics:** Realized attrition cost **$4.08M**, avg per attrition **$17.2k**  
  Cost hotspots (leavers): **R&D $1.97M**, **Sales $1.96M**; top role **Sales Executive $1.54M**

> **Interpretation:** Overtime practices, early-tenure support, satisfaction, and commute burden are practical levers with measurable upside.

<br>

## Business Questions

1. Where is attrition concentrated (Department, JobRole, Career/Employment Stage, Age)?
2. How do **Overtime**, **Income**, **Commute**, and **Satisfaction** relate to **Attrition Rate**?
3. Which management and growth signals matter (**Manager Stability**, **Recent Promotion**)?
4. What is the **financial impact** and where should we prioritize interventions?

<br>

## Findings (with evidence)

### 1) Operational drivers
- **Overtime** strongly associated with higher attrition (**30.5% vs 10.4%**).  
- **By department**, **Sales (20.6%)** highest; **R&D (13.8%)** lowest.   
**Action:** Introduce OT guardrails (caps, rota, rest windows) in **Sales** and **R&D** first.

(../images/overtime_x_department.png), (../images/attrition_by_department.png)


### 2) Lifecycle & experience
- **CareerStage:** **Early Career** (by TotalWorkingYears) has **38.2%** attrition.
- **EmploymentStage:** **New Hires** (by YearsAtCompany) attrite at **34.9%**.  
- **AgeGroup:** **<25 attrite at 39.2%**  
**Action:** Structured onboarding (first 90 days), buddy programs, and early-skill pathways.

(../images/attrition_by_agegroup.png), (../images/attrition_by_jobrole.png)

 
### 3) Rewards & commute
- **IncomeGroup:** **Low Income 21.8%** vs **High Income 3.8%**.
- **CommuteRange:** **20+ km 22.1%** is highest.  
**Action:** Targeted comp reviews for low-income roles; flexible shifts/WFH days or commute stipends.

(../images/attrition_by_income.png), (../images/attrition_by_commute.png)

 
### 4) People experience
- **Satisfaction:** drops from **36.7% (Very Low)** to **10.2% (Very High)**.
- **Manager Stability:** Unstable **32.3%** vs Stable **12.6%**.
- **Recent Promotion:** weak protective effect (Promoted **17.0%** vs Not **14.7%**).  
**Action:** Manager coaching + pulse checks; recognition programs beyond promotions.

(../images/attrition_by_satisfaction.png), (../images/attrition_by_manager.png)
 

### 5) Economic impact & prioritization
- **Total Attrition Cost:** **$4,062,773**  
- **Avg. Replacement Cost per Attrition:** **$17,143**  
- **By department (leavers):** R&D **$1.97M**, Sales **$1.96M**.  
- **By role (leavers):** Sales Executive **$1.54M**, Lab Technician **$0.65M**.
**Action:** Focus retention spend on highest-cost roles/departments; set 90-day reduction targets, reallocate quarterly by ROI.
  
(../images/replacement_by_jobrole.png), (../images/replacement_by_department.png)
 

### 6) Risk tiers
- **RiskTier:** Q4 (Highest) **44.1%** vs Q1 (Lowest) **5.1%**.
**Action:** Trigger Q4 rapid-response (manager 1:1s, OT fixes, quick recognition) with 30-day pulses.
  
(../images/attrition_by_risktier.png)

<br>

## Recommendations (measurable)

1. **OverTime discipline** in Sales & R&D  
   - Caps, rotation, and recovery windows; monitor after 60/90 days.  
   - **Target:** reduce **OverTime risk delta** by **3–5 pp**.

2. **Early-tenure program** (New Hires & Early Career)  
   - Structured 90-day onboarding; buddy program for **New Hires / Early Career**; clear skill pathway.  
   - **Target:** cut Early Career attrition to **<30%**.

3. **Manager stability & capability**  
   - Flag teams with `YearsWithCurrManager < 1`; coaching, 1:1 cadence, skip-levels.  
   - **Target:** close gap vs stable teams by **≥5 pp**.

4. **Income/commute interventions**  
   - Comp review for **Low Income** roles, targeted pay adjustments; flexible schedules or partial WFH for **20+ km**.  
   - **Target:** reduce cohort attrition by **≥3 pp**.

5. **Satisfaction lift**  
   - Focus groups where satisfaction is **Very Low/Low**; quick wins on workload, tooling, and recognition.  
   - **Target:** move ≥15% of employees one bucket up within 90 days.

<br>

## Limitations

- Cross-sectional snapshot; correlations ≠ causation.  
- Synthetic income—use for **relative** comparisons only.

<br>

## Next Steps

- Add **exit reasons** and **time-series refresh**.  
- Build an **early-warning score** combining OT, satisfaction, tenure, commute.
