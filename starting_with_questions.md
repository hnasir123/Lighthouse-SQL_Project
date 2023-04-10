Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


SQL Queries:


SELECT all_sessions.country,
	   all_sessions.city,
	   SUM(analytics.revenue) AS Revenue
FROM analytics
JOIN all_sessions ON analytics.visitid = all_sessions.visitid
WHERE analytics.units_sold >= 1 AND all_sessions.transactions IS NOT NULL AND all_sessions.city != 'not available in demo dataset'
GROUP BY all_sessions.country,all_sessions.city
ORDER BY Revenue DESC



Answer:

| country       | city          | revenue    |
|---------------|---------------|------------|
| United States | Sunnyvale     | 672.229992 |
| United States | Seattle       | 358        |
| United States | San Francisco | 312.679998 |
| United States | Chicago       | 306        |
| United States | Mountain View | 159.97     |
| United States | Palo Alto     | 151        |
| United States | New York      | 139.95     |
| Switzerland   | Zurich        | 16.99      |




**Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries:

SELECT all_sessions.country,
       all_sessions.city,
	   AVG(analytics.units_sold) AS Average_Units_Sold
FROM analytics
JOIN all_sessions ON analytics.visitid = all_sessions.visitid
WHERE analytics.units_sold >= 1 AND all_sessions.transactions IS NOT NULL AND all_sessions.city != 'not available in demo dataset'
GROUP BY all_sessions.country,all_sessions.city
ORDER BY Average_Units_Sold DESC



Answer:
| country       | city          | average_units_sold |
|---------------|---------------|--------------------|
| United States | Sunnyvale     | 2.375              |
| United States | Chicago       | 2                  |
| United States | Seattle       | 1.5                |
| United States | San Francisco | 1.44               |
| United States | Palo Alto     | 1                  |
| United States | Mountain View | 1                  |
| United States | New York      | 1                  |
| Switzerland   | Zurich        | 1                  |




**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:

SELECT all_sessions.country,
	   all_sessions.v2productcategory,
	   all_sessions.city,
	   SUM(analytics.units_sold) AS Count_By_Category
FROM analytics
JOIN all_sessions ON analytics.visitid = all_sessions.visitid
JOIN products ON all_sessions.productsku = products.sku
WHERE analytics.units_sold >= 1 AND all_sessions.transactions IS NOT NULL AND all_sessions.city != 'not available in demo dataset' 
GROUP BY all_sessions.v2productcategory,all_sessions.country,all_sessions.city
ORDER BY Count_By_Category DESC LIMIT 4



Answer:

| country       | v2productcategory                          | city          | count_by_category |
|---------------|--------------------------------------------|---------------|-------------------|
| United States | Housewares                                 | Sunnyvale     | 168               |
| United States | Home/Apparel/Women's/Women's-T-Shirts/     | San Francisco | 22                |
| United States | Home/Nest/Nest-USA/                        | Seattle       | 12                |
| United States | Home/Apparel/Men's/Men's-Performance Wear/ | New York      | 12                |




**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:

SELECT all_sessions.country,
	   all_sessions.city,
	   products.name,
	   COUNT(all_sessions.productsku) AS Count_By_Country
FROM analytics
JOIN all_sessions ON analytics.visitid = all_sessions.visitid
JOIN products ON all_sessions.productsku = products.sku
WHERE analytics.units_sold >= 1 AND all_sessions.transactions IS NOT NULL AND all_sessions.city != 'not available in demo dataset'
GROUP BY products.name,all_sessions.country,all_sessions.city
ORDER BY Count_By_Country DESC LIMIT 5


Answer:

| country       | city          | name                                              | count_by_country |
|---------------|---------------|---------------------------------------------------|------------------|
| United States | Sunnyvale     | SPF-15 Slim & Slender Lip Balm                    | 69               |
| United States | New York      |  Men's Short Sleeve Performance Badge Tee Pewter  | 12               |
| United States | San Francisco |  Women's Scoop Neck Tee White                     | 11               |
| United States | San Francisco |  Women's 3/4 Sleeve Baseball Raglan Heather/Black | 8                |
| United States | Seattle       |  Cam Indoor Security Camera - USA                 | 8           



**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:


SELECT all_sessions.country,
	   all_sessions.city,
	   SUM(analytics.revenue) AS Revenue
FROM analytics
JOIN all_sessions ON analytics.visitid = all_sessions.visitid
WHERE analytics.units_sold >= 1 AND all_sessions.transactions IS NOT NULL AND all_sessions.city != 'not available in demo dataset'
GROUP BY all_sessions.country,all_sessions.city
ORDER BY Revenue DESC



Answer:

| country       | city          | revenue    |
|---------------|---------------|------------|
| United States | Sunnyvale     | 672.229992 |
| United States | Seattle       | 358        |
| United States | San Francisco | 312.679998 |
| United States | Chicago       | 306        |
| United States | Mountain View | 159.97     |
| United States | Palo Alto     | 151        |
| United States | New York      | 139.95     |
| Switzerland   | Zurich        | 16.99      |






