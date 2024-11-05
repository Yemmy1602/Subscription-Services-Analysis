# Customer Segmentation for Subscription Services


## Table of Contents
- [Project Overview](#project-overview)


- [Project Objectives](#project-objectives)


- [Data Collected](#data-collected)


- [Data Sources](#data-sources)


- [Key Metrics](#key-metrics)


- [Tools Used](#tools-used)


- [Data Cleaning and Preparation](#data-cleaning-and-preparation)


- [Data Analysis](#data-analysis)


- [Data Visualization](#data-visualization)


- [Visual Analysis and Overall Insights](#visual-analysis-and-overall-insights)


- [Recommendations](#recommendations)



## Project Overview

This project analyzes customer data for a subscription service to understand customer behavior, identify key trends in cancellations and renewals, and uncover insights into 
customer segmentation by subscription type. The goal is to use data-driven insights to improve customer retention, optimize subscription offerings, and drive revenue growth. 

## Project Objectives
- Understand the distribution of customers by subscription type and identify top revenue-generating customers.
- Track and analyze cancellation trends to identify points of dissatisfaction.
- Analyze subscription activity over time and region, focusing on customer engagement and revenue performance.

## Data Collected
The dataset includes columns such as:
- CustomerID: Unique identifier for each customer.
- Region: Geographic area of the customer.
- SubscriptionType: Type of subscription (Basic, Standard, Premium).
- Revenue: Revenue generated per customer.
- SubscriptionStart and SubscriptionEnd: Start and end dates of each subscription.
- Canceled: Boolean flag indicating whether the subscription was canceled.

## Data Sources
The data used for this work is gotten from my project work.

## Key Metrics
- Total Customers: Total number of customers.
- Customers by Subscription Type: Count distribution of customers across Basic, Standard, and Premium plans.
- Top 5 Customers by Revenue: Revenue generated by the top five highest-value customers.
- Total Revenue: Total income generated from all customers.
- Revenue by Subscription Type: Revenue distribution across Basic, Standard, and Premium plans.
- Average Revenue per Customer: Average revenue contribution per customer.
- Revenue by Region: Revenue contributions from East, South, West, and North regions.
- Total Cancellations: Total number of canceled subscriptions.
- Cancellations by Region: Breakdown of cancellations by region.
- Monthly Cancellations: Monthly trend in subscription cancellations.
- Monthly Active Subscriptions: Number of active subscriptions over time.
- Active Subscriptions by Region: Distribution of active subscriptions by region.
- Average Subscription Duration: Average subscription length across all customers.


## Tools Used
- Excel: For preliminary data analysis and calculations.
- SQL: For querying and extracting insights from the customer and subscription data.
- Power BI: For interactive visualizations and dashboard creation.
- DAX (Data Analysis Expressions): For calculating key performance metrics such as churn rate, revenue per customer, and subscription trends.

## Data Cleaning and Preparation
- Data Loading and Inspection (Duplicates information were removed)
- No Missing Variables
- Creation of Calculated columns and measures

## Data Analysis
The following are the Excel formulas, SQL codes, DAX Expressions used during my Analysis
```
EXCEL FORMULA
Average Subscription Duration	= (12) =DATEDIF(@Sheet1!E:E,@Sheet1!F:F, "M")

SQLITE CODES
1. SELECT Region, COUNT(DISTINCT CustomerID) AS TotalCustomers
FROM CustomerData
GROUP BY Region;

2. SELECT TOP 1 SubscriptionType, COUNT(CustomerID) AS NumberOfCustomers
FROM CustomerData
GROUP BY SubscriptionType
ORDER BY NumberOfCustomers DESC;

3. SELECT CustomerID, CustomerName, SubscriptionStart, SubscriptionEnd, canceled
FROM CustomerData
WHERE Canceled = 'TRUE' 
  AND DATEDIFF(Month, 31/01/2022, 31/12/2024) <= 6;

4. SELECT AVG(DATEDIFF(Month, 31/01/2022, 31/12/2024)) AS AverageSubscriptionDuration
FROM CustomerData

5. SELECT CustomerID, CustomerName, SubscriptionStart, SubscriptionEnd
FROM CustomerData
WHERE DATEDIFF(month, 31/01/2022, 31/12/2024) > 12;
 
6. SELECT SubscriptionType, SUM(Revenue) AS TotalRevenue
FROM CustomerData
GROUP BY SubscriptionType
ORDER BY TotalRevenue DESC
 
7. SELECT TOP 3 Region, COUNT(CustomerID) AS Cancellations
FROM CustomerData
WHERE Canceled = 'TRUE'
GROUP BY Region
ORDER BY Cancellations DESC

8. SELECT CASE WHEN Canceled = 'TRUE' THEN 'Canceled' ELSE 'Active' END AS SubscriptionStatus, COUNT(CustomerID) AS Total_Count
FROM CustomerData
GROUP BY canceled;

DAX MEASURES USED IN POWERBI
Average Subscription Duration = AVERAGE(CustomerData[Subscription Duration (Months)]
)
Total Revenue = SUM(CustomerData[Revenue])
TotalCustomers = DISTINCTCOUNT(CustomerData[CustomerID])
Calculated Columns - Subscription Duration (Months) = DATEDIFF(CustomerData[SubscriptionStart],CustomerData[SubscriptionEnd],MONTH)
```
## Data Visualizations

### Microsoft Excel View for Analysis
![Excel Formula and Pivot Tables for CustomerData](https://github.com/user-attachments/assets/af4b2473-9e4c-4cf2-bf49-455d80368927)
![Excel Visual Representation for Customer Subscription Services](https://github.com/user-attachments/assets/2c998bd5-3db7-4a50-8d89-795296535b63)

### SQLITE Views
![SQLite Queries CustomerData view](https://github.com/user-attachments/assets/9e65b1b9-7211-45cd-a411-a1c67da987bd)
![SQLite Queries CustomerData II view](https://github.com/user-attachments/assets/55c9a596-34f0-4a3d-919d-cacc53632a8b)


### PowerBI - Subscription Services Analysis Dashboard
![Customer Segmentation by Subscription Type](https://github.com/user-attachments/assets/5dfa76b0-756f-4719-b08a-dd3e0d9dce81)
![Cancellation Trend Overtime](https://github.com/user-attachments/assets/6dcc9a83-cd2c-4198-a5f2-e2ae93603422)
![Subscription Trend Overtime](https://github.com/user-attachments/assets/fee05cf3-cef6-4cf8-b926-bad8831a8b93)

## Visual Analysis 

### Dashboard 1: Customer Segmentation by Subscription Type
This dashboard provides an overview of customer distribution by subscription type, revenue generation, and top customers.
- Total Customers and Revenue: Total Customers: 20, generating a Total Revenue of $150 million.
- Average Revenue per Customer: 1,996 indicating that each customer brings in high revenue. This metric is essential for understanding the average customer value and planning for customer acquisition or retention.

1. Subscription Types Distribution: The distribution by subscription type shows that Basic has the highest number of customers (10). Premium and Standard have an equal number of customers (5 each). The higher customer count in Basic may indicate its accessibility or popularity due to lower cost, but there might be an opportunity to encourage customers to upgrade to Premium or Standard plans, potentially increasing revenue per customer.

2. Top 5 Customers by Revenue: The Top 5 customers are primarily subscribed to Premium and Standard plans, with revenue per customer ranging between 7.5 and 7.56 million. These high-value customers are concentrated in the South and West regions, indicating that certain regions contribute disproportionately to revenue. This concentration could guide regional marketing efforts and customer service prioritization.

3. Total Revenue by Subscription Type: Despite having the highest customer count, Basic generates a revenue of 75 million, which is less than the combined revenue of Premium (38 million) and Standard (37 million). This suggests that although Basic is popular, Premium and Standard subscriptions bring in more revenue per customer. Strategies to promote Premium or Standard (e.g., by showcasing additional features or value) could help shift customer preference toward higher-tier plans.

### Dashboard 2: Cancellations Trend Over Time
This dashboard focuses on analyzing customer cancellation patterns across regions and time, which is critical for understanding and identifying points of customer dissatisfaction.

1. High Cancellations: 34,000 cancellations are reported, which is a significant churn rate relative to the total customer base.
The high number of cancellations suggests that customer retention is a major challenge. Understanding why customers leave could be a priority for improving subscription models or enhancing customer experience.

2. Cancellations by Region: The visual shows 100% cancellation trends across North, South, and West regions.
The uniformity in cancellation rates implies that customer dissatisfaction or lack of value perception is widespread, not restricted to any specific region. This points to broader issues with the service or the subscription model itself.

3. Cancellation Trends Over Time: A significant peak in cancellations occurs in April (7,000 cancellations) with a noticeable decline afterward. This spike could indicate seasonal factors, dissatisfaction post-holiday season, or billing/renewal cycles that result in higher cancellations. Analyzing customer feedback or conducting surveys around this period might provide insights into why cancellations are high in April.

4. Cancellation Trends by Region (Map): Cancellations are distributed globally, reinforcing the insight that churn is a widespread issue. Regional marketing or targeted customer retention programs could be implemented, especially focusing on regions where customer acquisition costs might be high.

### Dashboard 3: Subscriptions Trend Over Time
This dashboard visualizes subscription activity over time, active subscriptions by region, and revenue distribution across regions, offering insights into customer engagement trends and regional revenue performance.

1. Subscription Activity Over Time: The Subscriptions Trends Over Time graph indicates fluctuations in customer activity. Counts range from 56 to 62 active subscriptions, with the lowest activity in February and peaks in June and August.
These fluctuations might correlate with seasonal factors, suggesting times when customers are more or less engaged with the subscription service. Understanding the reasons behind these fluctuations could help in timing promotional activities or improving retention strategies.

3. Active Subscriptions by Region: This table provides a breakdown of active subscriptions by region: East and North have Basic subscriptions, South has Premium, West has Standard. This distribution may imply regional preferences or customer segment characteristics specific to each region, offering opportunities for tailored marketing strategies that cater to each region's preferred subscription type.

4. Revenue and Duration by Subscription Type: Premium and Standard subscriptions have the highest average revenue (around 2,003), with a 12-month duration for each type. Basic has a slightly lower revenue per customer (1,993) but also a 12-month duration.
The similar average revenue values suggest effective pricing strategies across the subscription tiers. However, encouraging customers to move from Basic to Premium/Standard could further increase revenue without significantly altering retention patterns.

5. Revenue by Region: East region generates the highest revenue ($37 million), with South, West, and North each contributing $15 million. This distribution suggests a concentration of high-value customers in the East, likely due to a larger or more engaged customer base. Targeting other regions with strategies to boost engagement or acquire new customers could balance the revenue distribution.
   
## Recommendations
- Focus on Upselling: Consider campaigns to move Basic subscribers to Premium or Standard plans to increase revenue.
- Regional Targeting: Prioritize customer engagement and retention in South and West regions due to their revenue contribution.
- Analyze Basic Subscribers: Identify what attracts customers to Basic, and assess if adding value to Premium could convert Basic users to higher tiers.
- Analyze Reasons for April Spike: Conduct surveys or analyze feedback around April to understand why cancellations peak during this period.
- Customer Retention Strategies: Develop programs aimed at enhancing value perception across all regions, as the cancellation trend is consistent geographically.
- Offer Renewal Incentives: Provide incentives for customers considering cancellation, especially around peak cancellation times.
- Regional Campaigns for Subscription Type Preference: Tailor marketing efforts in each region to align with their preferred subscription types, potentially increasing conversions by targeting the right customer profiles.
- Seasonal Promotions: Consider promotional efforts during lower activity months (e.g., February) to maintain engagement and prevent churn.
- Revenue Growth in Other Regions: Focus on customer acquisition or engagement programs in South, West, and North regions to reduce dependency on East for revenue.


