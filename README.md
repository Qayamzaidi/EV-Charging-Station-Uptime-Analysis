# EV-Charging-Station-Analysis
## 📌 Project Overview

This project analyzes the operational performance of EV charging stations using Power BI. The objective is to monitor station uptime, evaluate utilization, and provide actionable insights to improve charging station availability.
## Tools Used
- Microsoft Excel
- Power BI
- Power Query
- DAX

The project includes data cleaning, data modeling, KPI development, and interactive dashboards.
## 1. Data Understanding
The project consists of three datasets representing different aspects of the EV battery swapping ecosystem.
### Dataset 1: Swap Transactions
Contains all battery swap transactions performed by customers.
### Dataset 2: Station Uptime
Contains the operational status of each battery swapping station.
### Dataset 3: Battery Inventory
Contains battery lifecycle and health information.
# 2. Data Quality Checks
Before building reports, validated all datasets for quality.

1. I have Checked all the duplicate and Missing Value(Blank values, NULL values, Missing records) we have found that Null values in the Downtime_reason so we replace Null values with NA.
2. I have found duplicate values in Station_id and city, so Removed duplicates where required.
3. I have also Checked Data Consistency (such as Station IDs, City Names, Vehicle Types,Partner Names) that categorical values were standardized.

# 3. Created Model(relationship):
There is problem in swap_transactions table, station_uptime table and battery_inventory table i.e. there is many to many relationship between these table.  
1. I have created a composite column from station_id and city using addcolumn in power query editor in swap_transactions table, station_uptime table and also created the bridge_table for one to many relationship for swap_transactions table, station_uptime table.
2.  I have also created  another bridge table for the battery_inventory table and swap_transactions table by which we created one to many relationship.
3. Also selected the cross-filter-direction to Both for some relationship.

# 4. ### Created Measures
Key DAX measures include:

- Total Swaps = COUNTROWS(swap_transactions)
- Total_Revenue = Sum(swap_transactions[revenue_inr])
- Average Swaps per Station per Day =  DIVIDE([Total Swaps],[Station-Date Count])
- Station Uptime % = DIVIDE( SUM(station_uptime[uptime_hours]),  COUNTROWS(station_uptime) * 24,0 ) * 100
- Average Battery Health = AVERAGE(battery_inventory[battery_health_pct])
- Average Charge Cycles = AVERAGE(battery_inventory[charge_cycles])

# 5. Dashboard Development
An interactive Power BI dashboard was developed.

## Executive KPIs: 
Such as
- Total Revenue
- Total Swaps
- Average Uptime
- Average Battery Health
- Average Charge Cycles

## Operational Analysis

Visualizations include:
1. Total Swap by month and Days
2. Total Revenue by city and partner
3. Total Swap by city and partner
4. Avg. Energy Consumed by Station_id

## Relationship Analysis
Analyzed relationships between:
1. Total Swap and Station_Uptime by Station_id
2. Station Utilization and Avg._Battery_Health by Station_id

# 6. Business Insights

The dashboard helps identify:
- Best performing city : Pune
- Worst performing city : Hyderabad
- Best performing partner: Platform C
- Worst performing partner: Fleet B
- Low performing station : STN_4

# 7. Program Performance Insights : Is there a visible relationship between:
1. Station Uptime and Number of Swaps: Yes, there is a visible relationship.
Looking at the top scatter plot (Total Swaps and Station Uptime % by station_id), the dashed trendline slopes upwards from left to right. This indicates a positive correlation: as the number of total swaps increases, the station uptime percentage generally tends to increase as well.
2. Battery Health and Station Utilization: Yes, there is a visible relationship.
The dashed trendline clearly slopes upward from left to right, indicating a positive correlation. This means that as station utilization increases, the average battery health typically tends to be higher as well.

# Project Outcome

This dashboard enables Program Managers to monitor EV battery swapping operations, evaluate station performance, improve battery utilization, optimize supply chain planning, and make data-driven business decisions using interactive visualizations and KPIs.
