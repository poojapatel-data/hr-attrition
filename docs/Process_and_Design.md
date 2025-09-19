# Process & Design 

> **Workbook:** `data/HR_Employee_Attrition_Data.xlsx`  
> **Sheets (typical):** `attrition_data` (base), `kpis`, `analysis` (pivots), `charts` (chart pivots), `params`, `dashboard`  
> **Table name:** `data_employees` (base table)  
> **SelectedFactor in `params`:** **0.3 (Conservative)** → `ReplacementCost = 3.6 × MonthlyIncome`

---

## 1) Data Cleaning & Preparation (Power Query)

1. **Import & Promote Headers** from the Kaggle IBM HR dataset.
2. **Tidy text** (all text columns): `Transform → Format → Trim`, then `Clean`.
3. **Set data types**  
   - **Text:** `EmployeeId`, `Department`, `JobRole`, `BusinessTravel`, `Gender`, `OverTime`, etc.  
   - **Whole/Decimal:** `Age`, `MonthlyIncome`, `DistanceFromHome`, all `Years*` fields, satisfaction/ratings (scales 1–4).
4. **Remove duplicates** to ensure **one row per employee snapshot** (dedupe on `EmployeeId`).
5. **Drop noise/constant columns**  
   - Constants: `EmployeeCount`, `Over18`, `StandardHours`  
   - Synthetic rates: `MonthlyRate`, `HourlyRate`, `DailyRate`  
6. **Categorical standardization** (consistent, analysis-friendly tokens)  
   - `BusinessTravel` → `Non-Travel`, `Travel_Rarely`, `Travel_Frequently`  
   - `Gender` → `Male`, `Female`  
   - `OverTime` → `Yes`, `No`  
   - `Department` → `Sales`, `Research & Development`, `Human Resources` (unified spelling)
7. **Range & logic checks** (log exceptions if found)  
   - **Numeric sanity:** `MonthlyIncome > 0`, `DistanceFromHome ≥ 0`, `Age ∈ [18,65]`  
   - **Ordinal bounds:** `Education 1–5`, `PerformanceRating 1–4`, `StockOptionLevel 0–3`, all satisfaction scales `1–4`  
   - **Logical consistency:**  
     `YearsSinceLastPromotion ≤ YearsAtCompany`  
     `YearsWithCurrManager ≤ YearsAtCompany`  
     `TotalWorkingYears ≥ YearsAtCompany`
   
---

## 2) Engineered Fields

 Implemented in Power Query as helper columns in Excel.

- **AgeGroup** from `Age`: `<25`, `25–34`, `35–44`, `45–54`, `55–60`  
- **CommuteRange** from `DistanceFromHome`: `≤5`, `6–10`, `11–15`, `16–20`, `20+` km  
- **IncomeGroup** from `MonthlyIncome`: `Low`, `Lower-Middle`, `Upper-Middle`, `High` *(thresholds based on distribution; list in DataDictionary)*  
- **CareerStage** from `TotalWorkingYears`: `Early Career`, `Early-Mid`, `Mid`, `Experienced`, `Senior`  
- **EmploymentStage** from `YearsAtCompany`: `New Hires`, `Early Career`, `Established`, `Experienced`, `Veterans`  
- **SatisfactionIndex** = AVERAGE of (`EnvironmentSatisfaction`,`JobSatisfaction`,`RelationshipSatisfaction`,`WorkLifeBalance`)  
- **SatisfactionLevel** bucketed from `SatisfactionIndex`: `Very Low`, `Low`, `Medium`, `High`, `Very High` *(bin edges in DataDictionary)*  
- **RecentPromotion**: 1 if `YearsSinceLastPromotion ≤ 1`, else 0  
- **ManagerStability**: `Stable` if `YearsWithCurrManager ≥ 1`, else `Unstable`  
- **OverTimeFlag**: 1 if `OverTime="Yes"` else 0  
- **AttritionFlag**: 1 if `Attrition="Yes"` else 0  

<br>

**Load to Excel** as table **data_employees**  on `attrition_data`.
   
> Full code lists + thresholds are documented in `docs/DataDictionary.md`.

---

## 3) Params (governance) & Cost/Risk models

### Params (in `params` sheet)
- `SelectedFactor = 0.30` (**Conservative**)  
- `LongCommuteKm = 20`  
- `LowSatMax = 2`

### Cost model (Excel)
- `ReplacementCost = MonthlyIncome * 12 * SelectedFactor`  
  → with `SelectedFactor = 0.30`, this equals **`3.6 × MonthlyIncome`**
