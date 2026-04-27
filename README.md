# VPD Surveillance Dashboard: Vaccine-Preventable Disease Incidence in Yemen (2024–2025)

Interactive flexdashboard exploring how **disruptions in routine immunization** during active conflict affected **vaccine-preventable disease (VPD) incidence** across four CARE-supported governorates in Yemen between 2024 and 2025.

**Live Dashboard:**
https://Akanshya1998.github.io/DATA555_Dashboard/

---

## Why This Matters

Vaccine-preventable diseases are surging across CARE-supported governorates in Yemen, with Lahj recording a 950% increase in VPD cases between 2024 and 2025, directly linked to documented gaps in routine immunization service delivery during active conflict. Restoring EPI outreach and strengthening cold-chain infrastructure in disrupted districts is a measurable, cost-effective public health priority for humanitarian actors operating in Yemen.

---

## 1. Background & Research Question

- Postpartum and conflict-related disruptions to health systems in Yemen have severely impacted routine immunization coverage across multiple governorates.
- CARE's OPD (Outpatient Department) surveillance system tracks new cases of vaccine-preventable diseases monthly across health facilities in Abyan, Aden, Ad'Dhale, and Lahj.
- VPDs including Measles, Pertussis, Typhoid Fever, Mumps, Chickenpox, and Hepatitis are all preventable through routine EPI vaccination — yet case counts have risen sharply between 2024 and 2025 across most governorates.
- The EPI (Expanded Programme on Immunization) records vaccination doses administered monthly, allowing comparison of immunization coverage with disease outcomes.

This dashboard asks:

> **How were disruptions in routine immunization associated with changes in reported vaccine-preventable disease incidence in CARE-supported districts in Yemen between 2024 and 2025?**

---

## 2. Overview of the Dashboard

The dashboard is built as a **flexdashboard** (R Markdown) with three tabs and three interactive widgets:

