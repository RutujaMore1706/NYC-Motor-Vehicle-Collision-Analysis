# NYC-Motor-Vehicle-Collision-Analysis

## Overview

This project is an in-depth analysis of motor vehicle collisions data in New York City, utilizing data warehousing principles to transform and structure data for meaningful analysis. The aim is to model the data in a way that supports extensive reporting and dashboards, offering insights into traffic incidents, injuries, fatalities, and vehicle information.

## Project Architecture

The project involves a multi-layered data warehousing architecture, with an emphasis on staging, transformation, integration, and analysis layers. Key tools used include Alteryx for data profiling, Talend for ETL operations, SQL for data modeling, and Power BI/Tableau for visualization.

### 1. **Data Sources and Ingestion**

   - **Source Data:** The dataset includes NYC motor vehicle collision data, with tables for crashes, vehicles, and persons involved.
   - **Data Ingestion:** Data is initially ingested and loaded into staging tables using Talend, with SQL Server/Azure SQL as the primary RDBMS.
   
### 2. **Staging Area**

   - **Purpose:** Temporary storage where raw data is loaded before transformation.
   - **Tables:** Staging tables for `Crashes`, `Vehicles`, and `Persons`.
   - **Data Profiling and Cleansing:** Alteryx is used to identify data quality issues, inconsistencies, and format discrepancies. Profiling results guide data cleansing steps in the staging tables to standardize data types and ensure referential integrity.

### 3. **Data Transformation and Cleansing**

   - **Data Quality Rules:** Implement rules to handle invalid entries (e.g., negative vehicle years, undefined travel directions). Use surrogate keys (`-99` or similar) for missing values.
   - **Error Handling:** Error tables are created for `Model Year` and `Person Age` to record invalid values, allowing error tracking without halting the ETL process.

### 4. **Integration and Dimensional Modeling**

   - **Dimensional Model:** The dimensional model in the integration schema organizes data for analytics. This model includes fact and dimension tables, supporting historical and trend analysis across various dimensions.
   - **Dimensions and Facts:**
     - **Fact Table:** Stores metrics like collision count, injuries, fatalities, and vehicle involvements per collision.
     - **Dimension Tables:** Include `Dim_Date`, `Dim_Time`, `Dim_Location`, `Dim_Vehicle`, `Dim_Person`, and `Dim_Cause`, each representing a specific aspect of the collisions.
   - **Primary Keys:** Unique collision and person IDs serve as primary keys in staging and integration layers, with surrogate keys used for consistency across tables.
   - **Surrogate and Foreign Keys:** Surrogate keys (SK) are assigned to maintain relational integrity, and foreign keys (FK) establish relationships between fact and dimension tables.

### 5. **Data Loading**

   - **Loading Staging Data into Integration Layer:** Talend is used to transfer cleansed staging data into the dimensional model. This process involves mapping staging columns to dimension and fact tables, and updating reference keys.
   - **Job Scheduling and Monitoring:** ETL jobs are scheduled in Talend, ensuring data is regularly refreshed, with monitoring for error tracking and performance optimization.

### 6. **Analytics and Business Intelligence**

   - **Integration Schema for Querying:** Queries are executed on the integration schema to generate metrics for analytics and reporting purposes.
   - **Dashboards:** Power BI and Tableau dashboards provide insights on collision trends, high-risk areas, vehicle types involved, and injuries/fatalities by role (e.g., pedestrian, driver). 
   - **Business Questions:** The model addresses business questions, including:
     - Annual collision statistics by borough and time of day.
     - Most frequent causes of collisions and fatality trends.
     - Analysis of incidents involving specific vehicle types and road users (e.g., pedestrians, cyclists).

## Key Insights and Metrics

- **Collision Counts:** Track monthly and yearly trends in collision frequency.
- **Fatalities and Injuries:** Breakdown of collision outcomes by role and vehicle type.
- **Time Analysis:** Insights on peak collision times, including morning/evening rush hours.
- **Geographic Trends:** Identification of high-risk locations based on collision frequency.
