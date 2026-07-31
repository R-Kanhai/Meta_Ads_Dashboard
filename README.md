# 📊 Meta Ad Performance Analysis

An interactive **Power BI** dashboard analyzing the full-funnel performance of Meta (Facebook & Instagram) ad campaigns — from impressions and clicks through to purchases — with audience, geography, and time-based breakdowns.

![Power BI](https://github.com/R-Kanhai/Meta_Ads_Dashboard/blob/main/Snapshot%20of%20Meta_Ads_Dashboard.png)
---

## 📌 Business Objective

The marketing team needed a single performance-tracking report for ad campaigns running on **Facebook and Instagram**, giving visibility into reach, engagement, conversions, and budget utilization — enabling the team to:
- Identify the most effective platform (Facebook vs. Instagram)
- Track campaign ROI and optimize budget allocation
- Understand audience engagement patterns

**Scope:** Paid campaigns on Facebook and Instagram only. Messenger, Audience Network, and organic (non-paid) engagement are out of scope

---

## 🗂️ Dashboard Pages

The report has two near-identical pages, one per platform, linked via a page navigator — so performance can be compared side by side by switching tabs.

### Facebook / Instagram (per-page layout)

| Visual | Chart Type | Shows |
|---|---|---|
| **Top KPI card** | Multi-metric Card | Impressions, Clicks, Shares, Comments, Purchases, Engagements |
| **Efficiency KPI card** | Multi-metric Card | CTR, Engagement Rate, Conversion Rate, Purchase Rate, Total Budget, Avg Budget per Campaign |
| **Traffic by Segment** | Donut Chart | Selected metric split by target gender |
| **Target Age Group** | Column Chart | Selected metric across user age groups |
| **Engagement by Country** | Map | Geographic spread of the selected metric |
| **Weekly Engagement Trend** | Stacked Column Chart | Weekly performance, stacked by ad type |
| **Hourly Trend** | Area Chart | Selected metric by hour of day (0–23) |
| **Calendar Heat Map** | Matrix (by Week/Day) | Daily activity levels across the month, to spot spikes |
| **Ad Type Breakdown** | Matrix Table | CTR, Purchase Rate, Conversion Rate, Engagement Rate, Impressions, and Clicks by ad type |

**Dynamic metric switching:** A **"Select Measure"** slicer drives most visuals above — instead of building a separate chart per KPI, users pick which metric (Impressions, Clicks, Purchases, etc.) they want each chart to display, and titles update dynamically to match the selection.

**Other filters:** Month, Campaign Name, and Target Interests slicers apply across the whole page.

---

## 🧱 Data Model

Built on a star schema:

| Table | Role | Purpose |
|---|---|---|
| **ad_events** | Fact table | Event-level log of every ad interaction (impression, click, share, comment, purchase), with derived day-of-week and time-of-day fields |
| **ads** | Dimension | Ad creative metadata — platform, ad type, target gender/age/interests |
| **campaigns** | Dimension | Campaign name, start/end date, budget — basis for cost KPIs |
| **users** | Dimension | Demographics — gender, age, country, location, interests |

`ad_events` joins to `ads` (creative details), `ads` joins to `campaigns` (budget/timeframe), and `ad_events` joins to `users` (demographics) — giving a clean fact-to-dimension structure for all KPI calculations.

---

## 📐 KPIs & Definitions

| KPI | Formula |
|---|---|
| Impressions | Count of `event_type = Impression` |
| Clicks | Count of `event_type = Click` |
| Shares / Comments | Count of `event_type = Share / Comment` |
| Purchases | Count of `event_type = Purchase` |
| Engagements | Clicks + Shares + Comments |
| CTR | (Clicks ÷ Impressions) × 100 |
| Engagement Rate | (Engagements ÷ Impressions) × 100 |
| Conversion Rate | (Purchases ÷ Clicks) × 100 |
| Purchase Rate | (Purchases ÷ Impressions) × 100 |
| Total Budget | Sum of campaign budgets |
| Avg Budget per Campaign | Total Budget ÷ Campaign Count |

---

## 🔍 Key Insights from the Analysis

- **Strong top-of-funnel performance:** 216K impressions generated 25.4K clicks — an **11.76% CTR**, well above typical industry benchmarks (~1–2%), with a healthy **13.56% engagement rate**.
- **Funnel drop-off at purchase:** Only 1.3K purchases resulted from those clicks — a **5.21% conversion rate** from clicks and just **0.61%** from total impressions, pointing to landing-page, offer, or audience-fit issues rather than an awareness problem.
- **Audience:** Females (43% of engagement) outperform males (22%); the **18–30 age group** drives the majority of interactions.
- **Geography:** India and Brazil lead in engagement volume, while Germany and the UK show signs of higher-value (higher purchasing power) audiences — suggesting different strategies for high-volume vs. high-value markets.
- **Timing:** Engagement is steady week-over-week but peaks in the **afternoon and evening hours**; certain calendar dates show spikes likely tied to promotions or launches.
- **Ad format:** **Video ads** perform best on CTR, conversion, and engagement rate, followed closely by **Stories**; Image and Carousel formats lag slightly on conversion efficiency.

**Bottom line:** Campaigns are excellent at generating awareness and engagement, but the purchase funnel leaks heavily after the click — the recommended focus is landing-page optimization, retargeting, and reallocating budget toward Video/Stories formats, high-value geographies, and afternoon/evening scheduling.

---

## 🛠️ Tech Stack

- **Power BI Desktop** — data modeling, DAX, report design
- **Power Query** — data cleaning and transformation
- **DAX** — KPI measures and dynamic measure-switching logic (via the Select Measure parameter)

---

## 🚀 How to Explore

1. Open `Meta_Ads_Performance_Analysis.pbix` in Power BI Desktop, **or**
2. View the interactive version via the Publish-to-Web link above (no login required)
3. Use the **page navigator** to switch between Facebook and Instagram views
4. Use the **Select Measure** slicer to change which KPI drives the charts
5. Filter by **Month, Campaign, or Target Interests** to narrow the view
6. Hover over the map, calendar, or charts for detail; click any segment to cross-filter the page

---

## 📁 Repository Contents

```
├── Meta_Ads_Performance_Analysis.pbix   # Power BI report file
├── /docs                                 # Domain knowledge & business requirements
├── /screenshots                          # Dashboard preview images
└── README.md
```


## 📬 Contact

Built by **Rohan Kanhai** as part of a Power BI portfolio project.

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/rkanhai/) [![Email](https://img.shields.io/badge/Email-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:rohankanhai55@gmail.com)

- **LinkedIn:** [linkedin.com/in/rkanhai](https://www.linkedin.com/in/rkanhai/)
- **Email:** [rohankanhai55@gmail.com](mailto:rohankanhai55@gmail.com)

*Note: This project uses a simulated Meta Ads dataset for demonstration purposes.*