### Tab 1 — Dashboard
- **4 KPI value boxes:** total 2024 cases, total 2025 cases, Lahj % increase, governorates monitored
- **Widget 1A — Monthly VPD Trends by Governorate (line chart):**
  - X-axis: month; Y-axis: new VPD cases (count)
  - One coloured line per governorate (Abyan, Aden, Ad'Dhale, Lahj)
  - Dropdown to switch between **2024** and **2025** — one year shown at a time
  - Hover tooltip: governorate, month, year, case count
- **Widget 1B — 2024 vs 2025 Monthly Cases (grouped bar chart):**
  - X-axis: month; Y-axis: new VPD cases (count)
  - Two bars per month: blue = 2024, red = 2025
  - Dropdown to select **one governorate** at a time
  - Hover tooltip: governorate, month, year, case count

### Tab 2 — Disease Table & Vaccination
- **Widget 2 — Interactive Disease Table (DT):**
  - Searchable and sortable table of new VPD cases by governorate and disease
  - Columns: Governorate, Disease, 2024 Cases, 2025 Cases, Change, % Change
  - Colour-coded Change column (red = increase, green = decrease)
  - Blue bar background in 2025 Cases column for quick magnitude comparison
  - Hover tooltip on every cell shows column name and value
- **Widget 3 — Measles Doses vs Measles Cases (grouped bar chart):**
  - Solid bars = vaccination doses administered; faded bars = cases reported
  - 2024 (blue) and 2025 (red) shown side by side per governorate
  - Hover tooltip: doses administered or cases reported, governorate, year

### Tab 3 — About the Data
- Full dataset description: source, collection method, study population, time period, sample size
- Key variables table, important limitations, R packages used

---

## 3. Data & Sources

### 3.1 Dataset
- **Source:** CARE Yemen internal OPD (Outpatient Department) surveillance records and EPI (Expanded Programme on Immunization) monthly data entry sheets
- **Confidentiality:** This dataset is **confidential** and not publicly available; shared under a data-use agreement for academic research purposes only
- **All data is embedded directly in `index.Rmd`** — no external data files are required to run the dashboard

### 3.2 Study Population
Patients presenting to CARE-supported health facilities in four governorates of Yemen — **Abyan, Aden, Ad'Dhale, and Lahj** — with symptoms of vaccine-preventable diseases including Typhoid Fever, Measles, Chickenpox, Mumps, Hepatitis A, Hepatitis B, Pertussis, Rubella, and Meningitis.

### 3.3 Time Period
**April 2024 through September 2025.** January–March 2024 and October–December 2025 are excluded from trend analyses due to incomplete surveillance data availability.

### 3.4 Sample Size
498 new VPD case records across 25 governorate–disease combinations; monthly trend charts cover 51 data points across four governorates.

---

## 4. Key Variables

| Variable | Type | Description |
|----------|------|-------------|
| New VPD Cases | Count | Monthly new VPD patients at CARE OPD facilities |
| Governorate | Categorical | Administrative unit: Abyan, Aden, Ad'Dhale, or Lahj |
| Year | Categorical | 2024 or 2025 |
| Month | Ordered categorical | January through December |
| Disease | Categorical | Typhoid, Measles, Chickenpox, Mumps, Hepatitis A/B, Pertussis, Rubella, Meningitis |
| Measles Doses | Count | Measles 1st + 2nd dose administered per governorate (EPI records) |
| Change | Count | Difference in cases: 2025 minus 2024 |
| % Change | Numeric | Percentage change from 2024 to 2025 |

---

## 5. Code Structure

```
DATA555_Dashboard/
├── index.Rmd       ← R Markdown source (knit to produce index.html)
├── index.html      ← Rendered flexdashboard (served by GitHub Pages)
└── README.md       ← This file
```

The dashboard uses a single self-contained `index.Rmd` file. All data, code, and styling are embedded. No `global.R`, `server.R`, or `ui.R` files are needed — flexdashboard is a static HTML output, not a Shiny app.

---

## 6. Design Decisions

Two key design choices were made based on data visualization principles:

- **Widgets 1A and 1B are split into two separate charts** rather than one combined chart. Putting all four governorates and both years on one chart required users to simultaneously track colour (governorate) and line style (year), creating high cognitive load. Separating them means each chart encodes only one comparison dimension at a time.
- **No vertical axis labels or rotated text** appear anywhere in the dashboard. The interactive DT table uses horizontal column headers and on-hover tooltips to deliver label information, reducing visual clutter and improving readability on both desktop and mobile screens.

---

## 7. How to Run Locally

1. **Clone the repository:**
```bash
git clone https://github.com/Akanshya1998/DATA555_Dashboard.git
cd DATA555_Dashboard
```

2. **Install required R packages:**
```r
install.packages(c("flexdashboard", "plotly", "DT", "tidyverse", "htmltools"))
```

3. **Open `index.Rmd` in RStudio and click Knit.**
   This produces `index.html` which opens in your browser.

---

## 8. R Packages Used

| Package | Purpose |
|---------|---------|
| `flexdashboard` | Dashboard layout, tabs, and value boxes |
| `plotly` | Interactive line charts, bar charts, dropdown menus, and tooltips |
| `DT` | Interactive searchable and sortable disease table |
| `tidyverse` | Data wrangling and transformation |
| `htmltools` | Custom HTML content in the About the Data tab |

---

## 9. Limitations

- Surveillance data are **passive** — true case counts are likely underreported due to access constraints in conflict-affected areas.
- Abyan and Aden show zero cases from April–September 2025, which may reflect **data collection gaps** rather than true zero incidence.
- The measles dose–case relationship shown in Widget 3 is **descriptive, not causal** — displacement, population immunity gaps, and healthcare access barriers also affect incidence.
- Population denominators are unavailable, so **incidence rates** (cases per 1,000 population) cannot be calculated from this dataset.
- Surveillance coverage varies across governorates (e.g., Ad'Dhale has data from April 2024 while Lahj only from November 2024), limiting direct cross-governorate comparisons in 2024.

---

## Contact

**Author:** Akanshya Dash
**Course:** DATA 555 — Current Topics in Data Science
**Institution:** Rollins School of Public Health, Emory University | Spring 2026

For questions or issues, please open an issue on this GitHub repository.

---

## License
This project is for educational purposes as part of the DATA 555 coursework.
