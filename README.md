# 📦 Ekart Logistics Supply Chain & Operations Analytics

An end-to-end data analytics project analyzing e-commerce logistics operations, fleet performance, financial revenue, return-to-origin (RTO) rates, and customer satisfaction using **Power BI** and **Advanced SQL**.

---

## 🚀 Project Overview
This project provides deep operational insights into a simulated logistics and e-commerce delivery network (**Ekart Logistics**). The goal is to identify bottlenecks in fleet routing, track revenue generators, minimize high-cost RTO (Return to Origin) shipments, and correlate on-time delivery performance with customer satisfaction ratings.

---

## 📊 Dashboard Structure (Power BI)
The interactive Power BI dashboard is structured into multiple specialized pages:
1. **Fleet Management & Route Analytics:** Analyzes distance traveled versus package weight using scatter plots and hub performance breakdowns.
2. **Revenue & Financial Analytics:** Tracks total freight charges, revenue trends, and service-type profitability (`Standard`, `Express`, `Same-Day`).
3. **Returns & RTO Management:** Highlights delivery failures, cancellation tracking, and high-risk destination cities.
4. **Customer Feedback & Satisfaction:** Examines average customer ratings, negative feedback trends, and the direct link between delivery delays and score drops.

---

## 🛠️ Tech Stack & Tools
* **Data Visualization:** Power BI Desktop (DAX Measures, Interactive Slicers, Custom Tooltips)
* **Database & Querying:** SQL (Intermediate to Advanced Queries, CTEs, Window Functions, Conditional Aggregation)
* **Data Processing:** Python / Pandas (Dataset profiling and validation)

---

## 💻 Key SQL Solutions Included
This repository also contains complex SQL queries answering critical business questions:
* **Conditional Aggregation:** Calculating On-Time Delivery Rates percentage by service type.
* **Window Functions (`RANK()`):** Identifying top destination cities with the highest RTO shipments per origin hub using CTEs.
* **Correlated Subqueries / Joins:** Filtering shipments with freight charges higher than their respective service type averages.
* **Operational Matrix:** Generating hub-wise delay and cancellation summaries with calculated percentages.

---

## 📂 Repository Structure
```text
├── dataset/
│   └── ekart_logistics_dataset.csv
├── power_bi_dashboard/
│   └── ekart_logistics_dashboard.pbix
├── sql_queries/
│   └── advanced_logistics_queries.sql
└── README.md
