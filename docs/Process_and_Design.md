# Process & Design

## Data Cleaning & Preparation (Excel)
1. **Base sheet:** `Employee-Attriti` (1470 rows). Validated column types and blanks.
2. **Helper fields** were added (already present in your file):  
   `AgeGroup`, `IncomeGroup`, `CommuteRange`, `CareerStage`, `EmploymentStage`, `SatisfactionLevel`, `RecentPromotion`, `ManagerStability`, `RiskScore`, `AttritionFlag`, `OverTimeFlag`.
3. Verified unique employee keys (`EmployeeId`) and consistent labels (e.g., "Research & Development").

## Modeling in Excel
- **Pivot Tables** for segment analyses (Department, JobRole, OverTime, AgeGroup…).
- **Pivot Charts** for % comparisons and trends.
- **Slicers** connected to all pivots on the dashboard.
- **KPI cards** for Headcount, Attritions, Attrition %, Cost.

## Dashboard Design
- One-page dashboard with left-aligned KPIs, 2×2 chart grid, bottom matrix for **OverTime × Department**.
- Minimal colors; consistent number formats (percentages to one decimal).
- Slicers: Department, OverTime, Career Stage, Employment Stage, Satisfaction Level.

## Refresh & Maintenance
- Replace the base table with new employee data (same schema) → **Refresh All**.
- If labels change (e.g., new departments), slicers update automatically.
- Export PNGs from charts to `images/` for GitHub documentation.