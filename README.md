\# E-Commerce Intelligence Dashboard — Power BI



An end-to-end \*\*Business Intelligence and Data Analytics project\*\* built using Microsoft Power BI and an Indian e-commerce dataset.



The project transforms raw order data into an interactive dashboard covering sales performance, profitability, customers, products, geography, and target achievement.



\---



\## 📊 Project Overview



This Power BI project analyzes:



\- Sales performance

\- Profitability

\- Customer behavior

\- Product and sub-category performance

\- Geographic sales distribution

\- Monthly sales trends

\- Sales targets and achievement

\- Business KPIs



The goal is to demonstrate practical skills in \*\*data modeling, DAX, data visualization, business analysis, and dashboard design\*\*.



\---



\## 🛠️ Technologies Used



| Technology | Purpose |

|---|---|

| Microsoft Power BI | Dashboard and visualization |

| Power Query | Data cleaning and transformation |

| DAX | Measures and business calculations |

| CSV | Source datasets |

| Git \& GitHub | Version control and portfolio |



\---



\## 📁 Dataset



The project uses three datasets:



\### List of Orders

Contains order-level information:



\- Order ID

\- Order Date

\- Customer Name

\- State

\- City



\### Order Details

Contains transaction-level information:



\- Order ID

\- Amount

\- Profit

\- Quantity

\- Category

\- Sub-Category



\### Sales Target

Contains monthly sales targets by category.



\---



\## 🧮 Key DAX Measures



The dashboard includes measures such as:



\- Total Sales

\- Total Profit

\- Total Orders

\- Total Customers

\- Average Order Value

\- Profit Margin %

\- Sales Target

\- Target Achievement %

\- Sales Variance

\- Profit per Order

\- Average Quantity per Order

\- Orders per Customer



\---



\## 📈 Dashboard Pages



\### 1. Executive Overview

Provides a high-level summary of:



\- Sales

\- Profit

\- Orders

\- Customers

\- Average Order Value

\- Profit Margin

\- Monthly sales trends

\- Sales vs target

\- Category performance

\- State performance



\### 2. Sales \& Profit Analysis

Analyzes:



\- Sales by sub-category

\- Profit by sub-category

\- Monthly sales

\- Monthly profit

\- Category and sub-category performance



\### 3. Customer Intelligence

Analyzes:



\- Customer count

\- Orders per customer

\- Top customers

\- Customer sales by state

\- Customer sales by category

\- Customer sales trends



\### 4. Product Intelligence

Analyzes:



\- Product category performance

\- Sub-category sales

\- Sub-category profit

\- Quantity sold

\- Profit margins



\### 5. Geographic Analysis

Analyzes:



\- Sales by state

\- Profit by state

\- Sales by city

\- Geographic performance



\### 6. Target \& Performance

Analyzes:



\- Actual sales vs target

\- Target achievement

\- Sales variance

\- Category-level performance



\---



\## 🏗️ Data Model



The project uses a relational Power BI data model with:



\- `Orders`

\- `OrderDetails`

\- `SalesTargets`

\- `DimDate`

\- `DimCategory`

\- `DimMonth`



The model uses relationships between order, transaction, date, category, and target data to support interactive filtering and analysis.



\---



\## 🔄 Data Preparation



The raw data was prepared using Power Query.



Main transformations included:



\- Removing blank order records

\- Setting appropriate data types

\- Cleaning date fields

\- Preparing dimension tables

\- Creating relationships between datasets

\- Building a dedicated date dimension



\---



\## 🎯 Business Questions



The dashboard is designed to answer questions such as:



1\. How much revenue is being generated?

2\. How profitable is the business?

3\. Which categories and sub-categories generate the most sales?

4\. Which products contribute the most profit?

5\. Which states and cities generate the most revenue?

6\. Who are the highest-value customers?

7\. How are sales changing over time?

8\. Are sales meeting monthly targets?

9\. Which categories are above or below target?

10\. How efficiently is the business converting orders into revenue and profit?



\---



\## 📂 Project Structure



```text

E-Commerce-Intelligence-PowerBI/

│

├── Dataset/

│   ├── List of Orders.csv

│   ├── Order Details.csv

│   └── Sales target.csv

│

├── Documentation/

│

├── PowerBI/

│   └── E-Commerce-Intelligence-PowerBI.pbix

│

├── Python/

│

├── Screenshots/

│

├── SQL/

│

├── .gitignore

└── README.md

🚀 Skills Demonstrated
- Power BI
- Power Query
- DAX
- Data Cleaning
- Data Modeling
- Data Visualization
- Business Intelligence
- KPI Development
- Exploratory Data Analysis
- Customer Analytics
- Sales Analytics
- Profitability Analysis
- Geographic Analysis

👨‍💻 Author
Vaibhav Haldankar
Computer Science / MCA Graduate
Interested in AI/ML Engineering, Data Analytics, and Business Intelligence.
GitHub: NIGHTFURY-999
📌 Project Status
🚧 Actively developing
The dashboard and documentation will continue to be improved with additional analysis, screenshots, and insights.

