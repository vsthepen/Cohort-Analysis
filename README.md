# Cohort-Analysis

Cohort analysis is a form of behavioural analytics used to measure user engagement over time a.k.a. churn rate. Engagement is not the same as growth, you could be growing your customer base by acquiring new customers, but those customers are not sticking with you over time. So, cohort analysis helps you separate between engagement and growth.

It is frequently employed by businesses that interact with clients and provide goods and services through websites, apps, subscription models, etc.

## Business Problem

-	An online business wants to monitor, measure and assess how successfully it retains new customers after they make a first purchase, in addition to the average amount they spend over the next 12 months.

Data was collected in two different Excel worksheets. The order and sales information were in one workbook, while the customer information was in the other.

## Data Cleaning and Transformation

-	Power query was used to import the tables with the data from both workbooks, as well as clean and transform it.

-	Blank rows and unnecessary columns were eliminated, and each column was assigned the proper data type.

![Column quality indicators confirming cleaned data](https://user-images.githubusercontent.com/115559534/227917324-ab061084-7a38-4581-abf7-7292107214b9.png)

## Data Analysis

-	After cleaning, the tables were loaded into Power Bi.

-	a *“one to many”* relationship was drawn between the customer and sales table.

![Data Model showing relationship between tables](https://user-images.githubusercontent.com/115559534/227918182-f41ba991-3bf6-406d-961a-a59ff9f71e7a.png)

-	Creation of Future Months Table: This is a table that has a list of months number to denote the months after the customer’s first purchase.

•	The Future Months Table was created using the *“GENERATE SERIES”* DAX function in power BI.

![DAX - Future Months Table](https://user-images.githubusercontent.com/115559534/227918611-3cb7c583-33a0-43fb-86df-a159fa18fb37.png)

•	Month 0 - Initial purchase month

•	Month 12 – Twelve months after the purchase.

![Future Months Table](https://user-images.githubusercontent.com/115559534/227919086-92dca551-585a-4fba-9872-4308f5b0aa94.png)

-	Creation of Key Measures:

•	**Customer retention** i.e., the number of customers retained each month after the initial month of purchase and the retention rate of the customers (%).

![DAX - Customer retention %](https://user-images.githubusercontent.com/115559534/227919428-7b8b2469-9d8e-4377-a97f-05a819261f21.png)

•	**Avg. amount spent** i.e., the average amount spent by new customers in the first month of acquisition, and throughout the following 12 months.

![image](https://github.com/vsthepen/Cohort-Analysis/assets/115559534/98b50998-cd75-4d4c-9e08-9efcb0b2f42a)

-	Variables created when building the DAX formulas include:

•	*FirstOrderMonth*: This is the earliest date a purchase was made by a customer.

•	*CurrentMonthAfter*: This represents how many months into the future you want to calculate.

## Logic of the DAX formula used to create the “Customer Retention (%)” measure

### Variable Definitions:

- VAR FirstOrderMonth = SELECTEDVALUE(Sales[First Order Month]): This variable finds the "First Order Month" selected by the user in the Sales table. It represents the month when a customer made their first purchase.
  
- VAR CurrentMonthAfter = SELECTEDVALUE('Future Months Table'[Value]): This variable finds the "Value" selected by the user in the 'Future Months Table.' It represents how many months after the first order you want to count customers.

### Main Calculation (RETURN) : This is where the actual calculation happens.

- DIVIDE(): This function calculates the division of two numbers.
  
- CALCULATE() and DISTINCTCOUNT():

CALCULATE(DISTINCTCOUNT(Sales[Customer ID]), ...): This part of the formula calculates the number of distinct (unique) customers who made purchases within a specific time frame.

- FILTER() Function and EOMONTH() Function:

FILTER(Sales, EOMONTH(Sales[Order Date],0)=EOMONTH(FirstOrderMonth,CurrentMonthAfter)): This is a filter condition that selects customers who made purchases within the time frame defined by "FirstOrderMonth" (the first order month) and "CurrentMonthAfter" (the number of months into the future). Essentially, it filters the data to include only the customers who made purchases within this specified time frame.

- DISTINCTCOUNT(Sales[Customer ID]): This part counts the number of distinct customers in the Sales table. It tells us how many unique customers there are in total.

**Customer retention %**

Month 0, the first month of purchase, is at 100% because it is the first month that every member of that cohort made a purchase.

![Cohort - Customer retention %](https://user-images.githubusercontent.com/115559534/227920180-2357c2e6-b55d-404c-9c0f-a7f23dcd9b7e.png)

![image](https://github.com/vsthepen/Cohort-Analysis/assets/115559534/d834f64f-b51e-4fea-8b99-f3f6bcbede77)

**Avg. amount spent**

![image](https://github.com/vsthepen/Cohort-Analysis/assets/115559534/0f85ed87-654d-47c9-9612-8a460e81ff35)

## Insights

- The months of **March, September & November** are the company’s **highest** months for gaining new customers.

- The months of **January and February** are the company's **lowest** months for gaining new customers.

- Retention rates generally decline dramatically in the first six months following a user's initial order, but they appear to rise in the second half of the year.

- Since 2014, there has been a significant decline in the number of users acquired in the first month, and this decline seems to be continuous.

- In the year 2016, May had the highest average amount spent by users in the first order month despite acquiring only a few new users.

- The company’s products & services is most successful in attracting new users from the **East & West** regions.

