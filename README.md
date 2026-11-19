# Delivery and Logistics Performance Analysis

![Python](https://img.shields.io/badge/Python-3.10+-blue)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)
![Cost](https://img.shields.io/badge/Cost-Free%20(Google%20Colab)-orange)
![Data](https://img.shields.io/badge/Data-Simulated-lightgrey)

On-time delivery, failed deliveries and delay drivers across carriers, regions, distance bands, weekdays and months.

## Table of Contents
1. [Problem Statement](#problem-statement)
2. [STAR Summary](#star-summary)
3. [Dataset](#dataset)
4. [What the Notebook Does](#what-the-notebook-does)
5. [Key Results (from the executed run)](#key-results-from-the-executed-run)
6. [Sample Output](#sample-output)
7. [Checks and Fallbacks](#checks-and-fallbacks)
8. [Limitations](#limitations)
9. [Tech Stack](#tech-stack)
10. [How to Run](#how-to-run)
11. [Files](#files)
12. [About Me](#about-me)

## Problem Statement
A logistics company delivers thousands of orders through several carriers across five regions. Management wants to know how many orders arrive on time, which carriers and routes cause delays or failed deliveries, and which factors (distance, weight, weekday, season) push an order to be late.

## STAR Summary
- **Situation:** Orders were moving through 4 carriers and 5 regions, but delivery performance was only visible as one overall average.
- **Task:** Break delivery performance down so the weak carriers, regions and periods become visible.
- **Action:** Calculated delay days against the promised date for 6,000 orders, separated delivered, failed and returned orders, compared carriers, regions, a carrier x region heatmap, distance and weight bands, weekdays and months.
- **Result:** On-time delivery was 79.2% overall, but QuickMove delivered only 56.8% on time and 33.7% in the East region. November and December dropped to about 61% on-time against 80 to 84% in the other months.

## Dataset
- **Simulated data created inside the notebook** (fixed random seed), not real company data: 6,000 orders across 2025 with order date, promised date, delivered date, carrier, region, distance (km), weight (kg) and status.
- Different delay and failure tendencies were built in per carrier and region, plus a November/December surge and a weekend effect. The findings therefore show that the analysis finds those patterns. They are not claims about real carriers.
- Status split: 5,643 Delivered, 189 Failed (no delivery date), 168 Returned.

## What the Notebook Does
1. Creates the delivery orders dataset.
2. Checks missing values and duplicate order ids.
3. Calculates delivery days, delay days and an on-time flag (on-time = delivered on or before the promised date).
4. Calculates the main KPIs.
5. Compares carriers and regions, then builds a carrier x region on-time heatmap and lists the 5 weakest combinations (minimum 30 orders).
6. Checks distance bands, weight bands, correlations, weekdays and months.
7. Prints insights and recommendations, and saves charts and CSV files.

## Key Results (from the executed run)
| Metric | Value |
|---|---|
| Orders / delivered / failed / returned | 6,000 / 5,643 / 189 / 168 |
| On-time delivery rate (delivered orders) | 79.2% |
| Late deliveries | 1,173 |
| Average delay of late orders | 1.4 days |
| Average delivery time | 4.14 days |
| Failed / returned rate | 3.15% / 2.8% |

| Carrier | On-time % | Failed % |
|---|---|---|
| FastTrack | 91.22 | 1.90 |
| CityExpress | 83.45 | 2.73 |
| SafeShip | 78.23 | 3.35 |
| QuickMove | 56.79 | 5.26 |

| Region | On-time % |
|---|---|
| Central | 86.42 |
| South | 85.29 |
| North | 80.78 |
| West | 79.59 |
| East | 59.47 |

- Weakest carrier + region combination: QuickMove in East, 33.7% on time (181 orders).
- Distance: 89.9% on time for short (under 200 km), 83.39% for medium, 72.8% for long (600 km and above).
- Weight: 81.0% for light (0 to 3 kg) down to 72.56% for very heavy (15 kg and above).
- Correlation with delay days: distance 0.186, weight 0.097 (both weak).
- Weekdays: Thursday was best (84.8%), Sunday weakest (70.5%).
- Months: November 60.6% and December 61.6%, against 80.4% to 84.4% in January to October.

## Sample Output
```
KEY INSIGHTS
--------------------------------------------------
1. Overall on-time delivery rate is 79.2 % and 3.2 % of orders failed
2. Best carrier: FastTrack ( 91.2 % on time )
3. Weakest carrier: QuickMove ( 56.8 % on time )
4. Highest failed delivery rate: QuickMove ( 5.3 % )
5. Weakest region: East ( 59.5 % on time )
6. Weakest carrier + region combo: QuickMove in East ( 33.7 % on time )
7. Long distance orders are on time 72.8 % vs 89.9 % for short distance
8. Worst month: 2025-11 | Worst order weekday: Sunday
```

## Checks and Fallbacks
- Missing values (189 delivery dates, all for failed orders) and duplicate order ids (0) are checked and printed.
- On-time rate is calculated on delivered orders only. Failed and returned orders are reported separately so they do not distort it.
- The weakest-combination list uses a minimum of 30 orders so tiny groups do not appear.
- Data is generated with a fixed seed, so the numbers above repeat on every run.
- No LLM or paid API is used, so there is no cost or latency to track.

## Limitations
- The data is simulated, so rankings reflect the settings used to generate it.
- The on-time rate uses only orders with status Delivered (5,643). Failed and returned orders are left out of it and reported separately.
- Correlations are weak, so distance and weight explain only a small part of the delay.

## Tech Stack
| Area | Tools |
|---|---|
| Language | Python |
| Data handling | pandas, numpy |
| Charts | matplotlib, seaborn |
| Environment | Google Colab |

## How to Run
1. Open `delivery_logistics_performance.ipynb` in Google Colab.
2. Click Runtime > Run all.
3. No dataset download or API key is needed.
4. Charts and CSV files are saved in the Colab file panel.

## Files
- `delivery_logistics_performance.ipynb` (executed notebook with outputs)
- `requirements.txt`
- Generated by the notebook: `delay_distribution.png`, `carrier_performance.png`, `region_performance.png`, `carrier_region_heatmap.png`, `weekday_and_monthly_trend.png`, `carrier_performance.csv`, `region_performance.csv`, `weakest_carrier_region_combos.csv`, `delivery_orders_clean.csv`

## About Me
**Akshat Kesharwani** | Data Analyst and Data Scientist (fresher) | Sagar, Madhya Pradesh
- Portfolio: https://akshatkesharwani-info.github.io/
- GitHub: https://github.com/akshatkesharwani-info
- Email: akshatkesharwani12345@gmail.com
