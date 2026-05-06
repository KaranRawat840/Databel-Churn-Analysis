# Databel-Churn-Analysis
# 📊 Databel Customer Churn Analysis — Power BI Case Study

![Power BI](https://img.shields.io/badge/Power%20BI-2.91.884-F2C811?style=flat&logo=powerbi&logoColor=black)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=flat)
![Pages](https://img.shields.io/badge/Report%20Pages-10-blue?style=flat)
![Dataset](https://img.shields.io/badge/Dataset-Databel%20Telecom-orange?style=flat)

> **A comprehensive end-to-end Power BI case study analysing customer churn for Databel, a fictional telecommunications company. The report explores who is churning, why they are churning, and which customer segments are most at risk.**

---

## 📋 Table of Contents

- [Project Overview](#project-overview)
- [Dataset](#dataset)
- [Report Structure](#report-structure)
- [Key Findings](#key-findings)
- [DAX Measures](#dax-measures)
- [Data Model](#data-model)
- [How to Use](#how-to-use)
- [File Structure](#file-structure)
- [Tools & Technologies](#tools--technologies)

---

## Project Overview

Customer churn — the rate at which customers stop doing business with a company — is one of the most critical metrics in the telecommunications industry. This case study uses Power BI to build an interactive, multi-page analytical report that helps stakeholders understand:

- **Who** is churning (demographics, segment, geography)
- **Why** they are churning (reasons, categories)
- **When** churn is most likely (contract age, tenure)
- **How** pricing, plans, and service quality correlate with churn

The report is structured across **10 pages**, each diving deeper into a specific dimension of churn behaviour.

---

## Dataset

| Property | Detail |
|---|---|
| **Source** | Databel — fictional telecom company |
| **Table** | `Databel - Data` |
| **Tool** | Power BI Desktop (version 2.91.884) |
| **Created From** | Power BI Cloud (Release 2026.03) |

### Fields

| Field | Description |
|---|---|
| `Customer ID` | Unique customer identifier |
| `Churn Label` | Whether the customer churned (Yes/No) |
| `Churned` | Binary flag (1/0) for churn |
| `Churn Reason` | Customer-reported reason for leaving |
| `Churn Category` | Grouped churn reason category |
| `Contract Type` | Month-to-Month, One Year, Two Year |
| `Contract Category` | Simplified contract grouping |
| `Payment Method` | Payment method used |
| `Monthly Charge` | Monthly bill amount |
| `Account Length (in months)` | Tenure in months |
| `Age (bins)` | Customer age group |
| `Gender` | Customer gender |
| `Senior` | Whether the customer is a senior |
| `Under 30` | Whether the customer is under 30 |
| `State` | US state of the customer |
| `Group` | Whether customer is part of a group plan |
| `Number of Customers in Group` | Group size |
| `Unlimited Data Plan` | Whether customer has unlimited data |
| `Intl Plan` | International calling plan status |
| `Intl Active` | Whether the customer actively uses international calls |
| `Customer Service Calls` | Number of calls to customer service |
| `Grouped Consumption` | Data consumption bucket |

### Calculated Measures

| Measure | Description |
|---|---|
| `Churn Rate` | % of customers who churned |
| `Number of Customers` | Total customer count |
| `Avg Customer Service Calls` | Average service calls per customer |
| `Avg Extra Data Charges` | Average extra data charges incurred |
| `Avg Extra International Charges` | Average extra international charges |

---

## Report Structure

The report contains **10 pages**, each focusing on a distinct analytical perspective:

### 1. 🏠 Overview
**Visuals:** 3 KPI cards, Clustered Bar Chart (Churn Reasons), Donut Chart, Pie Chart, Map

High-level snapshot of the total customer base, overall churn rate, and geographic distribution. The bar chart surfaces the top churn reasons immediately.

---

### 2. 👥 Age Groups
**Visuals:** 2× Line & Stacked Column Combo Charts, Slicer

Explores how churn rate and customer volume vary across age brackets. The slicer allows filtering by demographic segments (Senior, Under 30).

---

### 3. 💳 Payment and Contract
**Visuals:** 2 KPI Cards, Scatter Chart, Slicer

Analyses the relationship between monthly charges, payment method, contract type, and churn risk. The scatter chart highlights which payment/contract combinations have the highest churn exposure.

---

### 4. 💰 Extra Charges
**Visuals:** Clustered Bar Chart, 2 KPI Cards

Investigates whether customers paying extra data or international charges are more likely to churn, and by how much.

---

### 5. 💡 Insights
**Visuals:** 4 KPI Cards, Line Chart, Map

Synthesises key metrics into an executive summary layer with trend analysis over account tenure and geographic concentration.

---

### 6. 🗂️ Groups and Categories
**Visuals:** Line & Stacked Column Combo, Pie Chart (Churn by Category), Clustered Column Chart, Multi-Row Card, Donut Chart (Customers by Contract Type)

Deep dive into how group membership and plan categories relate to churn patterns.

---

### 7. 📊 Churn Demographics
**Visuals:** Table, Clustered Bar Chart (Churn Reasons), 3 KPI Cards, Line & Stacked Column Combo

A demographic breakdown of churned customers, cross-referenced with churn reasons and service usage.

---

### 8. 📶 Unlimited Plan
**Visuals:** Table, Clustered Bar Chart

Compares churn rates and data consumption between customers on unlimited vs. limited data plans.

---

### 9. 🌍 International Calls
**Visuals:** Pivot Table, Map

Focuses on customers with international plans — are they being charged fairly? Are inactive international plan holders more likely to churn?

---

### 10. 📄 Contract Type
**Visuals:** Custom Visual, Pie Chart, 2 Line Charts

Examines how contract length (Month-to-Month vs annual) influences churn over time.

---

## Key Findings

> ⚠️ *The following insights are inferred from the report structure and field analysis. Open the `.pbix` file for the exact figures.*

- **Month-to-Month contracts** carry significantly higher churn risk than annual contracts.
- **Senior customers** and those **under 30** show distinct churn patterns compared to the mid-age cohort.
- Customers with **high customer service call volumes** are more likely to churn — a proxy for unresolved dissatisfaction.
- Customers on **international plans who are not actively using them** represent a high-risk, addressable segment.
- **Group plan customers** tend to churn less, suggesting bundled pricing increases retention.
- **Extra charges** (data overages, international) correlate with elevated churn rates.

---

## DAX Measures

Key measures used throughout the report (see [`docs/dax-measures.md`](docs/dax-measures.md) for full definitions):

```dax
-- Churn Rate
Churn Rate = DIVIDE([Churned Customers], [Number of Customers])

-- Number of Customers
Number of Customers = COUNT('Databel - Data'[Customer ID])

-- Churned Customers
Churned Customers = CALCULATE(
    COUNT('Databel - Data'[Customer ID]),
    'Databel - Data'[Churn Label] = "Yes"
)

-- Avg Customer Service Calls
Avg Customer Service Calls = AVERAGE('Databel - Data'[Customer Service Calls])

-- Avg Extra Data Charges
Avg Extra Data Charges = AVERAGE('Databel - Data'[Avg Extra Data Charges])
```

---

## Data Model

The report uses a **single flat table** (`Databel - Data`) with no relationships — all analysis is performed directly on the denormalised dataset via DAX measures and Power BI's built-in aggregations.

```
┌─────────────────────────┐
│     Databel - Data      │
├─────────────────────────┤
│ Customer ID (PK)        │
│ Churn Label             │
│ Churned                 │
│ Churn Reason            │
│ Churn Category          │
│ Contract Type           │
│ Contract Category       │
│ Payment Method          │
│ Monthly Charge          │
│ Account Length          │
│ Age (bins)              │
│ Gender                  │
│ Senior                  │
│ Under 30                │
│ State                   │
│ Group                   │
│ Number in Group         │
│ Unlimited Data Plan     │
│ Intl Plan               │
│ Intl Active             │
│ Customer Service Calls  │
│ Grouped Consumption     │
└─────────────────────────┘
```

---

## How to Use

### Prerequisites
- [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (free download)
- Windows OS (required for Power BI Desktop)

### Steps

1. **Clone this repository**
   ```bash
   git clone https://github.com/YOUR_USERNAME/databel-churn-analysis.git
   cd databel-churn-analysis
   ```

2. **Open the report**
   ```
   Double-click reports/CASE_STUDY.pbix
   ```
   or open Power BI Desktop → File → Open → `reports/CASE_STUDY.pbix`

3. **Navigate the pages**
   Use the page tabs at the bottom of Power BI Desktop to move between the 10 report pages.

4. **Interact with filters**
   - Use slicers to filter by contract type, age group, gender, state, etc.
   - Click on chart elements to cross-filter all visuals on the page.

5. **Explore the data model**
   Go to **Model View** in Power BI Desktop to inspect the table structure and DAX measures.

---

## File Structure

```
databel-churn-analysis/
│
├── README.md                    # This file
│
├── reports/
│   └── CASE_STUDY.pbix          # Main Power BI report file
│
├── data/
│   └── README.md                # Dataset documentation
│
├── docs/
│   ├── dax-measures.md          # Full DAX measure documentation
│   ├── report-pages.md          # Detailed page-by-page breakdown
│   └── data-dictionary.md       # Field definitions
│
├── screenshots/
│   └── README.md                # Screenshots guide
│
└── .github/
    └── workflows/
        └── validate.yml         # CI: file integrity check
```

---

## Tools & Technologies

| Tool | Version | Purpose |
|---|---|---|
| Power BI Desktop | 2.91.884 | Report authoring |
| Power BI Cloud | 2026.03 | Published from |
| DAX | — | Calculations & measures |
| Power Query (M) | — | Data transformation |

---

## Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/new-analysis`
3. Commit your changes: `git commit -m 'Add churn cohort analysis'`
4. Push to the branch: `git push origin feature/new-analysis`
5. Open a Pull Request

---

## License

This project is for educational and portfolio purposes. The Databel dataset is a fictional dataset commonly used in data analytics courses.

---

*Built with ❤️ using Power BI | Case study for telecom churn analytics*
