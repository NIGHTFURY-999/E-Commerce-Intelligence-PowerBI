\# E-Commerce Intelligence Power BI — Project Documentation



\## 1. Project Objective



The objective of this project is to transform raw e-commerce transaction data into an interactive Business Intelligence dashboard.



The dashboard provides analysis across:



\- Sales

\- Profit

\- Orders

\- Customers

\- Products

\- Geography

\- Monthly performance

\- Sales targets



The project demonstrates practical implementation of Power BI data modeling, Power Query, DAX, and business-focused visualization.



\---



\# 2. Dataset



The project uses three source datasets.



\## List of Orders



Contains order and customer information.



| Column | Description |

|---|---|

| Order ID | Unique identifier for an order |

| Order Date | Date on which the order was placed |

| CustomerName | Customer associated with the order |

| State | Customer/order state |

| City | Customer/order city |



\## Order Details



Contains transaction-level information.



| Column | Description |

|---|---|

| Order ID | Links transactions to orders |

| Amount | Sales/revenue amount |

| Profit | Profit generated |

| Quantity | Number of units sold |

| Category | Product category |

| Sub-Category | Product sub-category |



\## Sales Target



Contains monthly sales targets.



| Column | Description |

|---|---|

| Month of Order Date | Target month |

| Category | Product category |

| Target | Sales target |



\---



\# 3. Data Cleaning



Power Query was used to prepare the raw datasets.



Main transformations included:



\- Removing completely blank order records

\- Validating data types

\- Converting order dates to Date format

\- Preparing category and month dimensions

\- Establishing relationships between tables

\- Preparing the data model for DAX analysis



The original `List of Orders` dataset contained blank rows that were removed during Power Query transformation.



\---



\# 4. Data Model



The Power BI model contains the following tables:



\### Fact Tables



\- `Orders`

\- `OrderDetails`

\- `SalesTargets`



\### Dimension Tables



\- `DimDate`

\- `DimCategory`

\- `DimMonth`



\## Relationships



