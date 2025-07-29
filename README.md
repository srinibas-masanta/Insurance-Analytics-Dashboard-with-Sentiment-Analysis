# 📊 Insurance Analytics Dashboard w/ Sentiment Analysis

This project presents an end-to-end analytical solution built in **Power BI** for an insurance company. It combines insurance policy and claims data with customer sentiment data to provide rich, interactive dashboards and data insights. It includes visuals on policy performance, claim distribution, customer demographics, and feedback sentiment, enabling data-driven decision-making.

---

## 📁 Dataset Description

The dataset used in this project comprises **insurance policy records**, **customer demographics**, and **claim details**. It includes \~10,000 rows of structured data imported from a flat file into Microsoft SQL Server and further processed using Power BI.

### Main columns include:

* **PolicyNumber**: Unique ID for each policy
* **CustomerID**: Unique identifier for each customer
* **Gender**: Customer's gender (Male/Female)
* **Age**: Customer's age
* **PolicyType**: Type of policy (e.g., Auto, Travel, Life, etc.)
* **PolicyStartDate / PolicyEndDate**: Duration of the policy
* **PremiumAmount**: Premium paid by the customer
* **CoverageAmount**: Maximum amount covered under the policy
* **ClaimNumber**: Unique ID for each claim
* **ClaimDate**: Date when the claim was filed
* **ClaimAmount**: Amount claimed
* **ClaimStatus**: Status of the claim (Rejected, Pending, Settled)

Additional customer feedback data (Excel) was used for **sentiment analysis** in the final part of the dashboard.

---

## 🛠️ Tools & Technologies Used

* **Microsoft SQL Server** – Data storage and import
* **Power BI Desktop** – Visualization and dashboard creation
* **Power Query Editor** – Data cleaning and transformation
* **Text Analytics (Power BI AI)** – Sentiment analysis on feedback data

---

## ⚙️ Data Preparation Process

### 1. **SQL Server as a Data Source**

* Created a new database in **Microsoft SSMS**
* Imported the flat file and adjusted data types accordingly
* Queried and validated data before connecting to Power BI

### 2. **Power BI Data Connection**

* Connected to the SQL Server database using **Import Mode**
* Previewed and transformed data in **Power Query Editor**
* Loaded 10,000 rows of structured insurance data for reporting

### 3. **Data Transformations in Power Query**

#### a. **Age Group Column** (for Claim Amount by Age Group line chart):

```powerquery
= Table.AddColumn(#"Removed Duplicates", "Age Group", each 
  if [Age] <= 25 then "Young Adult" 
  else if [Age] <= 44 then "Adult" 
  else if [Age] <= 59 then "Middle Age" 
  else "Old Age")
```

#### b. **Active/Inactive Policy Column** (for Donut Chart):

```powerquery
= Table.AddColumn(#"Changed Type", "Custom", each 
  if [PolicyEndDate] <= #date(2024, 12, 6) then "Inactive" 
  else "Active")
```

---

## 📈 Dashboard Pages

### 🔹 **Page 1 – Interactive Insurance Dashboard**

**Visuals Created:**

* 📊 *Stacked Bar Chart*: **Premium Amount by Policy Type**
* 📈 *Line Chart*: **Claim Amount by Age Group**
* 📉 *Ribbon Chart*: **Number of Claims by Claim Status**
* 🍩 *Donut Chart*: **Count of Active/Inactive Policies**
* 🧮 *Matrix Table*: **Coverage Distribution by Policy Type and Claim Outcome**

**KPI Cards:**

* **Total Premium Amount**
* **Total Coverage Amount**
* **Total Claim Amount**

**Slicers:**

* PolicyNumber
* ClaimNumber
* CustomerID

### 🔹 **Page 2 – Drill-Through Detail Page**

* Table displaying all policy, customer, and claim-related columns
* **Drill-through Filters**: PolicyType, Active/Inactive
* Enabled interactivity between visuals on page 1 and this detail view
* Power BI auto-generates a **back button** for easy navigation

🔍 *Purpose*: Enables users to click on a chart element (e.g., policy type) and view detailed associated records.

### 🔹 **Page 3 – Sentiment Analysis**

* Uploaded an Excel file containing **customer feedback**
* Used **Text Analytics > Score Sentiment** in Power BI
* A new column with sentiment scores (0 to 1) was generated

**Conditional Column to Categorize Sentiment:**

```powerquery
if [Sentiment Score] >= 0.8 then "Excellent"
else if [Sentiment Score] >= 0.6 then "Good"
else "Needs Improvement"
```

**Visuals Created:**

* ☁️ *Word Cloud*: Highlights most frequently used words in feedback
* 📝 *Feedback Table*: Detailed view of customer feedback with sentiment score and category
* 📊 *Stacked Bar Chart*: Count of Customer Name by Feedback Category

---

## 🎯 Key Insights

* **Travel Insurance** generates the highest premium and coverage.
* **Old Age** group contributes the highest claim amount, highlighting an age-related risk pattern.
* **Rejected Claims** form the majority of claim statuses, indicating potential issues in claim approval processes.
* **40%** of policies are **inactive**, signaling an opportunity for retention or remarketing.
* Sentiment analysis reveals that not all feedback is positive — categories like "Needs Improvement" provide actionable insights for customer experience teams.

---

## 🚀 Features & Interactivity

* Dynamic filtering using slicers
* Drill-through navigation from summary to detailed views
* AI-powered sentiment scoring of customer feedback
* Real-time insights via KPIs and visual storytelling

---

## 📌 Conclusion

This Power BI project demonstrates how to connect, transform, and visualize complex insurance data using SQL Server and Power BI, while also incorporating AI-driven sentiment insights. It offers a comprehensive view of both **operational performance** and **customer experience**, making it a powerful reporting tool for insurance analytics.
