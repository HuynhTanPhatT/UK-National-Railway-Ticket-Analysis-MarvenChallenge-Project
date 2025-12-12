# 🚂UK-National-Railway-Ticket-Analysis (12/2023 - 05/2024)
- Author: Huỳnh Tấn Phát
- Date: 12/2025
- Tool Used: **Python**, **Power Bi**
  - `Python`: Pandas, Numpy, Datetime
  - `Power Bi`: Dax, calculated columns, data visualization, data modeling
# ReadMe - Table Of Contents (TOCS)
1. [Executive Summary & Background & Objectives]()
2. [Dataset Description]()
3. [Data Processing & Metric Definations (Dax)]()
4. [Key Insights & Visualization]()
5. [Recommendations]()
# 📌Background & Objective
## Executive Summary:
- This project provides an exploratory dashboard of National Rail's data to inform Manager with data-driven insights to:
  - Understand current business performance
  - Enhance service efficiency
  - Optimize scheduling
  - Improve customer satisfaction

## BackGround:
- During `12/2023` - `04/2024`, a company provides business services to passenger train operators in UK recorded **+30.000** ticket transactions through two main purchases: `Online` and `Station`.

## Challenge Objectives:
1. Analyze revenue from different ticket types & classes
2. Identify the most popular routes
3. Determine peak travel times
4. Diagnose on-time performance and contributing factors

🕵🏼‍♂️Who is this project for ?
- Manager of National Rail Service
- Operation Team

