# Project: Credit_Card_Weekly_Insights_Dashboard

# Table of content 
- Introduction
- Objective
- Tools and Technologies 
- Data Analysis
- Data Modeling
- Data Analysis (DAX)
- Build Dashboard or report
- Project Insights 

# Introduction:
In the rapidly evolving financial services industry, the ability to effectively monitor and analyze credit card operations is crucial for maintaining competitive advantage and ensuring customer satisfaction. This project focuses on developing a Credit Card Weekly Insights Dashboard using Power BI, to visualize and analyze credit card transaction data stored in a MySQL database.
The dashboard provides a comprehensive overview of credit card performance metrics on a weekly basis. The dashboard enables stakeholders to gain real-time insights into transaction volumes, revenue generation, and customer behavior. This information is essential for making informed decisions, identifying areas for improvement, and enhancing overall credit card operations.

# Objective:
The primary objective of this project is to develop a comprehensive and interactive Credit Card Weekly Insights Dashboard using Power BI. This dashboard aims to provide real-time insights into key performance metrics and trends related to credit card operations.By leveraging data from a MySQL database, the dashboard will enable stakeholders to Monitor and analyze weekly credit card transactions and also track key performance indicators (KPIs) such as total transactions, revenue and average transaction value.

#  Tools and Technologies:
- MySQL
- Microsoft Power BI
- Power Query and DAX 

# Data Analysis using Power BI:

1. Data Extraction:
   Database Connection: Use Power BI MySQL connector to establish a connection to the MySQL database.

2. Data Cleaning:
   Use Power Query Editor in Power BI to clean and transform the data. This includes handling missing values, removing duplicates, and converting data types.

3. Data Transformation:
   To facilitate analysis and create useful visualizations, additional transformations and calculations are necessary.

     - Create Relationships: In the "Model" view, create a relationship between the Credit details and Cust details tables based on the Client_Num column.

# Data Modeling:

And then dataset was cleaned and transformed, it was ready to the data modeled.

![Data model](https://github.com/prajaktakadu11/Credit_Card_Weekly_Insights_Dashboard/blob/main/Data/Data%20model.PNG)

# Data Analysis (DAX):

Key Measures:
 1. AgeGroup: To categorize customers into different age groups.
 ```
 AgeGroup = SWITCH(
 TRUE(),
 'cust_detail'[customer_age] < 30, "20-30",
 'cust_detail'[customer_age] >= 30 && 'cust_detail'[customer_age] < 40, "30-40",
 'cust_detail'[customer_age] >= 40 && 'cust_detail'[customer_age] < 50, "40-50",
 'cust_detail'[customer_age] >= 50 && 'cust_detail'[customer_age] < 60, "50-60",
 'cust_detail'[customer_age] >= 60, "60+",
 "unknown"
 )
```

 2.IncomeGroup: To categorizes the income into three groups: Low, Medium, and High.
 ```
 IncomeGroup = SWITCH(
 TRUE(),
 'cust_detail'[income] < 35000, "Low",
 'cust_detail'[income] >= 35000 && 'cust_detail'[income] <70000, "Med",
 'cust_detail'[income] >= 70000, "High",
 "unknown"
 )
 ```

3. week_num2: To extracts the week number from a date column in dataset
```
week_num2 = WEEKNUM('credit_details'[week_start_date])
```

4. Revenue: To calculate the total revenue based on the annual fees, total transaction amount, and interest earned.
```
Revenue = 'credit_details'[annual_fees] + 'credit_details'[total_trans_amt] + 'credit_details'[interest_earned]
```

5. Current week revenue : To calculate the revenue for the current week.
 ```
 Current_week_Revenue = CALCULATE(
 SUM('credit_details'[Revenue]),
 FILTER(
 ALL('credit_details'),
 'credit_details'[week_num2] = MAX('credit_details'[week_num2]))) 
  ```

6. Previous_week_Reveneue = To calculate the revenue for the previous week.
```
 Previous_week_Reveneue = CALCULATE(
 SUM('credit_details'[Revenue]),
 FILTER(
 ALL('credit_details'),
 'credit_details'[week_num2] = MAX('credit_details'[week_num2])-1))
```
7. Week over week revenue :  To calculate the Week-over-Week (WoW) revenue growth
 ```
[ WOW_revenue = DIVIDE(
 (credit_details[Current_Week_revenue]-credit_details[Previous_Week_revenue]),
 credit_details[Previous_Week_revenue])
 ```

# Build Dashboard or report:

![Credit card transaction dashboard](https://github.com/prajaktakadu11/Credit_Card_Weekly_Insights_Dashboard/blob/main/Data/Credit%20card%20transaction%20report.PNG)

![Credit card customer dashboard](https://github.com/prajaktakadu11/Credit_Card_Weekly_Insights_Dashboard/blob/main/Data/Credit%20card%20customer%20report.PNG)

# Project Insights:
  The Credit Card Weekly Insights Dashboard provides a powerful tool for stakeholders to monitor and analyze credit card operations. Key insights include:

  - Transaction Trends: Visualization of daily transaction volumes helps identify peak transaction times and patterns.
  - Revenue Analysis: Insights into total revenue and average transaction values aid in financial analysis.
  - Male customers are contributing more in revenue is 31M, and female 26M.
  - TX, NY & CA is contributing to 68% in revenue.
