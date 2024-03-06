# PWC Power BI Virtual internship Task 2 - Customer Churn Retention

![PwC Power BI Virtual Case Experience](https://user-images.githubusercontent.com/118357991/227788348-b988c4df-7923-46d6-8af7-102b8042f721.png)

## Problem Statement :

The purpose of this task is to:

- Define proper KPI's
- Create a dashboard for the retention manager reflecting the KPI's
- Write a short email to him (the engagement partner) explaining your findings, and include suggestions as to what needs to be changed
- Customers who left within the last month
- Services each customer has signed up for: phone, multiple lines, internet, online security, online backup, device protection, tech support, and streaming TV and movies
- Customer account information: how long as a customer, contract, payment method, paperless billing, monthly charges, total charges and number of tickets opened in the categories administrative and technical
- Demographic info about customers – gender, age range, and if they have partners and dependents

## Datasource:

Dataset: [02 Churn-Dataset.xlsx](https://github.com/sonali-guptaa/customer_retention_analysis/files/14509440/02.Churn-Dataset.xlsx)

## Data Preparation:

Completed the Data transformation in Power Query and the dataset is then loaded into Microsoft Power BI Desktop for visualization.

## Dataset Description:

Customer Churn dataset contains `23 columns and 7043 rows` of observation. Dataset includes columns like:

customerID: Customer ID
gender: gender (female, male)
SeniorCitizen: Whether the customer is a senior citizen or not (1, 0)
Partner: the customer has a partner or not (Yes, No)
Dependents: Whether the customer has dependents or not (Yes, No)
tenure: Number of months the customer has stayed with the company
PhoneService: Whether the customer has a phone service or not (Yes, No)
MultipleLines: Whether the customer has multiple lines or not (Yes, No, No phone service)
InternetService: Customer’s internet service provider (DSL, Fiber optic, No)
OnlineSecurity: Whether the customer has online security or not (Yes, No, No internet service)
OnlineBackup: Whether the customer has online backup or not (Yes, No, No internet service)
DeviceProtection: Whether the customer has device protection or not (Yes, No, No internet service)
TechSupport: Whether the customer has tech support or not (Yes, No, No internet service)
StreamingTV: Whether the customer has streaming TV or not (Yes, No, No internet service)
StreamingMovies: Whether the customer has streaming movies or not (Yes, No, No internet service)
Contract: The contract term of the customer (Month-to-month, One year, Two year)
PaperlessBilling: Whether the customer has paperless billing or not (Yes, No)
PaymentMethod: The customer’s payment method (Electronic check, Mailed check, Bank transfer (automatic), Credit card (automatic))
MonthlyCharges: The amount charged to the customer monthly
TotalCharges: The total amount charged to the customer
Churn: Whether the customer churned or not (Yes or No)

## Data Cleaning

Data Cleaning for the dataset was done in the power query editor as follows:

- Added a conditional column named `Duration` to divide the tenure into the groups of 0-1 year, 1-2 year, 2-3 year, 3-4 year, 4-5 year and 5-6 year.

![1](https://github.com/sonali-guptaa/customer_retention_analysis/assets/151986702/7f6f06ce-1342-46a5-8b6f-1a729feeac9c)

- Each of the columns in the table were validated to have the correct data type too.

## Calculated Measures created using DAX:

Measures used in  all visualization are:

- Average MonthlyCharges = `AVERAGE('Churn-Dataset'[MonthlyCharges])`

- Average Tenure = `AVERAGE('Churn-Dataset'[tenure])`

- Average TotalCharges = `AVERAGE('Churn-Dataset'[TotalCharges])`

- Churn rate = `DIVIDE(COUNTROWS(FILTER('Churn-Dataset', 'Churn-Dataset'[Churn] = "Yes")), COUNTROWS('Churn-Dataset'))`

- Churned customer count = `CALCULATE(DISTINCTCOUNT('Churn-Dataset'[customerID]), 'Churn-Dataset'[Churn] = "Yes")`

- Dependent in % = `DIVIDE(CALCULATE(COUNT('Churn-Dataset'[Dependents]), 'Churn-Dataset'[Dependents]="Yes",'Churn-Dataset'[Churn]="Yes"), CALCULATE(COUNT('Churn-Dataset'[Dependents]),'Churn-Dataset'[Churn]="Yes"), 0)`

- Device protection in % = `DIVIDE(CALCULATE(COUNT('Churn-Dataset'[DeviceProtection]), 'Churn-Dataset'[DeviceProtection] ="Yes", 'Churn-Dataset'[Churn]="Yes"),CALCULATE(COUNT('Churn-Dataset'[DeviceProtection]),'Churn-Dataset'[Churn]="Yes"),0)`

- Monthly Revenue = `SUMX('Churn-Dataset', 'Churn-Dataset'[MonthlyCharges])`

- Not churned customer count = `COUNTX(FILTER('Churn-Dataset' , 'Churn-Dataset'[Churn] = "No"), 'Churn-Dataset'[Churn])`

- Online backup in % = `DIVIDE(CALCULATE(COUNT('Churn-Dataset'[OnlineBackup]), 'Churn-Dataset'[OnlineBackup] ="Yes", 'Churn-Dataset'[Churn]="Yes"),CALCULATE(COUNT('Churn-Dataset'[OnlineBackup]),'Churn-Dataset'[Churn]="Yes"),0)`

- Online security in % = `DIVIDE(CALCULATE(COUNT('Churn-Dataset'[OnlineSecurity]), 'Churn-Dataset'[OnlineSecurity] ="Yes", 'Churn-Dataset'[Churn]="Yes"),CALCULATE(COUNT('Churn-Dataset'[OnlineSecurity]),'Churn-Dataset'[OnlineSecurity]="Yes"),0)`

- Partner in % = `DIVIDE(CALCULATE(COUNT('Churn-Dataset'[Partner]),'Churn-Dataset'[Partner]="Yes",'Churn-Dataset'[Churn]="Yes"), CALCULATE(COUNT('Churn-Dataset'[Partner]), 'Churn-Dataset'[Churn]="Yes"), 0)`

- Phone service in % = `DIVIDE(CALCULATE(COUNT('Churn-Dataset'[PhoneService]), 'Churn-Dataset'[PhoneService] ="Yes", 'Churn-Dataset'[Churn]="Yes"),CALCULATE(COUNT('Churn-Dataset'[PhoneService]),'Churn-Dataset'[Churn]="Yes"),0)`

- Retention rate = `1 - 'Churn-Dataset'[Churn rate]`

- SenioCitizen in % = `DIVIDE(CALCULATE(COUNT('Churn-Dataset'[SeniorCitizen]),'Churn-Dataset'[SeniorCitizen]=1,'Churn-Dataset'[Churn]="Yes"), CALCULATE(COUNT('Churn-Dataset'[SeniorCitizen]),'Churn-Dataset'[Churn]="Yes"), 0)`

- Streaming Movies in % = `DIVIDE(CALCULATE(COUNT('Churn-Dataset'[StreamingMovies]), 'Churn-Dataset'[StreamingMovies] ="Yes", 'Churn-Dataset'[Churn]="Yes"),CALCULATE(COUNT('Churn-Dataset'[StreamingMovies]),'Churn-Dataset'[Churn]="Yes"),0)`

- Streaming TV in % = `DIVIDE(CALCULATE(COUNT('Churn-Dataset'[StreamingTV]), 'Churn-Dataset'[StreamingTV] ="Yes", 'Churn-Dataset'[Churn]="Yes"),CALCULATE(COUNT('Churn-Dataset'[StreamingTV]),'Churn-Dataset'[Churn]="Yes"),0)`

- Tech Support in % = `DIVIDE(CALCULATE(COUNT('Churn-Dataset'[TechSupport]), 'Churn-Dataset'[TechSupport] ="Yes", 'Churn-Dataset'[Churn]="Yes"),CALCULATE(COUNT('Churn-Dataset'[TechSupport]),'Churn-Dataset'[Churn]="Yes"),0)`

## Data Visualization (Dashboard):

Dashboard created using the calculated measures in Microsoft Power BI Desktop:

Customer Churn
![2](https://github.com/sonali-guptaa/customer_retention_analysis/assets/151986702/41e070db-4a23-4ffd-ae95-f8e76737d3be)

Customer Risk
![3](https://github.com/sonali-guptaa/customer_retention_analysis/assets/151986702/7d9f05a1-6391-42b2-a7e3-8532a934e02c)

Services
![4](https://github.com/sonali-guptaa/customer_retention_analysis/assets/151986702/dd4b184a-eb99-46d6-993b-f4508d3776a6)

Insights
![5](https://github.com/sonali-guptaa/customer_retention_analysis/assets/151986702/653d6f77-a197-4505-b552-6ad0d7bf77ec)

Recommendations:
![6](https://github.com/sonali-guptaa/customer_retention_analysis/assets/151986702/c62c9eb1-7ef7-4eb4-a50c-935d8bcb3618)

## Insights:

As per the visualizations, it has been deduced that :

· Customers with Two-Year contract, have stayed longer with the company as compared to the customers who are in Month-to-Month contract with it.

· Total 7043 customers joined the company out of which 5174 stayed with it. The churn

rate is 26.54% for the remaining 1869 customers who churned.

· Total yearly charges are $16.06M and monthly charges are $456.12K and total 2955 tech tickets and 3632 admin tickets were opened.

· Most of the churned customers didn't sign up for the services like Online Security, tech support, internet service and online backup.

· A lot of customers had an issue with Fiber Optic. Up to 42% of the customers who churned were using Fiber Optic as their Internet Services.

· Also, streaming TV and streaming movies services didn’t have much impact on the people leaving or staying with the company.

## Recommendation:

Some recommendations based on the analysis are:

· The Company could try convincing customers to subscribe to One-Year and Two-Year contract.

· Also, customers should be encouraged to sign up for the services like online security, tech support, online backup and internet service.

· Also, Increasing the sale of 1 and 2 year contract by 5% each and Yearly increase of automatic payments by 5% will be beneficial for the company.

· Also, the company should look into the issues they are facing who opted for fiber optic internet service.

·  Also, the company should look into the issues that people are facing with the electronic check payment method as the churn rate for this method is higher than others.

---