- `AttritionCost = AttritionFlag * ReplacementCost`

### Risk model (Excel)
- `RiskScore` = sum of 5 simple rules (1 point each):  
  1) `OverTime = "Yes"`  
  2) `YearsAtCompany ≤ 2`  
  3) `SatisfactionLevel ∈ {"Very Low","Low"}` *(or SatisfactionIndex ≤ LowSatMax)*  
  4) `DistanceFromHome ≥ LongCommuteKm`  
  5) `YearsSinceLastPromotion ≥ 3`
- `RiskTier` = quartiles of `RiskScore` → `Q1 (Lowest)` … `Q4 (Highest)`

---

## 4) KPI Design

All KPI logic and exact formulas are centralized in **`docs/KPI_Definitions.md`**.  
This section only covers placement and wiring for the dashboard.

- Location: **kpis** sheet (each KPI in a dedicated cell with a **named range**)
- Binding: Dashboard cards reference those named ranges
- Slice-awareness: Where required, KPI cells pull from pivot cells via **GETPIVOTDATA** so slicers affect them
- Labels used on the dashboard: Headcount, Attritions, Attrition Rate, Total Attrition Cost, Avg. Replacement Cost per Attrition, OverTime Attrition Rate, OverTime risk delta (pp), New-Hire Attrition Rate

> For formulas, thresholds, and assumptions (e.g., `SelectedFactor`), see **`docs/KPI_Definitions.md`**.

---

## 5) Analysis Pivots & Slicers

Build pivots on `analysis` (tables) and `charts` (chart-friendly copies).

**Core pivots (connect slicers to all):**
- **Attrition % by**: Department, JobRole, OverTime, AgeGroup, EmploymentStage, IncomeGroup, CommuteRange, SatisfactionLevel, RecentPromotion, ManagerStability, CareerStage, RiskTier  
- **Cost by**: Department (Total Attrition Cost), JobRole (Total Attrition Cost)

**Slicers:** Department, JobRole, OverTime, AgeGroup, IncomeGroup, CommuteRange, SatisfactionLevel, EmploymentStage, CareerStage  
> In Excel: **Right-click Slicer → Report Connections…** and tick each pivot above.

---

## 6) Dashboard Layout & Binding

**Top row (8 KPI cards):**  
- **Headcount**, **Attritions**, **Attrition Rate**, **Total Attrition Cost**,  
- **Replacement Cost Exposure** *(same as Total Attrition Cost for this snapshot)*,  
- **Avg. Replacement Cost per Attrition**, **OverTime Attrition Rate**, **New-Hire Attrition Rate**

**Charts:** 
- **Workforce & Cost (KPI overview)**
- **Core Drivers** — Department, JobRole, OverTime
- **Lifecycle & Experience** — AgeGroup, EmploymentStage, SatisfactionLevel
- **Economic Impact** — Total Attrition Cost by JobRole & Department

**Shape binding:**  
- ** Each card is a shape whose text references a named cell.

---

## 7) Exporting Images

From each chart: **Right-click → Save as Picture…** (or **Copy → Picture…**) → save to `images/` with descriptive names used in `README.md` (e.g., `attrition_by_department.png`, `overtime_x_department.png`, `replacement_by_jobrole.png`).

---

## 8) Validation & QA

- **Totals:** `Headcount` equals pivot grand total; `Attritions` equals `COUNTIFS([Attrition],"Yes")`
- **Rates:** Spot-check segment rates via `COUNTIFS/COUNTIF` against the pivot values
- **Costs:** `SUM(attrition_data[AttritionCost])` equals cost pivot total; role vs department totals reconcile within rounding
- **Slicer sync:** Toggle a slicer and confirm **all** connected pivots and KPI cells update

---

## 9) Refresh Instructions

1. Append/replace rows in `attrition_data` (same columns).  
2. **Data → Refresh All** (Power Query → Pivots → Charts).  
3. Re-export any changed visuals to `images/`.  
4. To change replacement-cost assumptions, update **`params.SelectedFactor`** (e.g., 0.30 Conservative, 1.00 Aggressive).

---

## 10) Reproducibility Notes

- All engineered fields are documented (see **Engineered Fields** and `docs/DataDictionary.md`).  
- KPIs are centralized on `kpis` and use **named ranges** for shape binding.  
- Slice-awareness is achieved via **GETPIVOTDATA** links to connected pivots.  
- No macros or external add-ins required.