```text

DimMonth

&#x20;  │

&#x20;  ├────────────── DimDate

&#x20;  │                  │

&#x20;  │                  └──────── Orders

&#x20;  │                              │

&#x20;  │                              └──────── OrderDetails

&#x20;  │

&#x20;  └────────────── SalesTargets



DimCategory

&#x20;  │

&#x20;  ├────────────── OrderDetails

&#x20;  │

&#x20;  └────────────── SalesTargets





Main Relationships

Orders\[Order ID]

&#x20;       1

&#x20;       │

&#x20;       \*

OrderDetails\[Order ID]



DimDate\[Date]

&#x20;       1

&#x20;       │

&#x20;       \*

Orders\[Order Date]



DimCategory\[Category]

&#x20;       1

&#x20;       │

&#x20;       \*

OrderDetails\[Category]



DimCategory\[Category]

&#x20;       1

&#x20;       │

&#x20;       \*

SalesTargets\[Category]



DimMonth\[MonthStart]

&#x20;       1

&#x20;       │

&#x20;       \*

DimDate\[MonthStart]



DimMonth\[MonthStart]

&#x20;       1

&#x20;       │

&#x20;       \*

SalesTargets\[Month of Order Date]



Relationships use a single-direction filter flow from dimensions to related fact tables.

5\. Date Dimension

A dedicated date table was created using DAX.

DimDate =

ADDCOLUMNS(

&#x20;   CALENDAR(

&#x20;       MIN(Orders\[Order Date]),

&#x20;       MAX(Orders\[Order Date])

&#x20;   ),

&#x20;   "Year", YEAR(\[Date]),

&#x20;   "Month Number", MONTH(\[Date]),

&#x20;   "Month", FORMAT(\[Date], "MMM"),

&#x20;   "Month Year", FORMAT(\[Date], "MMM YYYY"),

&#x20;   "Quarter", "Q" \& FORMAT(\[Date], "Q"),

&#x20;   "Year Month Sort", YEAR(\[Date]) \* 100 + MONTH(\[Date])

)



A month-start column was also created:

MonthStart =

DATE(

&#x20;   YEAR(DimDate\[Date]),

&#x20;   MONTH(DimDate\[Date]),

&#x20;   1

)



The Year Month Sort column ensures chronological ordering of monthly visuals.

6\. Category Dimension

The category dimension combines categories from transaction and target data.

DimCategory =

DISTINCT(

&#x20;   UNION(

&#x20;       SELECTCOLUMNS(

&#x20;           OrderDetails,

&#x20;           "Category", OrderDetails\[Category]

&#x20;       ),

&#x20;       SELECTCOLUMNS(

&#x20;           SalesTargets,

&#x20;           "Category", SalesTargets\[Category]

&#x20;       )

&#x20;   )

)



7\. Month Dimension

The month dimension provides a common monthly filtering structure.

DimMonth =

DISTINCT(

&#x20;   SELECTCOLUMNS(

&#x20;       DimDate,

&#x20;       "MonthStart",

&#x20;           DATE(

&#x20;               YEAR(DimDate\[Date]),

&#x20;               MONTH(DimDate\[Date]),

&#x20;               1

&#x20;           ),

&#x20;       "Year",

&#x20;           YEAR(DimDate\[Date]),

&#x20;       "Month Number",

&#x20;           MONTH(DimDate\[Date]),

&#x20;       "Month",

&#x20;           FORMAT(DimDate\[Date], "MMM"),

&#x20;       "Month Year",

&#x20;           FORMAT(DimDate\[Date], "MMM YYYY")

&#x20;   )

)



8\. DAX Measures

Total Sales

Total Sales =

SUM(OrderDetails\[Amount])



Calculates total revenue generated by the transactions.

Total Profit

Total Profit =

SUM(OrderDetails\[Profit])



Calculates total profit generated by transactions.

Total Quantity

Total Quantity =

SUM(OrderDetails\[Quantity])



Calculates the total number of units sold.

Total Orders

Total Orders =

DISTINCTCOUNT(Orders\[Order ID])



Counts unique orders.

Average Order Value

Average Order Value =

DIVIDE(

&#x20;   \[Total Sales],

&#x20;   \[Total Orders],

&#x20;   0

)



Calculates the average revenue generated per order.

Profit Margin %

Profit Margin % =

DIVIDE(

&#x20;   \[Total Profit],

&#x20;   \[Total Sales],

&#x20;   0

)



Measures profit as a percentage of total sales.

Sales Target

Sales Target =

SUM(SalesTargets\[Target])



Calculates the target sales amount under the current filter context.

Target Achievement %

Target Achievement % =

DIVIDE(

&#x20;   \[Total Sales],

&#x20;   \[Sales Target],

&#x20;   0

)



Measures actual sales as a percentage of the sales target.

Sales Variance

Sales Variance =

\[Total Sales] - \[Sales Target]



Measures the difference between actual sales and target sales.

A positive value indicates sales above target, while a negative value indicates sales below target.

Profit per Order

Profit per Order =

DIVIDE(

&#x20;   \[Total Profit],

&#x20;   \[Total Orders],

&#x20;   0

)



Calculates average profit generated per order.

Total Customers

Total Customers =

DISTINCTCOUNT(Orders\[CustomerName])



Calculates the number of unique customers.

Average Quantity per Order

Average Quantity per Order =

DIVIDE(

&#x20;   \[Total Quantity],

&#x20;   \[Total Orders],

&#x20;   0

)



Calculates the average number of units per order.

Orders per Customer

Orders per Customer =

DIVIDE(

&#x20;   \[Total Orders],

&#x20;   \[Total Customers],

&#x20;   0

)



Measures average order frequency per customer.

9\. Dashboard Pages

Executive Overview

Provides a high-level view of business performance.

Key metrics:

\- Total Sales

\- Total Profit

\- Total Orders

\- Total Customers

\- Average Order Value

\- Profit Margin %

Visuals include:

\- Monthly Sales Trend

\- Sales vs Target

\- Sales by Category

\- Profit by Category

\- Sales by State

Sales \& Profit Analysis

Focuses on revenue and profitability.

Includes:

\- Sales by Sub-Category

\- Profit by Sub-Category

\- Monthly Sales

\- Monthly Profit

\- Sales by Category and Sub-Category

Filters include:

\- Category

\- State

\- Year

Customer Intelligence

Focuses on customer behavior and value.

Includes:

\- Top 10 Customers by Sales

\- Sales by State

\- Customer Sales by Category

\- Customer Sales Trend

Filters include:

\- City

\- Category

Product Intelligence

Focuses on product performance.

Includes:

\- Sales by Sub-Category

\- Profit by Sub-Category

\- Quantity by Sub-Category

\- Product performance matrix

Filters include:

\- Category

Geographic Analysis

Focuses on geographic performance.

Includes:

\- Sales by State

\- Profit by State

\- Sales by City

Filters include:

\- Category

\- State

\- City

Target \& Performance

Focuses on performance against business targets.

Includes:

\- Actual Sales vs Sales Target

\- Sales Variance by Category

\- Target Achievement % by Category

Filters include:

\- Year

\- Category

10\. Key Business Questions

The dashboard can be used to investigate:

1\. What is the total sales performance?

2\. How much profit is being generated?

3\. Which categories generate the most revenue?

4\. Which sub-categories generate the most profit?

5\. Which customers generate the most sales?

6\. Which states and cities generate the most revenue?

7\. How does sales performance change over time?

8\. Are actual sales meeting targets?

9\. Which categories are above or below target?

10\. How efficiently are orders generating revenue and profit?

11\. Skills Demonstrated

This project demonstrates:

\- Microsoft Power BI

\- Power Query

\- DAX

\- Data Cleaning

\- Data Transformation

\- Data Modeling

\- Dimensional Modeling

\- KPI Development

\- Business Intelligence

\- Data Visualization

\- Sales Analytics

\- Customer Analytics

\- Product Analytics

\- Geographic Analysis

\- Target Performance Analysis

\- Git \& GitHub

12\. Project Status

Status: Actively Developing

Future improvements may include:

\- Additional business insights

\- Dashboard screenshots

\- Advanced DAX calculations

\- Performance optimization

\- Additional documentation

\- Further visualization improvements



