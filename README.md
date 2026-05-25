# End-to-End Credit Risk Analysis & Executive Dashboard

## Project Overview
This project delivers an end-to-end data analytics solution designed to evaluate portfolio risk and isolate key default drivers for a consumer lending portfolio. Utilizing a dataset of over 32,000 credit applications, I built a robust data pipeline in Python to audit, clean, and validate structural and logical anomalies. The refined data was then modeled in Power BI to create an interactive executive dashboard that surfaces compounding risk factors for underwriting teams.

### Key Business Insights
* **Macro Portfolio Health:** The portfolio represents **$306M in total allocated capital** with a baseline **Portfolio Default Rate of 21.54%**.
* **The "Dead Zone" (Compounding Risk):** Multi-dimensional matrix analysis revealed that **Low-Income applicants who Rent** exhibit a devastating default rate of **42.81%** (rising to **48.48%** for the "Other" housing category)—nearly double the portfolio baseline.
* **Risk Concentration:** **55.49% of all defaults** are heavily concentrated within the Low-Income bracket (individuals earning under \$45,000 annually).
* **Volume vs. Ratio Drivers:** While Medical loans demonstrate a high visual proportion of defaults relative to volume, **Education** and **Medical** loans combined drive the highest total volume of applications and total absolute defaults.

---

## Data Pipeline & Engineering (Python)

### 1. Structural Auditing & Data Cleaning
* **Logical Constraint Validation:** Discovered and dropped 897 structurally corrupt records where an applicant's reported employment length (`person_emp_length`) logically exceeded their biological age.
* **Outlier Mitigation:** Identified extreme anomalies in the age feature (including records showing an applicant age of 144 years). Handled these by capping extreme values at the feature median to preserve corresponding, valid financial metrics (like high-income records) without skewing statistical distributions.
* **Deduplication:** Performed granular business-logic checks for identical rows. Maintained data integrity by avoiding arbitrary row deletion in the absence of an explicit primary key.

### 2. Feature Engineering & Type Mapping
* **Income Tiering:** Segmented continuous income variables into distinct, business-aligned buckets (`Low Income: $0–$45k`, `Medium Income: $45k–$90k`, `High Income: >$90k`) using Power Query conditional logic to enable macro-composition risk tracking.
* **Categorical Encoding Strategy:** Bypassed Power BI's default numeric summation on the binary loan_status field by implementing an explicit Count aggregation. This successfully exposed the massive baseline volume of non-defaulting records (0) alongside defaults (1), preventing data suppression in stacked and clustered column layouts.

---

## Interactive Dashboard Architecture (Power BI)

The dashboard is structured around the **Z-Pattern layout layout best practices**, optimizing visual hierarchy for executive scannability:

1. **Executive Overview (Top Ribbon):** High-level summary cards exposing Total Capital Allocated ($306M) and Overall Portfolio Default Rate (21.54%) to establish immediate baseline orientation.
2. **Categorical Drivers (Left Column):** Clustered horizontal bar charts and stacked column charts tracking applications and risk profiles across housing statuses and loan purposes.
3. **Financial Concentrations (Right Column):** A filtered Donut Chart isolating the macro-composition of defaults across income tiers alongside a continuous time/rate distribution chart mapping volume clusters between 7% and 13% interest.
4. **The Standout Matrix Heatmap (Bottom Canvas):** Cross-references housing status directly against income tiers. Uses conditional formatting gradients to explicitly map risk boundaries, distinguishing the high-risk "Dead Zones" from the low-risk "Safe Havens" (<9% default probability).

---

## Technologies Used
* **Data Extraction & Engineering:** Python 3.x, Pandas, NumPy, Jupyter Notebook
* **Business Intelligence & Visualization:** Power BI Desktop, Power Query / DAX
