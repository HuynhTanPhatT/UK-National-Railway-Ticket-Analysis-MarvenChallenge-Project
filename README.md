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

## Background:
- During `12/2023` - `04/2024`, a company provdes business services to passenger train operators in UK recorded +30.000 ticket transactions through two main purchase option: Online and Station.

## Challenge Objective:
1. Analyze revenue from different ticket types & classes
2. Determine peak travel times
3. Identify the most popular routes
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


2. Using [Power BI]() to:
   - 
   - DAX Calculations & Formulas



# Key Insights & Visualizations
## I. Railway Train Ticket | Overview
<img width="1293" height="724" alt="image" src="https://github.com/user-attachments/assets/cdafd18c-5cfc-4853-9622-7e50f6a08019" />

##📌Key Findings:
1. **Ticket Sales & Revenue Overview**
- From 12/2023 -> 05/2024, the company sold **⇈31.00K** tickets, bringing in ~**742K** USD in **gross revenue** with an average ticket price of **23.44 USD. However, due to operational issues (weather, technical issues,etc..), 2.43K tickets were refunded, leading to a revenue loss of **71.65K**.

=> The revenue loss mainly from operational issues by improving them could increase **net revenue**, while enhancing the customer experience.

2. **Online Ticket purchases increase significantly, but Revenue remain as Station purchase**
- Online purchases account for **59.04%** of all tickets (**17.26K**), mainly because of lower average ticket price compared to Station purchases (**$20.67** USD vs. **$27.35** USD)
- Although, Online sold **5.3K** more tickets than Station, the total revenue gap is small (**359.06K** vs. **311.25K**)

3. **Passengers'need prefer low-price ticket**
- Standard class tickets make up 90% of total sales (**26.41K** tickets at $20.72) across both purchase type, bringing about ~**534.39K (79.72%)** in revenue -- with Advance tickets being the most common type within this class.

=> The UK ticket market prefers low-cost purchase options such as Standard (Advance)

⇒ Doanh thu hiện tại vẫn không chênh lệch đáng kể, nhưng về dài  thì First-Class và loại vé Anytime sẽ bị ảnh hưởng bởi nhu cầu này.

4. **Routes**
- The top 5 highest-selling routs are around areas: **Manchester-London-Birmingham**.


## II. Railway Train Ticket | Passenger Analysis: Peak Travel Times
<img width="1297" height="721" alt="image" src="https://github.com/user-attachments/assets/c062c446-f25c-4c42-b130-fe6974850517" />




# 💡Recommendations

