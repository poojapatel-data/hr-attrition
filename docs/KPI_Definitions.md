# KPI Definitions

`data/HR_Employee_Attrition_Data.xlsx` → **kpis** sheet (slice-aware where linked to pivots/GETPIVOTDATA).

<br>

| KPI | Business Meaning | Formula |
|---|---|---|
| **Headcount** | Total active employees | `=COUNTA(attrition_data[EmployeeId])` |
| **Attritions** | # employees with Attrition = "Yes" | `=SUM(attrition_data[AttritionFlag])` |
| **Attrition Rate** | % employees who left | `=Attritions / Headcount` *(or pivot % of row total)* |
| **Total Attrition Cost** | Realized replacement cost for leavers | `=SUM(attrition_data[AttritionCost])` |
| **Avg. Replacement Cost per Attrition** | Mean replacement cost per leaver | `=IFERROR(Replacement Cost Exposure/Attritions,0)` |
| **Avg Tenure (years)** | Average YearsAtCompany | `=AVERAGE(attrition_data[YearsAtCompany])` |
| **Avg Satisfaction Index** | Mean of satisfaction drivers (Env, Job, Relationship, WLB) | `=AVERAGE(attrition_data[SatisfactionIndex])` |
| **Overtime Share** | % of workforce with OverTime = "Yes" | `=COUNTIFS(attrition_data[OverTime], "Yes") / ROWS(attrition_data[EmployeeId])` |
| **Early Career Workforce (CareerStage)** | Share of employees tagged Early Career | `=COUNTIFS(attrition_data[CareerStage], "Early Career") / ROWS(attrition_data[EmployeeId])` |
| **New-Hire Attrition Rate** | Attrition within EmploymentStage = New Hires | `=IFERROR(SUMIFS(attrition_data[AttritionFlag], attrition_data[EmploymentStage], "New Hires") / COUNTIFS(attrition_data[EmploymentStage], "New Hires"),0)` |
| **OverTime Attrition Rate** | Attrition rate among OverTime = Yes | `=IFERROR(SUMIFS(attrition_data[AttritionFlag], attrition_data[OverTime], "Yes") / COUNTIFS(attrition_data[OverTime], "Yes"),  0)` |
| **OverTime risk delta (percentage points)** | OT=Yes rate minus OT=No rate | `=100*(GETPIVOTDATA("Attrition Rate", charts!$A$19, "Overtime", "Yes") - GETPIVOTDATA("Attrition Rate", charts!$A$19, "Overtime", "No")) |
| **Long-Commute Attrition Rate** | Attrition where DistanceFromHome ≥ 20 km | `=IFERROR(SUMIFS(attrition_data[AttritionFlag], attrition_data[CommuteRange], "20+ km") / COUNTIFS(attrition_data[CommuteRange], "20+ km"),0)` |
| **Low-Income Attrition Rate** | Attrition in IncomeGroup = Low | `=IFERROR(SUMIFS(attrition_data[AttritionFlag], attrition_data[IncomeGroup], "Low Income") / COUNTIFS(attrition_data[IncomeGroup], "Low Income"),0)` |
| **Manager-Instability Attrition Rate** | Attrition where ManagerStability = Unstable | `=IFERROR(SUMIFS(attrition_data[AttritionFlag], attrition_data[ManagerStability], 0) /COUNTIFS(attrition_data[ManagerStability],0),0)` |
| **Median Income — Leavers** | Median MonthlyIncome of leavers | `=MEDIAN( FILTER(attrition_data[MonthlyIncome], attrition_data[AttritionFlag]=1) )` *(array / dynamic formula)* |
| **Median Income — Stayers** | Median MonthlyIncome of stayers | `=MEDIAN( FILTER(attrition_data[MonthlyIncome], attrition_data[AttritionFlag]=0) )` *(array / dynamic formula)* |
| **Pay Gap %** | Median(leavers) vs median(stayers) | `=IFERROR( Median Income – Leavers/Median Income – Stayers - 1, 0 ) |
| **Replacement Cost Exposure** | Exposure for current leavers (same as Total Attrition Cost in snapshot) | `=SUMIFS(attrition_data[ReplacementCost], attrition_data[Attrition], "Yes")` |
| **Top Cost Department** | Department with highest realized attrition cost | `=analysis!(top label cell)` *(From “Top Cost by Department” pivot: reference top label cell)* |
| **Top Cost Department (Value)** | Cost value for that department | `=GETPIVOTDATA("ReplacementCost", analysis!(top-left pivot cell), "Department", analysis!(top label cell)`  *(From “Top Cost by Department” pivot)* |

