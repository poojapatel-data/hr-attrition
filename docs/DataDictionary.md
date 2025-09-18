# Data Dictionary

This file documents all fields used in the project—both **raw source columns** from the IBM HR sample dataset and **engineered columns** created in Power Query in Excel.

### Notes
- **Raw columns** come from the IBM HR sample dataset.
- **Engineered columns** were created in Power Query/Excel for analysis and dashboards.
- **Ordinal scales** (1–4 / 1–5) are summarized in **Code Lists** at the end.
- **Dropped fields** (constant/unused) are listed at the end with reasons.
<br>

### A) Raw Columns (retained)
| Column                     | Type            | Definition                                                          | Example           |
| -------------------------- | --------------- | ------------------------------------------------------------------- | ----------------- |
| `EmployeeNumber`           | Integer         | Unique employee identifier.                                         | `101`             |
| `Age`                      | Integer (years) | Employee age.                                                       | `41`              |
| `Gender`                   | Categorical     | Gender.                                                             | `Female`          |
| `MaritalStatus`            | Categorical     | Marital status.                                                     | `Single`          |
| `Department`               | Categorical     | Department/Function.                                                | `Sales`           |
| `JobRole`                  | Categorical     | Specific role/title.                                                | `Sales Executive` |
| `JobLevel`                 | Ordinal (1–5)   | Hierarchical level (1=Entry, 5=Exec).                               | `2`               |
| `JobInvolvement`           | Ordinal (1–4)   | Perceived involvement in job.                                       | `3`               |
| `EnvironmentSatisfaction`  | Ordinal (1–4)   | Satisfaction with workplace environment.                            | `2`               |
| `JobSatisfaction`          | Ordinal (1–4)   | Satisfaction with job.                                              | `4`               |
| `RelationshipSatisfaction` | Ordinal (1–4)   | Satisfaction with collegial relationships.                          | `1`               |
| `WorkLifeBalance`          | Ordinal (1–4)   | Perceived work–life balance.                                        | `3`               |
| `BusinessTravel`           | Categorical     | Business travel frequency.                                          | `Travel_Rarely`   |
| `DistanceFromHome`         | Integer (km)    | One-way commute distance.                                           | `7`               |
| `MonthlyIncome`            | Integer         | Monthly pay (synthetic values in this dataset; used comparatively). | `5993`            |
| `PercentSalaryHike`        | Integer (%)     | Last salary hike percent.                                           | `11`              |
| `StockOptionLevel`         | Ordinal (0–3)   | Stock option level.                                                 | `0`               |
| `TotalWorkingYears`        | Integer (years) | Total career experience.                                            | `8`               |
| `YearsAtCompany`           | Integer (years) | Tenure at the company.                                              | `6`               |
| `YearsInCurrentRole`       | Integer (years) | Years in current role.                                              | `4`               |
| `YearsSinceLastPromotion`  | Integer (years) | Time since last promotion.                                          | `0`               |
| `YearsWithCurrManager`     | Integer (years) | Years under current manager.                                        | `5`               |
| `NumCompaniesWorked`       | Integer         | Prior employers count.                                              | `3`               |
| `OverTime`                 | Yes/No          | Works overtime.                                                     | `Yes`             |
| `PerformanceRating`        | Ordinal (1–4)   | Performance score.      | `3`               |
| `TrainingTimesLastYear`    | Integer         | Courses attended last year.                                         | `2`               |
| `Education`                | Ordinal (1–5)   | Highest education level.                                            | `3`               |
| `EducationField`           | Categorical     | Field of study.                                                     | `Life Sciences`   |
| `Attrition`                | Yes/No          | Whether the employee left.                                          | `Yes`             |

<br>

