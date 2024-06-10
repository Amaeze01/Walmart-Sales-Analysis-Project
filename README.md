
# Walmart Sales Analysis Project
![Walmart logo](https://github.com/Amaeze01/Walmart-Sales-Analysis-Project/assets/170688872/9a97e8e6-a4e3-4f26-b1e5-80c2c1aeff18)

# Problem Statement
Walmart supermarket chain seeks to enhance its overall sales performance and customer satisfaction by identifying key areas of strength and opportunities for improvement. The management needs a comprehensive sales data analysis to make informed decisions on product offerings, marketing strategies, and customer engagement initiatives. Specifically, they want to understand product line performance, revenue trends, customer demographics, and the impact of different sales channels and times on overall business outcomes.
# How I Plan on Solving the Problem
To help the Walmart supermarket gather valuable insights from its extensive sales dataset, I will utilize SQL and a data visualization tool like Tableau to extract relevant information and conduct insightful analyses. By leveraging SQL's functions, I can uncover key metrics such as product line performance, revenue trends, customer demographics, and sales patterns. Once the data is extracted and prepared, I will leverage Tableau to present the findings. This will allow for interactive exploration of the data, enabling stakeholders to gain actionable insights through visually appealing charts, graphs, and interactive visualizations.

- Dataset used: The dataset was obtained from [Kaggle Walmart Sales Forecasting Competition](https://www.kaggle.com/c/walmart-recruiting-store-sales-forecasting). This dataset contains sales transactions from three different branches of Walmart, respectively located in Mandalay, Yangon and Naypyitaw.
- Tools used: Excel, MySQL, Tableau

# Key Questions to Address
1. General Overview
- How many unique cities does the data cover?
```Sql
SELECT distinct city 
FROM sales;
```
Result:

![1 1](https://github.com/Amaeze01/Walmart-Sales-Analysis-Project/assets/170688872/f5b7bbf6-04e7-45ba-b52c-2ec2b76ec25d)

- Which city has the highest total revenue?
```Sql
SELECT branch, city,
ROUND(SUM(total), 1) AS total_revenue 
FROM sales
GROUP BY branch, city
ORDER BY total_revenue DESC;
```
Result:

![1 2](https://github.com/Amaeze01/Walmart-Sales-Analysis-Project/assets/170688872/60184ba8-4559-402d-b69b-cab284854bcd)

**Insight**: The data spans three major cities: Naypyitaw, Yangon, and Mandalay. Understanding the performance across these cities can help tailor specific marketing and operational strategies. Naypyitaw, with the highest revenue, indicates strong sales and potentially a larger or more spendthrift customer base. Yangon follows closely, showing robust sales and potential for growth to surpass Naypyitaw. Despite having the lowest revenue, Mandalay is close behind the other two, indicating room for improvement by addressing factors such as customer preferences, competition, or socio-economic conditions.

2. Sales & Product Analysis
- What is the total revenue by month?
```Sql
SELECT month_name AS month, 
ROUND(SUM(total) ,1) AS total_revenue
FROM sales
GROUP BY month_name
ORDER BY total_revenue DESC;
```
Result: 

![2 1](https://github.com/Amaeze01/Walmart-Sales-Analysis-Project/assets/170688872/72801cba-2ee9-4e97-a854-44670c819c53)

- What is the number of sales made at different times of the day?
```Sql
SELECT time_of_day,
COUNT(time_of_day) AS total_sales
FROM sales
WHERE day_name = "Saturday"
GROUP BY time_of_day
ORDER BY total_sales DESC;
```
Result:

![2 2](https://github.com/Amaeze01/Walmart-Sales-Analysis-Project/assets/170688872/f35fd2c9-e1b2-4768-bfa0-e86cdcf96bfa)

- How many unique product lines are in the data?
```Sql
SELECT distinct product_line
FROM sales;
SELECT COUNT(distinct product_line)
FROM sales;
```
Result: 

![2 3](https://github.com/Amaeze01/Walmart-Sales-Analysis-Project/assets/170688872/19c63399-c605-43ef-b2c7-b1a27a560c6d)

- What is the best-selling product line?
```Sql
SELECT product_line,
COUNT(product_line) AS PL_cnt
FROM sales
GROUP BY product_line
ORDER BY PL_cnt DESC;
```
Result: 

![2 4](https://github.com/Amaeze01/Walmart-Sales-Analysis-Project/assets/170688872/a614d5d8-9873-48d5-a9b6-33a05f96c729)

- Which product line generated the most revenue?
```Sql
SELECT product_line,
ROUND(SUM(total), 1) AS total_revenue
FROM sales
GROUP BY product_line
ORDER BY total_revenue DESC;
```
Result: 

![2 5](https://github.com/Amaeze01/Walmart-Sales-Analysis-Project/assets/170688872/06fb511a-f00a-4fa9-9a33-c618f11975c7)

- What is the average rating of each product line?
```Sql
SELECT 
ROUND(AVG(rating), 2) AS avg_rating, 
product_line
FROM sales
GROUP BY product_line
ORDER BY avg_rating DESC;
```
Result: 

![2 6](https://github.com/Amaeze01/Walmart-Sales-Analysis-Project/assets/170688872/3e6e1775-293e-46f3-89a0-e0155393917c)

**Insight**: January has the highest revenue, likely due to post-holiday shopping or new year promotions. Revenue dips in February but recovers in March, possibly due to February's shorter duration and seasonal effects.

Evening sales are the highest, indicating customers prefer shopping after work. Afternoon sales are significant but lower, and morning sales are the least, suggesting an opportunity to boost morning foot traffic.

There are six unique product lines. Fashion accessories lead in sales, followed by food and beverages, indicating high customer interest. Health and beauty have the lowest sales but still show potential for targeted marketing.

Food and beverages generate the most revenue, despite being second in sales volume, and have the highest average rating, showing strong customer satisfaction. Fashion accessories also perform well in sales and satisfaction. Other product lines have slightly lower ratings, indicating areas for improvement in product quality or customer experience.

3. Customer insight
- What is the most common customer type?
```Sql
SELECT customer_type,
COUNT(customer_type) AS cnt
FROM sales
GROUP BY customer_type;
```
Result:

![3 1](https://github.com/Amaeze01/Walmart-Sales-Analysis-Project/assets/170688872/6286f3b7-ab2d-4a2f-b0a5-cda781e0243f)

- Which customer type generates the most revenue?
```Sql
SELECT customer_type,
ROUND(SUM(total) ,1) AS total_revenue
FROM sales
GROUP BY customer_type
ORDER BY total_revenue DESC;
```
Result:

![3 2](https://github.com/Amaeze01/Walmart-Sales-Analysis-Project/assets/170688872/fc9ad5fb-7b2e-4647-9d95-2ecb8db13e09)

- What is the gender distribution of the customers?
```Sql
SELECT gender,
COUNT(gender) AS gender_cnt
FROM sales
GROUP BY gender;
```
Result: 

![3 3](https://github.com/Amaeze01/Walmart-Sales-Analysis-Project/assets/170688872/882e7236-d6b8-4329-9f57-5ee3d1dd92a6)

**Insight**: The data reveals a near-equal distribution of customer types, with 496 Normal and 499 Member customers, indicating the supermarket's effectiveness in appealing to both groups. However, Members generate more revenue ($163,625.10) than Normal customers ($157,261.30), suggesting that Members tend to spend more. The supermarket can capitalize on this by enhancing membership benefits to attract more Members and boost revenue. The supermarket could also implement targeted engagement strategies like personalized recommendations, special events for Members, and feedback systems to continually improve the shopping experience for both Normal and Member customers. Additionally, the gender distribution is almost balanced, with 498 Male and 497 Female customers, indicating that the supermarket's products and services appeal equally to both genders. Maintaining this balance is essential by offering products catering to male and female customers.

# Data visualization
To enhance the understanding and performance of Walmart's sales, I created an interactive Tableau dashboard visualizing key metrics:

- Summary metrics: The title block includes total sales, total profits, and average ratings across the three cities, offering a quick snapshot of overall performance.
- Weekly Sales: Tracks sales trends and fluctuations on a weekly basis, helping to identify peak periods and strategize promotions and inventory management.
- Profit by Product by City: Shows profit margins for different products across cities, aiding in targeted marketing and inventory decisions based on regional preferences.
- Units Sold in Each City: Displays sales volume by city, allowing for better stock level management and ensuring availability of popular items.
- Sales by City: Provides a clear picture of revenue contributions from each city, helping to evaluate store performance and adjust sales strategies.
This dashboard provides actionable insights to drive better decision-making, optimize marketing efforts, and improve customer satisfaction.

**Dashboard link**: [Walmart Sales Analysis Project dashboard](https://public.tableau.com/views/WalmartSalesAnalysis_Visualization/Dashboard1?:language=en-US&publish=yes&:sid=&:display_count=n&:origin=viz_share_link)

# Conclusion
The Walmart Sales Analysis Project identified key insights to improve sales performance and customer satisfaction. Using SQL and Tableau, I analyzed product performance, revenue trends, customer demographics, and sales patterns.

Key findings include:
- **Revenue Trends:** January had the highest revenue, while February saw a dip, likely due to its shorter duration and seasonal effects.
- **Customer Behavior:** Evening sales were the highest, indicating a preference for shopping after work. Morning sales were the lowest, suggesting an opportunity to boost traffic during this time.
- **Product Performance:** Fashion accessories led in sales, while food and beverages generated the most revenue and had the highest customer satisfaction. Health and beauty, despite lower sales, show potential for targeted marketing efforts.
- **Customer Insights:** Members spent more than Normal customers, highlighting the benefits of enhancing membership programs. The gender distribution was nearly equal, showing that the supermarket's offerings appeal to both male and female customers.

The interactive Tableau dashboard visualizes these insights, providing Walmart management with actionable data to drive better decisions, optimize marketing, and improve customer satisfaction.

Dashboard link: [Walmart Sales Analysis Project dashboard](https://public.tableau.com/views/WalmartSalesAnalysis_Visualization/Dashboard1?:language=en-US&publish=yes&:sid=&:display_count=n&:origin=viz_share_link)
