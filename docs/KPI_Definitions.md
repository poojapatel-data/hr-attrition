# KPI Definitions

## Core KPIs
- **Headcount** = Count of rows in base employee table.
- **Attritions** = Count of rows where `Attrition = "Yes"`.
- **Attrition %** = `Attritions / Headcount`.

## Segment KPIs
For any categorical segment `S` (e.g., Department, JobRole, OverTime, AgeGroup, IncomeGroup, CommuteRange, CareerStage, EmploymentStage, SatisfactionLevel, RecentPromotion, ManagerStability):

- **Segment Attrition %** = `(# Attrition = "Yes" in S) / (Headcount in S)`.

Use PivotTables with `Values: Count of EmployeeId` and a calculated `AttritionFlag` (1 if "Yes" else 0) to plot percentages.

## Cost KPIs
- **ReplacementCost**: Estimated replacement cost per attrited employee (pre-calculated in the file).  
- **AttritionCost**: Per-employee cost for attrition events (pre-calculated in the file).

- **Total Attrition Cost** = `SUM(AttritionCost)` = **$4,062,773**  
- **Avg Attrition Cost (per attrition)** = `AVERAGE(AttritionCost where Attrition="Yes")` = **$17,143**

> In the workbook, costs are ready-to-use as columns. In a pure-Excel build without columns, you can add helper columns or use SUMIFS/AVERAGEIFS on `Attrition = "Yes"`.

## Feature Engineering (in your Excel file)
- **AgeGroup** (e.g., 25–34, 35–44, 45–54, 55–60, <25)
- **IncomeGroup** (Low, Lower-Middle, Upper-Middle, High)
- **CommuteRange** (≤5 km, 6–10, 11–15, 16–20, 20+)
- **CareerStage** (Early, Early-Mid, Mid, Experienced, Senior)
- **EmploymentStage** (New Hires, Early Career, Established, Experienced, Veterans)
- **SatisfactionLevel** (Very Low, Low, Medium, High, Very High)
- **RecentPromotion** (0/1 within the chosen window)
- **ManagerStability** (0/1 based on tenure/turnover rules)
- **RiskScore** (0–4 categorical score)