



# Enterprise Data Modeling & Analytics: Star Schema Transformation

## 📌 Project Overview

This project focuses on refactoring a chaotic, highly fragmented relational database into a clean, optimized **Star Schema** in Power BI.

Originally, the dataset suffered from mixed granularity, scattered staging tables (`ORDERS_2025`, `ORDERS_2026`, `shipments`, `INVOICES`, `payments`), and missing dimensional hierarchy, which led to high query complexity and performance bottlenecks.

Through custom ETL modeling in Power Query, the architecture was completely redesigned into an enterprise-grade Star Schema with normalized dimension tables, dedicated fact tables, snapshot lifecycle tracking, and organized DAX measures.

---

## 🛠️ Key Transformations (Before vs. After)

### Before (Disorganized Staging Layout)

* **Disjointed Tables:** Historical orders split across separate yearly tables (`ORDERS_2025`, `ORDERS_2026`).


* **Grain Mismatch:** Order header details, invoice line items, customer contacts, and shipment milestones scattered without unified foreign keys.


* **Poor Model Navigation:** Overlapping, complex relationships causing ambiguous relationship paths.



### After (Optimized Star Schema)

* **Central Fact & Dimension Architecture:** Standardized dimensional tables (`01_dim_customers`, `02_dim_products`, `03_dim_junks`, `04_dim_locations`, `05_dim_campaign`, `dim_date`) surrounding core business processes.


* **Accumulating Process Tracking:** Built process tracking models (`05_fact_order_date_process`) to capture key operational milestones (`Order_Date`, `Shipment/Invoice Date`, `Delivery_Date`, `Payment_Date`) on a single line item.


* **Specialized Fact Tables:** Integrated core sales (`01_facts_sales`), inventory levels (`02_fact_inventory`), campaign performance (`03_fact_campaign`), and sales targets (`06_fact_salestarget`).


* **Centralized DAX Measure Repository:** Created a dedicated `_measures` table containing key KPIs such as `total_sales`, `total_orders`, `base_total_customer`, and `average_order_pay`.


* **Row-Level Security (RLS):** Implemented user domain and regional security tables (`security`) for access control.



---

## 📐 Data Model Architecture

```text
               ┌───────────────────────┐
               │       dim_date        │
               └───────────┬───────────┘
                           │
       ┌───────────────────┼───────────────────┐
       │                   │                   │
┌──────▼──────┐     ┌──────▼──────┐     ┌──────▼──────┐
│01_dim_cust  │     │01_facts_sales│     │02_dim_prod  │
└─────────────┘     └──────▲──────┘     └─────────────┘
                           │
       ┌───────────────────┼───────────────────┐
       │                   │                   │
┌──────┴──────┐     ┌──────┴──────┐     ┌──────┴──────┐
│04_dim_locs  │     │03_dim_junks │     │ _measures   │
└─────────────┘     └─────────────┘     └─────────────┘

```

---

## 📈 Technical Highlights

* **Tooling:** Power BI Desktop, Power Query (M), DAX.


* **Modeling Principles:** Star Schema Architecture, Accumulating Snapshot Fact Tables, Role-Playing Date Dimensions, Junk Dimensions, Row-Level Security (RLS).


* **Key DAX Metrics:** Gross Revenue, Active Customers, Average Order Value, Target vs. Actual Revenue.
