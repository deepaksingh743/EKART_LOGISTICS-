# 📦 Ekart Logistics & Supply Chain Analytics Dashboard

An end-to-end data analytics and business intelligence project built to optimize logistics operations, track revenue growth, minimize high-cost RTO (Return to Origin) shipments, and analyze customer satisfaction for an e-commerce delivery network.

---

## 📸 Dashboard Preview
### 1. Dashboard Overview 
(<img width="895" height="506" alt="dashbaord 01" src="https://github.com/user-attachments/assets/402e5933-d747-4873-a054-4c1754168172" />

### 1. Fleet Management & Route Analytics
<img width="892" height="501" alt="dashbaord 02" src="https://github.com/user-attachments/assets/b12a008c-74e1-40aa-a783-feb35c6d00b0" />


### 2. Revenue & Financial Insights
<img width="892" height="506" alt="dashboard 3" src="https://github.com/user-attachments/assets/fe0f10a8-dc18-4cdc-b466-da814e2637e2" />


### 3. Returns & RTO Management
<img width="890" height="501" alt="dashboard 4" src="https://github.com/user-attachments/assets/8602df25-a9b9-48fd-9dc5-7a31acc95759" />


### 4. Customer Feedback & Quality Scorecard
<img width="891" height="503" alt="dashboard 5" src="https://github.com/user-attachments/assets/1cb11b5e-173a-4207-83fa-6bb76622839b" />


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
