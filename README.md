# Cohort-Analysis

Cohort analysis is a form of behavioural analytics used to measure user engagement over time a.k.a. churn rate. Engagement is not the same as growth, you could be growing your customer base by acquiring new customers, but those customers are not sticking with you over time. So, cohort analysis helps you separate between engagement and growth.

It is typically used in companies that engage customers and offer products and services via websites, apps, subscription model etc.

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

•	**Customer Avg. Spend** i.e., the average amount spent by new customers in the first month after acquisition, and throughout the following 12 months.

![DAX - New Customer Avg. spend](https://user-images.githubusercontent.com/115559534/227919746-e07dea84-feb8-47f5-b0d0-38828692b1c1.png)

-	Some of the variables created when building the DAX formulas include:

•	*FirstOrderMonth*: This is the earliest date a purchase was made by a customer.

•	*CurrentMonthAfter*: This indicates the following months after the first order month.

•	*FutureNewCustomers*: Identifies customers acquired in a particular month e.g., May 2014, that also bought in the following months e.g., June 2014, August 2014.

## Logic of the DAX formula used in creation of the “Customer Retention (%)” measure

-Before I proceed, kindly note that the EOMONTH function takes in two parameters, the start date in DateTime format, or in an accepted text representation of a date, and the months, a number representing the number of months before or after the start_date.

EOMONTH(<start_date>, <months>)

-In order to return the selected first order month and future months, I first generated two variables. I calculated the number of distinct customers and filtered the result so that the end of month in the selected date equals end of month (start date is the (first order date), interval is the selected current month after). The DIVIDE function was then used to divide the number of customers kept each succeeding month/distinct count of new customers obtained from the first order date.

-With the addition of a new variable called FutureNewCustomers, the second measure called “Customer Avg. Spend” was developed using a methodology similar to that described previously.

## Data Visualization

A matrix was used to create a straightforward visual representation. The retention rate was highlighted using conditional formatting. A higher retention rate is indicated by a darker shade of blue in the format, whereas a lower retention rate is shown by a lighter shade of blue.
In a cohort Table, the months on the left side of the matrix (column) are knows as the acquisition months, while the months at the top (rows) are known as the future months within a period.

![Cohort - Customer retention %](https://user-images.githubusercontent.com/115559534/227920180-2357c2e6-b55d-404c-9c0f-a7f23dcd9b7e.png)

![Cohort - Customer Avg. Spend](https://user-images.githubusercontent.com/115559534/227920468-f204fabb-6b0b-4ae7-b5f6-577d6bdc467f.png)

Month 0, the first month of purchase, is at 100% because it is the first month that every member of that cohort made a purchase.

## Insights

-	In general, the company's customer retention rate during the first five months is much lower than it is between six and twelve months.
-	It was observed that, up to six months after purchase, the average spend significantly decreases.
-	Over a three-year period (2014-2016), the average amount spent by new customers in the month of initial purchase lingered in-between $436 – $497.

## Recommendations

-	Better marketing campaigns must be developed by the company with a focus on newly acquired customers. Once the customer is on board, the campaign should run for the first three to five months.
-	The new customer should have enough time during this phase (3-5 months) to interact with the product/service offerings and ultimately convert to a sold-and-retained customer.
-	We should check to see if items bought by first-time customers are constantly in stock and occasionally offer discounts on those items.