### B) Engineered Columns (created for analysis)
| Column              | Type          | How it’s computed                                                                                                                   | Example        |
| ------------------- | ------------- | ----------------------------------------------------------------------------------------------------------------------------------- | -------------- |
| `AttritionFlag`     | 0/1           | 1 if `Attrition = "Yes"`, else 0.                                                                                                   | `1`            |
| `OverTimeFlag`      | 0/1           | 1 if `OverTime = "Yes"`, else 0.                                                                                                    | `1`            |
| `EarlyCareer`       | 0/1           | 1 if `TotalWorkingYears ≤ 3`, else 0.                                                                                               | `0`            |
| `RecentPromotion`   | 0/1           | 1 if `YearsSinceLastPromotion ≤ 1`, else 0.                                                                                         | `1`            |
| `ManagerStability`  | 0/1           | 1 if `YearsWithCurrManager ≥ 1`, else 0.                                                                                            | `1`            |
| `AgeGroup`          | Categorical   | Bands from `Age` (e.g., `18–24`, `25–34`, `35–44`, `45–54`, `55–60`).                                                               | `35–44`        |
| `CommuteRange`      | Categorical   | Bands from `DistanceFromHome` (`≤5 km`, `6–10 km`, `11–15 km`, `16–20 km`, `20+ km`).                                               | `≤5 km`        |
| `IncomeGroup`       | Categorical   | Brackets from `MonthlyIncome` (e.g., `Low`, `Lower-Middle`, `Upper-Middle`, `High`).                                                | `Lower-Middle` |
| `EmploymentStage`   | Categorical   | Tenure stage from `YearsAtCompany` (`New Hires`, `Early Career`, `Established`, `Experienced`, `Veterans`).                         | `Established`  |
| `CareerStage`       | Categorical   | Career stage from `TotalWorkingYears` (5-range version: `Early Career`, `Early-Mid`, `Mid`, `Experienced`, `Senior`).               | `Mid`          |
| `SatisfactionIndex` | Decimal (1–4) | Average of `EnvironmentSatisfaction`, `JobSatisfaction`, `RelationshipSatisfaction`, `WorkLifeBalance`.                             | `2.75`         |
| `SatisfactionLevel` | Categorical   | Bands from `SatisfactionIndex` (5-range: `Very Low` 1.0–1.5, `Low` 1.6–2.0, `Medium` 2.1–2.5, `High` 2.6–3.0, `Very High` 3.1–4.0). | `High`         |

<br>

### C) Raw Columns (dropped during cleaning)
| Column                                   | Reason dropped                                                   |
| ---------------------------------------- | ---------------------------------------------------------------- |
| `EmployeeCount`                          | Constant = 1 (no information).                                   |
| `Over18`                                 | Constant = "Y" (all employees are adults).                       |
| `StandardHours`                          | Constant (e.g., 80) — no variance.                               |
| `HourlyRate`, `DailyRate`, `MonthlyRate` | Redundant with `MonthlyIncome` and not used in analysis/visuals. |

<br>

### D) Code Lists (for ordinal scales)

> These fields are **ordinal** (ranked categories). Treat codes as ordered labels, not equal-interval numbers.

| Field                     | Code | Label        |
|--------------------------|-----:|--------------|
| **Education (1–5)**      | 1    | Below College|
|                          | 2    | College      |
|                          | 3    | Bachelor     |
|                          | 4    | Master       |
|                          | 5    | Doctor       |
| **EnvironmentSatisfaction (1–4)** | 1 | Low   |
|                          | 2    | Medium       |
|                          | 3    | High         |
|                          | 4    | Very High    |
| **JobInvolvement (1–4)** | 1    | Low          |
|                          | 2    | Medium       |
|                          | 3    | High         |
|                          | 4    | Very High    |
| **JobSatisfaction (1–4)**| 1    | Low          |
|                          | 2    | Medium       |
|                          | 3    | High         |
|                          | 4    | Very High    |
| **RelationshipSatisfaction (1–4)** | 1 | Low  |
|                          | 2    | Medium       |
|                          | 3    | High         |
|                          | 4    | Very High    |
| **WorkLifeBalance (1–4)**| 1    | Bad          |
|                          | 2    | Good         |
|                          | 3    | Better       |
|                          | 4    | Best         |
| **PerformanceRating (1–4)** | 1 | Low         |
|                          | 2    | Good         |
|                          | 3    | Excellent    |
|                          | 4    | Outstanding  |

<br>

### E) Interpretation Notes

- **MonthlyIncome** in this public sample is **synthetic**; use it **comparatively** (e.g., via `IncomeGroup`) rather than as a literal salary KPI.
- **Attrition Rate** shown in tables/charts is the **average of `AttritionFlag`** within each group (**1 = left**, **0 = stayed**).
