# Zomato Restaurant Analytics — End-to-End Data Analysis & BI Dashboard

![Python](https://img.shields.io/badge/Python-3.13-blue?logo=python)
![Pandas](https://img.shields.io/badge/Pandas-2.x-150458?logo=pandas)
![Seaborn](https://img.shields.io/badge/Seaborn-0.13-4C72B0)
![Power BI](https://img.shields.io/badge/PowerBI-Dashboard-F2C811?logo=powerbi)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen)
![License](https://img.shields.io/badge/License-MIT-lightgrey)

> **Transforming raw restaurant data into actionable business intelligence** — a full-cycle analytics project covering data cleaning, exploratory analysis, statistical visualization, and an interactive Power BI dashboard across 148 restaurants.

---

## Table of Contents

- [Project Overview](#project-overview)
- [Business Problem](#business-problem)
- [Tech Stack](#tech-stack)
- [Dataset Description](#dataset-description)
- [Project Structure](#project-structure)
- [How to Run](#how-to-run)
- [Notebook Workflow](#notebook-workflow)
- [Key Insights](#key-insights)
- [Dashboard](#dashboard)
- [Business Recommendations](#business-recommendations)
- [Future Improvements](#future-improvements)
- [Limitations](#limitations)
- [Author](#author)

---

## Project Overview

This project delivers a comprehensive analysis of Zomato restaurant data using Python for exploratory data analysis (EDA) and Power BI for interactive business intelligence reporting. The dataset covers 148 restaurants with attributes including customer ratings, vote counts, pricing, online ordering availability, table booking status, and restaurant category.

The goal is to surface data-driven insights that restaurant operators, food-tech platforms, and business strategists can act on — from digital adoption patterns to pricing-quality relationships.

---

## Business Problem

The food & beverage industry relies on customer ratings, digital reach, and price positioning as key levers for growth. Without structured analysis, operators lack clarity on:

- Which restaurant categories attract the most customer engagement
- Whether digital features (online ordering, table booking) correlate with higher ratings
- How pricing relates to perceived quality across restaurant segments
- Which outlets are top performers vs. underperformers

This project addresses each of these questions with evidence-backed analysis.

---

## Tech Stack

| Layer | Tool / Library | Purpose |
|---|---|---|
| Data Manipulation | Python 3.13, Pandas 2.x | Cleaning, transformation, aggregation |
| Numerical Computing | NumPy | Array operations, type conversion |
| Visualization | Matplotlib, Seaborn | EDA charts — histograms, boxplots, heatmaps |
| Business Intelligence | Power BI | Interactive dashboard, KPIs, drill-down filters |
| Development | Jupyter Notebook | Reproducible analysis environment |
| Version Control | Git / GitHub | Source control and portfolio hosting |

---

## Dataset Description

**Source:** Zomato restaurant listings  
**Records:** 148 restaurants | **Features:** 7 columns  
**File:** `Zomato_data_.csv`

| Column | Type | Description | Example |
|---|---|---|---|
| `name` | string | Restaurant name | Jalsa, Truffles |
| `online_order` | categorical | Online ordering available (Yes/No) | Yes |
| `book_table` | categorical | Table booking available (Yes/No) | No |
| `rate` | string → float | Customer rating originally as "X/5", cleaned to float | 4.1/5 → 4.1 |
| `votes` | integer | Total customer votes received | 775 |
| `approx_cost(for two people)` | integer | Approximate dining cost for two (INR) | 800 |
| `listed_in(type)` | categorical | Restaurant category | Dining, Cafes, Buffet, Other |

**Type Distribution:**
- Dining: 54.7% (81 restaurants)
- Cafes: 24.3% (36 restaurants)
- Other: 14.2% (21 restaurants)
- Buffet: 6.8% (10 restaurants)

---

## Project Structure

```
zomato-restaurant-analytics/
│
├── 📓 zomato.ipynb              # Jupyter Notebook — EDA & visualization
├── 📄 Zomato_data_.csv          # Raw dataset (148 restaurants, 7 features)
├── 🖼️  dashboard.png            # Power BI dashboard screenshot
├── 📘 README.md                 # Project documentation (this file)
├── 📊 PROJECT_REPORT.md         # Executive analytics report
├── 📦 requirements.txt          # Python dependencies
└── 📁 assets/
    └── dashboard.png            # Dashboard image for README display
```

---

## How to Run

### Prerequisites

- Python 3.8 or higher
- Jupyter Notebook or JupyterLab
- Power BI Desktop (for dashboard interaction)

### Setup Instructions

**1. Clone the repository**
```bash
git clone https://github.com/your-username/zomato-restaurant-analytics.git
cd zomato-restaurant-analytics
```

**2. Create and activate a virtual environment**
```bash
python -m venv venv
# Windows
venv\Scripts\activate
# macOS / Linux
source venv/bin/activate
```

**3. Install dependencies**
```bash
pip install -r requirements.txt
```

**4. Launch the notebook**
```bash
jupyter notebook zomato.ipynb
```

**5. Run all cells** — execute top to bottom via `Kernel → Restart & Run All`

> **Power BI Dashboard:** Open `Zomato_Dashboard.pbix` in Power BI Desktop. Use the filter panel (Type, Online Order, Book Table, Rating Range, Cost Range) to explore interactive views.

---

## Notebook Workflow

The Jupyter Notebook follows a structured, reproducible analysis pipeline:

| Step | Action | Purpose |
|---|---|---|
| 1 | Library imports (Pandas, NumPy, Matplotlib, Seaborn) | Environment setup |
| 2 | `pd.read_csv()` — load dataset | Data ingestion |
| 3 | `isnull().sum()` — null check | Data quality validation |
| 4 | `df.info()` — schema inspection | Dtype and memory audit |
| 5 | `handleRate()` custom function | Rate column: "X/5" → float conversion |
| 6 | Countplot by `listed_in(type)` | Restaurant category distribution |
| 7 | `groupby('listed_in(type)')['votes'].sum()` + line/bar plot | Engagement by category |
| 8 | Histogram on `rate` | Rating distribution analysis |
| 9 | Countplot on `approx_cost(for two people)` | Pricing pattern analysis |
| 10 | Boxplot: `online_order` vs `rate` | Digital adoption impact on ratings |
| 11 | Pivot table + Heatmap: `listed_in(type)` × `online_order` | Cross-dimensional adoption mapping |

**Rate Cleaning Function:**
```python
def handleRate(value):
    value = str(value).split('/')
    value = value[0]
    return float(value)

df['rate'] = df['rate'].apply(handleRate)
```

---

## Key Insights

> All metrics sourced directly from the dataset (148 restaurants) and Power BI dashboard.

1. **Dining dominates by volume but not quality.** Dining restaurants represent 54.7% of all listings but hold an average rating of 3.57 — below Buffet (3.84) and Other (3.91) categories, suggesting a volume-quality trade-off.

2. **Table booking is the strongest rating predictor.** Restaurants offering table booking average 4.12 stars vs. 3.36 for those without — a 0.76-point gap, the largest differential in the dataset. This signals that reservation-capable venues invest more in the overall dining experience.

3. **Online ordering correlates with higher ratings.** Restaurants accepting online orders average 3.74 stars vs. 3.29 for offline-only venues — a 0.45-point advantage, indicating that digitally accessible restaurants tend to perform better overall.

4. **Higher cost does not guarantee higher ratings.** The Rating vs. Cost scatter plot shows dispersed data across all price ranges, with top-rated restaurants (4.4–4.6) concentrated in the mid-price segment (₹300–₹600), not at the top end.

5. **Dining category captures most customer engagement.** Dining restaurants receive 20,363 total votes — more than double the next category (Other: 9,367) — making it the highest engagement segment despite relatively moderate average ratings.

6. **Buffet restaurants are the most expensive and highest rated.** With an average cost of ₹671 for two and an average rating of 3.84, Buffets represent a premium-value segment that over-indexes on customer satisfaction.

7. **More votes consistently predict higher ratings.** The Rating vs. Votes scatter plot shows a positive trend — restaurants with large vote counts (3,000+) cluster at 3.9–4.6 stars, confirming that broad customer engagement reinforces quality perception.

---

## Dashboard

### Power BI Dashboard — Zomato Restaurant Analytics

![Zomato Dashboard](dashboard.png)

**Dashboard KPIs:**

| Metric | Value |
|---|---|
| Total Restaurants | 148 |
| Average Rating | 3.63 / 5 |
| Total Customer Votes | 39,192 |
| Average Cost for Two | ₹418.2 |
| Online Order Availability | 55.4% |
| Table Booking Availability | 56.8% |

**Dashboard Components:**
- **Pie Chart:** Type distribution across Dining (54.7%), Cafes (24.3%), Other (14.2%), Buffet (6.8%)
- **Bar Charts:** Average Rating and Total Votes by restaurant type
- **Comparison Charts:** Average rating by Online Order availability and Table Booking status
- **Scatter Plots:** Rating vs. Cost, Rating vs. Votes (correlation analysis)
- **Top 10 Lists:** Restaurants ranked by votes (leader: AB's Absolute Barbecues, 4,884) and by rating (leader: Coast Cafe, 4.6)
- **Interactive Filters:** Type, Online Order, Book Table, Rating Range (2.6–4.6), Cost Range (₹100–₹950)

---

## Business Recommendations

Based on the analytical findings, the following actions are recommended for restaurant operators and platform managers:

1. **Prioritize table booking enablement.** The 0.76-star rating premium for table booking restaurants justifies platform investment in reservation infrastructure — especially for Dining and Cafes segments.

2. **Accelerate online ordering adoption.** With only 55.4% of restaurants currently offering online orders and an associated 0.45-star rating advantage, expanding digital ordering coverage is a high-ROI initiative.

3. **Advise mid-range pricing strategies.** Data shows that optimal ratings cluster in the ₹300–₹600 range. Premium-priced restaurants (₹800+) do not consistently outperform on ratings, suggesting pricing above that threshold carries diminishing returns.

4. **Focus engagement campaigns on Dining category.** Given its 54.7% share and high vote volume (20,363), Dining is the most customer-active segment. Loyalty programs and promotional campaigns here will yield the broadest reach.

5. **Investigate low-vote, high-rated restaurants.** Several restaurants in the Top 10 by rating have relatively few votes. These could be hidden gems with strong quality signals that benefit from increased platform visibility.

---

## Future Improvements

- **Geospatial analysis** — Map restaurant performance by neighborhood or city zone
- **Time-series analysis** — Track rating and vote trends over time
- **Predictive modeling** — ML regression to predict ratings from cost, type, and digital features
- **Sentiment analysis** — NLP on customer reviews to extract qualitative themes
- **Customer segmentation** — Cluster restaurants by profile (price, type, digital adoption) for targeted insights
- **Competitive benchmarking** — Cross-platform comparison with Swiggy or Google Reviews data

---

## Limitations

- **Sample size:** 148 restaurants is sufficient for EDA but limits statistical generalizability
- **No geographic data:** Neighborhood or city-level breakdown is unavailable, preventing location-based analysis
- **Static snapshot:** The dataset represents a single point in time; no temporal trend analysis is possible
- **No review text:** Analysis is quantitative only; sentiment and qualitative signals are absent
- **Self-reported metrics:** Rating and vote data is as-of dataset creation and may not reflect current restaurant status

---

## Author

Nishant Ranjan  
Data Analyst | Python | Power BI | SQL  
[LinkedIn](https://www.linkedin.com/in/nishant015/) · [Instagram](https://www.instagram.com/inishantindia/?hl=en) .[Email](nishant845423@gmail.com)

---

*Last Updated: May 2025 | Dataset: Zomato Restaurant Listings | Records: 148*