# 📂Dataset Description
## 📌Data Source:
- Source:
    - [Kaggle](https://www.kaggle.com/datasets/motsimaslam/national-rail-uk-train-ticket-data)
    - [Maven Anlytics](https://mavenanalytics.io/challenges/maven-rail-challenge)
- Size: The **Ticket** table contains **31.653** records with **18** fields
- Format: CSV

## 📊Data Structure & Relationships
1️⃣Table Used
- x
  
2️⃣Data Relationships
<img width="1352" height="664" alt="image" src="https://github.com/user-attachments/assets/fb70e694-d34d-43a1-a83e-484234f8a6ca" />

- x

# Data Processing by Python & Power Bi

1. Using [Python](https://github.com/HuynhTanPhatT/UK-National-Railway-Ticket-Analysis/tree/main/Python%3A%20Data%20Cleaning) to:
> - **Data Cleaning**: check data quality, handle null values, convert data types, detect anomalies, recreate columns and update values.
2. Using Power Bi to:
> - ETL
> - DAX Calculations & Formulas

- `🔶Employ some several DAX formulas to calculate Key Performance Indicators (KPIs)`:
<details>
  <summary>Click to view examples of DAX formulas</summary>
  <br>

- **Ticket Sales**:
```dax
1_ticket_sales = COUNT(FactTable[transaction_id])

1_Avg_TicketSales = AVERAGEX(VALUES(FactTable[departure_time]),CALCULATE(COUNTROWS(FactTable)))

1_cancelled_ticket_sales = CALCULATE(
    COUNT(FactTable[transaction_id]),
    FILTER(FactTable,FactTable[journey_status] = "Cancelled"))

1_refunded_ticket_sales = CALCULATE(
    COUNTROWS(FactTable),
    FILTER(FactTable,FactTable[refund_requested] = "Yes"))

2_average_price_per_ticket (APT) = 
DIVIDE([2_gross_revenue],[1_ticket_sales])
```

- **Revenue**:
```dax
2_gross_revenue = sum(FactTable[ticket_price])

2_net_revenue = //ticket_sold * price (actual earned)
CALCULATE(
    SUMX(FactTable,FactTable[ticket_price]),
    FactTable[refund_requested] = "No")

2_refund_revenue = CALCULATE(
    SUM(FactTable[ticket_price]),
    FILTER(FactTable,FactTable[refund_requested] = "Yes"))
```
</details>

- `🔶Employee some several DAX Formulas to calculate Customer Measures`:
<details>
    <summary>Click to view examples of DAX formulas</summary>
    <br>

- **Total Daily Train Trips**: Đếm tất cả các chuyến trong dataset, có bao nhiêu chuyến đến đúng giờ | trễ | hủy 
```dax
3_daily_train_trips = 
VAR total_train_trips = 
    SUMMARIZECOLUMNS(
        DimDate[Date],
        DimStation[route],
        "Trips", DISTINCTCOUNT(FactTable[departure_time])
    )
RETURN
SUMX(total_train_trips, [Trips])
```

- **On-Time Train Trips**: Đếm tất cả chuyến tàu đến đúng giờ dự kiến (ability of a train to depart and arrive at their scheduled times
)
```dax
3_on-time train trips = 
VAR on_time_train_trips =
    SUMMARIZECOLUMNS(
        DimDate[Date],
        DimStation[route],
        FILTER(FactTable,FactTable[journey_status] = "On Time"),
        "Trips", DISTINCTCOUNT(FactTable[departure_time]))
RETURN
SUMX(on_time_train_trips, [Trips])
```

- **Delayed Train Trips**
```dax
3_delayed train trips = 
VAR delayed_train_trips =
    SUMMARIZECOLUMNS(
        DimDate[Date],
        DimStation[route],
        FILTER(FactTable,FactTable[journey_status] = "Delayed"),
        "Trips", DISTINCTCOUNT(FactTable[departure_time]))
RETURN
SUMX(delayed_train_trips, [Trips])
```

- **On-Time Performance (OTP): The percentage of recorded station stops where the train arrived less than one minute later than its advertised time.
```dax
4_on-time performance = (Number of Trips On Time / Total Number of Trips arrived Train Stops) x 100
DIVIDE( -- On-Time + Delayed  không thêm Cancelled, bởi vì chuyến tàu bị hủy không đi tới "train stops"
    [3_on-time train trips],
    [3_on-time train trips] + [3_delayed train trips])
```
</details>



# 📊Key Insights & Visualizations
## I. Railway Train Ticket | Overview
<img width="1301" height="730" alt="image" src="https://github.com/user-attachments/assets/054a7554-c65a-4abb-be9c-693356ce326c" />

## 📌Key Findings:
1. **Ticket Sales & Revenue Overview**:
    - From 12/2023 -> 05/2024, the company sold **⇈31.00K** tickets, bringing in ~**742K** USD in **gross revenue** with an average ticket price of **23.44** USD.
    - However, due to operational issues (weather, technical issues,etc..), **1.12K** tickets were refunded, leading to a revenue loss of **38.70K**.

    => **`The revenue loss mainly from operational issues by improving them could increase net revenue, while enhancing the customer experience.`**

2. **Ticket Purchases**:
    - Online purchases account for **59.32%** of all tickets (**18.11K**), mainly because of `lower average ticket price` compared to Station purchases (**$20.67** vs. **$27.35**)
    - Although, Online sold **5.3K** more tickets than Station, the total revenue gap is small (**374.54K** vs. **328.68K**)

3. **Passengers prefer low-priced tickets**:
    - Standard class tickets make up **90%** of total sales (**27.59K** tickets at $20.72) across both purchase type, bringing about ~**560K (~80%)** in revenue -- with Advance tickets being the most common type (**55.27%**) within this class.

    => **`The UK ticket market prefers low-cost purchase options such as Standard (Advance)`**

4. **Routes**:
    - The top 5 highest-selling routs are around areas: **Manchester-London-Birmingham**.


## II. Railway Train Ticket | Passenger Analysis: Peak Travel Times
<img width="1290" height="725" alt="image" src="https://github.com/user-attachments/assets/0c546423-b09f-49a6-83a6-61bad23a4212" />

## 📌Key Findings:

1. **Passenger Demand across the Week**:
    - Passenger demand is mainly concentrated on weekdays (Business days), higher than weekends, with 7K passengers.
    - Howver, the different between Peak Hours and Off-Peak Hours on both Business days and Weekends is not significant (10.43K vs. 11.43K) and (4.19K vs. 4.48K).
    - The highest passenger volume occurs in the morning (5AM-12PM), with 12.04K passengers (39.44%), and the difference between AM and PM demand is minimal.

2. **Peak Time Windows**:
    - Passenger volume increases sharply during two main time windows: `6-8 AM` and `4-6 PM`, aliging with daily activities: commuting to work or school.
    - In contrast, Off-Peak Hours remain below 1,500 passengers per hour

  => **`Passenger demain concentrated by during peak hours.`**

3. **The distribution of passengers by Time Period**:
    - Passenger volume remains stable, ranging from 2.000-2.300 in both the AM and PM periods.

4. **Time Slots within Peak Hours**:
    - Morning: `6:30 AM` && `8:00 AM` accounted for (**17.74%** - **1.409** passengers) && (**16.68%** - **1.369** passengers)
    - Evening:  `5:45 PM` && `6:45 PM` accounted for (**20.75%** - **1.165** passengers) & (31.91**%** - **2.545** passengers)**

    => Train services remain stable, but it fluctuates significantly at specific time slots within the peak hours.

## III. Railway Train Ticket | Operation Analysis: Diagnose on-time performance and contributing factors
<img width="1297" height="719" alt="image" src="https://github.com/user-attachments/assets/97bbe8a6-cd30-47d4-9691-b8a04f5c52cc" />


# 💡Recommendations

