# Toyota Tanzania — Business Intelligence & Marketing Analytics Dashboard

> **A multi-dimensional Power BI analytics project covering sales performance, supply chain, marketing campaign effectiveness, digital traffic, after-sales operations, and customer voice for Toyota Tanzania (2025)**

---

## Table of Contents

- [Project Overview](#project-overview)
- [Business Questions Answered](#business-questions-answered)
- [Data Sources](#data-sources)
- [Data Model](#data-model)
- [Dashboard Pages](#dashboard-pages)
- [Key KPIs & Metrics](#key-kpis--metrics)
- [Key Insights](#key-insights)
- [Tools & Technologies](#tools--technologies)
- [How to Use This Report](#how-to-use-this-report)
- [Project Structure](#project-structure)
- [Author](#author)

---

## Project Overview

This project is a comprehensive **Business Intelligence dashboard** built in **Power BI** for Toyota Tanzania Ltd, analyzing 2025 business performance across six interconnected data domains. The dashboard is designed to give marketing, sales, and operations teams a single source of truth — enabling data-driven decisions across the entire customer lifecycle, from vehicle importation through to after-sales satisfaction.

The analysis covers **595 imported units**, **43 sales transactions worth 5.28 billion TZS**, **18 marketing campaigns**, **36 months of digital traffic data**, **30 service centre records**, and **25 customer survey responses** — all modelled into a unified star schema for cross-domain analysis.

---

## Business Questions Answered

### Sales & Revenue
- Which vehicle model generates the most revenue, and which generates the most volume?
- How does revenue trend month-over-month across 2025?
- Which region (Dar es Salaam, Mbeya, Arusha, Mwanza) drives the highest sales?
- What is the revenue split between Corporate, Fleet, SME, and Individual customers?
- Does discounting correlate with higher transaction volume or lower margin?

### Supply Chain & Imports
- What is the estimated gross margin per model (import cost vs. selling price)?
- Which supplier and source country provides the most vehicles by volume and value?
- Are imported quantities aligned with sales velocity — or is stock building up?
- What is the cost difference between air and sea freight, and when is each used?

### Marketing Effectiveness
- Which campaign channel (TV, Social Media, Facebook, Google Ads, Email, LinkedIn) delivers the best ROI?
- What is the cost per lead and cost per conversion by channel?
- How do lead-to-conversion rates compare across campaigns?
- Is there a measurable lift in sales during or after campaign periods?
- Which model-specific campaigns outperformed?

### Digital Analytics
- How has organic search traffic grown across 2025?
- Which source/medium (Google Organic, Direct, Facebook, Instagram, YouTube, TikTok) converts best?
- What are users searching for, and what does keyword intent reveal about the buying funnel?
- How do bounce rate and session duration differ by channel?

### After-Sales & Service
- Which service type and location scores highest on customer satisfaction?
- Are Fleet and Corporate customers more loyal (repeat visits) than Individual customers?
- What is the revenue and profitability profile of different service types?
- Which service jobs take the most labour hours and carry the highest parts cost?

### Customer Voice
- What does the typical buyer profile look like for each vehicle model?
- What is the Net Promoter Score (NPS) proxy — and who are the detractors?
- How does financing method preference vary by income group and age?
- Which purchase channel (Showroom vs. Direct) is preferred by different demographics?

---

## Data Sources

All data is sourced from the Toyota Tanzania business intelligence Excel workbook (`Toyota-Analysis.xlsx`), containing six sheets:

| Sheet Name | Records | Description |
|---|---|---|
| `sales vehicle` | 43 rows | Vehicle sales transactions Jan–Dec 2025 |
| `vehicle imports data` | 25 rows | Inbound shipment records Jan–Dec 2025 |
| `marketing campaign` | 18 rows | Campaign performance by channel Jan–Dec 2025 |
| `vehicle digital` | 36 rows | Monthly website traffic by source/medium Jan–Dec 2025 |
| `vehicle center operations` | 30 rows | Service centre job records Jan–Jun 2025 |
| `customer survey` | 25 rows | Post-purchase customer satisfaction survey |

---

## Data Model

The project uses a **star schema** with `sales vehicle` as the central **fact table**, connected to four supporting dimension/supplementary tables via shared keys.

```
vehicle imports data ──── Model ────┐
marketing campaign   ──── Date  ────┤
vehicle digital      ──── Date  ────┤──► sales vehicle (FACT)
vehicle center ops   ──── Model ────┤
customer survey      ──── Model ────┘
```

### Relationships

| From Table | Key Column | To Table | Key Column | Cardinality |
|---|---|---|---|---|
| `vehicle imports data` | `Model` | `sales vehicle` | `Model` | Many-to-Many |
| `marketing campaign` | `Start_Date` | `sales vehicle` | `Date` | Many-to-Many |
| `vehicle digital` | `Date` | `sales vehicle` | `Date` | Many-to-One |
| `vehicle center operations` | `Vehicle_Model` | `sales vehicle` | `Model` | Many-to-Many |
| `customer survey` | `Vehicle_Model` | `sales vehicle` | `Model` | Many-to-Many |

> All data transformations (column renaming, data type correction, date formatting, and derived columns) were handled in **Power Query** before loading into the model.

---

## Dashboard Pages

### Page 1 — Executive Summary
High-level overview of 2025 business performance. KPI cards for total revenue, units sold, average transaction value, campaign ROI, service satisfaction, and NPS proxy. Year-at-a-glance sparklines for revenue and traffic trends.

### Page 2 — Sales Performance
Revenue and unit volume by model, region, customer type, sales channel, and payment method. Monthly revenue trend line. Discount analysis by customer segment. Top and bottom performing models by both value and volume.

### Page 3 — Supply Chain & Imports
Import volume and cost by model, supplier, and source country. Gross margin estimates (import cost USD vs. selling price TZS). Inventory turnover comparison — units imported vs. units sold by model. Shipping mode (Air vs. Sea) cost analysis.

### Page 4 — Marketing Campaign Analytics
Campaign ROI ranked by channel. Cost per lead and cost per conversion by channel. Lead-to-conversion funnel. Budget allocation vs. revenue generated. Month-by-month campaign activity overlaid with sales trends.

### Page 5 — Digital & Web Analytics
Monthly traffic trend by source/medium. Bounce rate vs. session duration scatter (traffic quality). Conversion rate by channel. Top-performing keywords and their associated conversion types. Organic traffic growth trend (Jan–Dec 2025).

### Page 6 — Service Centre Operations
Service job frequency by type and location. Average satisfaction score by service type, location, and customer type. Repeat customer rate by segment. Labour hours vs. revenue per job. Parts cost vs. total job value analysis.

### Page 7 — Customer Insights
Buyer persona profiles by vehicle model. Age group, gender, and income distribution. Purchase channel preference by demographic. Financing method vs. income group. NPS proxy breakdown — promoters vs. detractors.

---

## Key KPIs & Metrics

| KPI | Value | Notes |
|---|---|---|
| Total Sales Revenue | 5.28B TZS | 43 transactions, Jan–Dec 2025 |
| Units Sold | 71 | Across 8 models |
| Total Import Cost | $10.47M USD | 595 units, 25 shipments |
| Average Transaction Value | 122.8M TZS | Per sales record |
| Best Campaign ROI | 14,400% | Eid Special — Facebook |
| Worst Campaign ROI | -100% | Service Campaign — Radio |
| Average Service Satisfaction | 4.62 / 5 | 30 service records |
| Repeat Customer Rate (Service) | 67% | 20 of 30 are repeat visits |
| Customer NPS Proxy | 92% | Would recommend Toyota |
| Organic Traffic Growth | +54% | Jan 1,250 → Dec 1,920 users |
| Digital Conversions (Annual) | 413 | Across all channels |
| Average Campaign ROI | 6,712% | Excluding failed Radio campaign |

---

## Key Insights

### 1. Digital channels outperform traditional media by ~6x on cost per conversion
Facebook (Eid Special): **82,759 TZS per conversion** vs. TV (Q1 Hilux Push): **529,412 TZS per conversion**. Yet TV and Radio absorb ~38% of total campaign budget while delivering only ~22% of campaign revenue. This represents a significant budget reallocation opportunity.

### 2. The Hilux DX is the volume king; Land Cruiser 300 is the margin king
Hilux DX is the most imported model (198 units), the most sold by frequency (8 transactions), and the most searched online ("hilux double cabin" is the #1 organic keyword). However, Land Cruiser 300 generates the highest revenue per transaction (265–275M TZS) on the lowest import volume — making it the most profitable model per unit.

### 3. Passo faces a potential overstock problem
230 Passo units were imported across 2025, but only ~11 units appear in sales records. At 9.5–10.5M TZS per unit, these are the lowest-margin vehicles in the range. A targeted pricing or campaign push may be needed to move inventory.

### 4. Fleet and Corporate customers drive disproportionate revenue
Fleet customers receive up to 7% discount but place the largest multi-unit orders (3–5 vehicles per transaction). Corporate customers buying Fortuners and Land Cruisers via Finance account for the highest single-transaction values. Both segments show near-100% repeat service loyalty.

### 5. Organic search traffic grew 54% across the year with zero paid search spend
Google Organic grew from 1,250 users in January to 1,920 in December — the highest-converting channel at ~1.1% conversion rate, driven entirely by brand and model-specific keyword searches. This demonstrates strong unpaid brand equity.

### 6. The one failed campaign reveals a channel-audience mismatch
The Radio Service Campaign (8M TZS budget) generated 210 leads but **zero conversions** — a -100% ROI. Cross-referencing with customer survey data shows that service customers skew toward Fleet and Corporate types who are unlikely to respond to radio. SMS (CAMP013) with a 4.5M budget achieved 380 conversions at a fraction of the cost, suggesting direct channels work far better for after-sales.

---

## Tools & Technologies

| Tool | Purpose |
|---|---|
| **Power BI Desktop** | Dashboard development, data modelling, DAX measures, visualizations |
| **Power Query (M language)** | Data transformation, column typing, date formatting, table shaping |
| **DAX** | Calculated measures (gross margin estimate, conversion rate, ROI, repeat rate) |
| **Microsoft Excel** | Source data — 6-sheet business intelligence workbook |
| **Python (pandas, numpy)** | Exploratory data analysis and data validation prior to Power BI import |

---

## How to Use This Report

1. Clone or download this repository
2. Open `Toyota-Analysis.pbix` in **Power BI Desktop** (free download at [powerbi.microsoft.com](https://powerbi.microsoft.com))
3. If prompted to refresh data, ensure `Toyota-Analysis.xlsx` is in the same folder as the `.pbix` file
4. Use the **page navigation** tabs at the bottom to move between dashboard sections
5. Use the **slicers** on each page to filter by Model, Region, Customer Type, Channel, or Date
6. Cross-filter is enabled — clicking any chart element will filter all visuals on the page

> **Note:** The data covers Jan–Dec 2025 for Sales, Imports, Marketing, and Digital; and Jan–Jun 2025 for Service Centre operations.

---

## Project Structure

```
toyota-analysis/
│
├── Toyota-Analysis.pbix          # Power BI report file
├── Toyota-Analysis.xlsx          # Source data (6 sheets)
├── README.md                     # Project documentation
│
└── assets/
    └── screenshots/              # Dashboard preview images
```

---

## Author

**Hilda Galder Gabriel**
BSc Computer Science — University of Dar es Salaam

[![GitHub](https://img.shields.io/badge/GitHub-Dbrey27-181717?style=flat&logo=github)](https://github.com/Dbrey27)
[![Email](https://img.shields.io/badge/Email-hildagalder12%40gmail.com-D14836?style=flat&logo=gmail)](mailto:hildagalder12@gmail.com)

---

*Part of a growing data analytics portfolio. Also see: [Telecom Customer Churn Analysis](https://github.com/Dbrey27/telecom-churn-analysis)*
