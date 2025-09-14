# HR Employee Attrition — Excel Analytics Project

A professionally documented **Excel-based** analysis of employee attrition using the classic HR dataset.  
This repository includes a reproducible Excel workbook, clearly defined KPIs, and an executive-ready dashboard with insights for retention strategy.

> **Tech stack:** Microsoft Excel (Pivot Tables, Pivot Charts, Slicers, Formulas).  
> **Owner:** You (Pooja Patel). **Use case:** Portfolio-quality business analytics project.

---

## 🗂️ Dataset & Source

- **Source:** Kaggle — IBM HR Analytics Attrition dataset  
  https://www.kaggle.com/datasets/pavansubhasht/ibm-hr-analytics-attrition-dataset
- **Use in this repo:** The Kaggle dataset is imported into Excel and used as the base table for all pivots, KPIs, and the dashboard. We add only lightweight cleaning and feature engineering (see `docs/Process_and_Design.md`).
- **Engineered fields:** `AgeGroup`, `IncomeGroup`, `CommuteRange`, `CareerStage`, `EmploymentStage`, `SatisfactionLevel`, `RecentPromotion`, `ManagerStability`, `RiskScore`.
- **Attribution & license:** Credit to the original dataset contributors on Kaggle. Please refer to the Kaggle page for licensing and terms of use; this project uses the data for educational/portfolio analysis.
- **Repro tip:** If you prefer starting from the Kaggle CSV, import it into Excel and ensure column names/types match the definitions in `docs/DataDictionary.md`.

---

## 📦 Repository Structure

```
.
├─ data/
│  └─ HR_Employee_Attrition.xlsx            # Final Excel with KPIs, pivots, dashboard
├─ docs/
│  ├─ CaseStudy.md                           # Business questions → analysis → insights
│  ├─ KPI_Definitions.md                     # KPI formulas, segmentation logic
│  ├─ DataDictionary.md                      # Column meanings & example values
│  └─ Process_and_Design.md                  # Cleaning steps, modeling, Excel design
├─ images/                                   # Exported PNGs from your dashboard/charts
│  ├─ dashboard.png
│  ├─ attrition_by_department.png
│  ├─ overtime_x_department.png
│  └─ ...
└─ README.md
```

> Copy your Excel file here as `data/HR_Employee_Attrition.xlsx` (keep your local filename too if you want).

---

## 🎯 Business Questions

1. **How high is attrition overall?** Which **departments** and **job roles** are most impacted?
2. Does **OverTime** correlate with higher attrition? In which departments is the overlap most severe?
3. What is the attrition pattern by **Career/Employment Stage** and **Age Group**?
4. How do **Income Group** and **Commute Range** relate to attrition risk?
5. Do **Satisfaction levels**, **Manager Stability**, and **Recent Promotion** show protective or risk signals?
6. What is the **economic impact** of attrition (replacement/attrition cost)? Where is it concentrated?

---

## 🔑 Key Results (from your final Excel)

- **Workforce size:** **1470** employees  
- **Attritions:** **237** employees → **16.1%** overall attrition rate

**Operational drivers**
- **OverTime** workers attrite at **30.5%** vs **10.4%** for non-OverTime.
- By **Department**, highest attrition rate in **Sales** (**20.6%**), followed by **Human Resources** (**19.0%**).

**Talent lifecycle**
- **Career Stage:** **Early Career** shows the highest attrition (**38.2%**).  
- **Employment Stage:** **New Hires** are most at risk (**34.9%**).  
- **Age Group:** **>25** segment shows highest attrition (**39.2%**).

**Reward & commute**
- **Income Group:** **Low Income** has the highest attrition (**21.8%**); **High Income** the lowest (**3.8%**).
- **Commute Range:** **20+ km** is most at risk (**22.1%**).

**People experience**
- **Satisfaction:** Attrition drops from **36.7%** at *Very Low* to **10.2%** at *Very High*.
- **Manager Stability:** Unstable teams show **32.3%** vs **12.6%** when stable.
- **Recent Promotion:** No clear protective effect (promoted **17.0%** vs not promoted **14.7%**).

**Economic impact**
- **Total attrition cost:** **$4,062,773**  
- **Replacement cost exposure:** **$4,084,348** (avg **$17,143** per attrition)

> See **docs/CaseStudy.md** for segment-level details and recommended actions.

---

## 📊 Dashboard (Excel)

Export these visuals to `images/` and embed them in the docs:
- Overall KPIs (Headcount, Attritions, Attrition %, Cost)
- Attrition % by **Department**
- Attrition % by **Job Role**
- **OverTime × Department** matrix
- Attrition % by **Age Group**, **Income Group**, **Commute Range**
- Attrition % by **Employment Stage** / **Career Stage**
- Attrition % by **Satisfaction Level**, **Recent Promotion**, **Manager Stability**

> Slicers: Department, Overtime, Career Stage, Employment Stage, Satisfaction Level.

---

## 🔁 How to Reproduce / Use

1. Open `data/HR_Employee_Attrition.xlsx` in Excel.
2. Review **kpis**, **Analysis**, **charts**, and **Dashboard** sheets.
3. Use slicers on the Dashboard to interactively filter segments.
4. To update: replace the base table in `Employee-Attriti` with new data (same schema) and refresh pivots.

---

## 📚 Documentation

- **CaseStudy:** Business questions → analysis → insights → actions → ROI  
- **KPI Definitions:** Exact formulas used to compute all metrics  
- **Data Dictionary:** Column descriptions and sample values  
- **Process & Design:** Cleaning, feature engineering (AgeGroup, IncomeGroup, etc.), and Excel design choices

---

## 📝 License

This project is for portfolio demonstration. If you plan to use or extend it commercially, please add an appropriate license.
