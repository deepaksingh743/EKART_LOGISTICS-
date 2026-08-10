# 📦 Ekart Logistics & Supply Chain Analytics Dashboard

An end-to-end data analytics and business intelligence project built to optimize logistics operations, track revenue growth, minimize high-cost RTO (Return to Origin) shipments, and analyze customer satisfaction for an e-commerce delivery network.

---

## 📸 Dashboard Preview
*(Aap apne Power BI pages ke screenshots yahan upload karke attach kar sakte hain)*

### 1. Fleet Management & Route Analytics
![Fleet Dashboard](screenshots/fleet_page.png)

### 2. Revenue & Financial Insights
![Revenue Dashboard](screenshots/revenue_page.png)

### 3. Returns & RTO Management
![RTO Dashboard](screenshots/rto_page.png)

### 4. Customer Feedback & Quality Scorecard
![Customer Dashboard](screenshots/customer_page.png)

---

## 🎯 Business Problem & Objective
In the e-commerce logistics sector, operational inefficiencies like delivery delays, high RTO (Return to Origin) rates, and unoptimized routing lead to significant financial leakage and lower customer retention. 

**Objective:** Build an interactive Power BI dashboard backed by robust SQL queries to monitor supply chain bottlenecks, evaluate hub-wise performance, and provide actionable insights for cost reduction and service improvement.

---

## 📊 Key Dashboard Pages & Features

1. **Fleet & Route Analytics:** 
   * Analyzes distance traveled against package weight using scatter plots.
   * Tracks hub-wise operational workloads to identify heavy shipment bottlenecks.
2. **Revenue & Financial Performance:** 
   * Highlights total freight charges, revenue trends, and service-type profitability (`Standard` vs `Express` vs `Same-Day`).
3. **Returns & RTO Analysis:** 
   * Tracks delivery failures, cancellation counts, and pinpoints high-risk destination cities with elevated RTO percentages.
4. **Customer Experience & Satisfaction:** 
   * Correlates delivery status (On-Time vs Delayed) with customer ratings, proving the direct financial and retention impact of on-time deliveries.

---

## 💡 Key Business Insights & Findings
* **The Delay-Rating Drop:** Data proves that on-time deliveries consistently maintain a rating of **4.5+ stars**, whereas delayed shipments suffer a steep drop in customer satisfaction scores, directly impacting brand loyalty.
* **Weight & Distance Trend:** The majority of standard e-commerce packages remain under **5 KG** across all distances, while heavy shipments (20+ KG) require specialized handling lanes.
* **RTO Optimization Hotspots:** Identifying specific destination cities with high RTO rates allows management to implement proactive address verification prior to dispatch, saving two-way shipping overhead costs.

---

## 🛠️ Tech Stack & Skills Demonstrated
* **Data Visualization & BI:** Power BI Desktop, DAX Measures, Conditional Formatting, Interactive Slicers, Tooltips.
* **Database & Advanced SQL:** CTEs, Window Functions (`RANK()`), Conditional Aggregation (`CASE WHEN`), Joins, Grouping Sets.
* **Data Validation:** Python / Pandas (Dataset preprocessing and profiling).

---

## 💻 Sample Advanced SQL Implementation
This project includes complex SQL logic to solve real-world supply chain problems, such as identifying top RTO destination cities per hub using window functions:

```sql
WITH RTO_Summary AS (
    SELECT 
        Origin_Hub,
        Destination_City,
        COUNT(Shipment_ID) AS RTO_Count
    FROM ekart_logistics_dataset
    WHERE Delivery_Status = 'RTO (Return to Origin)'
    GROUP BY Origin_Hub, Destination_City
),
Ranked_Destinations AS (
    SELECT 
        Origin_Hub,
        Destination_City,
        RTO_Count,
        RANK() OVER (PARTITION BY Origin_Hub ORDER BY RTO_Count DESC) AS rnk
    FROM RTO_Summary
)
SELECT Origin_Hub, Destination_City, RTO_Count
FROM Ranked_Destinations
WHERE rnk <= 2;
