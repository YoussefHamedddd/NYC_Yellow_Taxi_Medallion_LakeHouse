#  From 47 Million Raw Records to Business Intelligence: NYC Taxi Data Lakehouse

##  Project Overview
This project demonstrates a full-scale **End-to-End Data Lakehouse** implementation. I processed **47 million raw records** from the NYC Taxi & Limousine Commission dataset, transforming massive, fragmented CSV files into a highly optimized **Gold Layer** that powers interactive business dashboards and analytical insights.

---

##  1. Architecture Design (Medallion Architecture)
The pipeline is built on the **Medallion Architecture** to ensure data integrity and progressive enrichment at scale:

* **Bronze Layer:** Raw data ingestion from Cloud Object Storage into Delta format.
* **Silver Layer:** Data cleaning, schema enforcement, and handling of missing values using PySpark.
* **Gold Layer:** Business-level aggregates and Dimensional Modeling (**Star Schema**) for high-performance analytics.

![Project Design](https://github.com/YoussefHamedddd/NYC_Yellow_Taxi_Medallion_LakeHouse/blob/main/docs/Project%20Design.png?raw=true)

---

##  2. Data Modeling (Star Schema)
To optimize query performance for 47M records, I designed a **Star Schema** that separates quantitative facts from descriptive dimensions, ensuring fast joins and efficient storage:

* **Fact Table:** `fact_trips` (Stores metrics like fare_amount, trip_distance, and passenger_count).
* **Dimension Tables:** `dim_vendor`, `dim_date`, `dim_payment_type`, and `dim_rate_code`.

![Star Schema](https://github.com/YoussefHamedddd/NYC_Yellow_Taxi_Medallion_LakeHouse/blob/main/docs/Star%20Schema.png?raw=true)

---

##  3. Pipeline Orchestration & Jobs
Workflow automation was managed using **Databricks Jobs**, creating a robust production pipeline with built-in quality gates:

1.  **Ingest_to_Bronze:** Batch ingestion of 47 million records.
2.  **Transform_to_Silver:** Applying transformation logic and data validation.
3.  **Gold_Modelling:** Loading cleaned data into the final analytical schema.
* **Quality Checks:** Automated tasks like `Verify_Silver_Quality` ensure that only high-quality data reaches the final layers.

![Tasks Workflow](https://github.com/YoussefHamedddd/NYC_Yellow_Taxi_Medallion_LakeHouse/blob/main/docs/Tasks.png?raw=true)

---

##  4. Business Intelligence & Visualization
Using **Databricks SQL Dashboards**, I translated millions of rows into actionable business stories:

###  Key Discovery: Price vs. Distance Correlation
The analysis revealed a strong **Positive Linear Correlation** between trip distance and fare amount. This validates the data quality and proves that the pricing logic remains consistent even across a massive dataset of 47M rows.

###  Revenue Performance
Implemented time-series analysis to track daily revenue trends, identifying peak demand periods and seasonal patterns in NYC transit activity.

![Dashboard](https://github.com/YoussefHamedddd/NYC_Yellow_Taxi_Medallion_LakeHouse/blob/main/docs/Dashboard.png?raw=true)

---

##  Tech Stack
* **Engine:** Apache Spark (PySpark)
* **Platform:** Databricks (Lakehouse Platform)
* **Storage:** Delta Lake (Supporting ACID Transactions & Time Travel)
* **Language:** SQL & Python
* **Orchestration:** Databricks Workflows

---

## Engineering Challenges Handled
* **Scalability:** Managed 47M records by leveraging Delta Lake’s optimization features.
* **Data Integrity:** Implemented automated validation steps to handle "dirty" data in the raw files.
* **Cost Efficiency:** Optimized Spark jobs to process large volumes within the Databricks Community Edition constraints.
