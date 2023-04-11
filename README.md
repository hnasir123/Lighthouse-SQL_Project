# Final-Project-Transforming-and-Analyzing-Data-with-SQL

## Project/Goals
The goal of the project is to analyze the data of a ecommerce to drive insights from data

## Process

Step 1 - The first step was to download all the csv files and load in Postgresql

Step 2 - Created tables from all the csv files with the required data types

Step 3 - Understand the data and try to find the meaning of all the coulumn and how the the tables and linked together

Step 4-  Cleaning and transforming the data.

Step 5 - Drive insights and answer the questions

Step 6 - Quality assurance

## Results

-  Which cities and countries have the highest level of transaction revenues on the site?
        country	     city	     revenue
      United States	Sunnyvale 	672.22999
- What is the average number of products ordered from visitors in each city and country?
   country	        city	      average_units_sold
    United States	  Sunnyvale	    2.375
    United States	    Chicago     	2
- Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?    
  country	      v2productcategory	  city	  count_by_category
  United States 	Housewares	   Sunnyvale 	168
- What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?
     country	      city	        name	                  count_by_country
    United States	Sunnyvale	SPF-15 Slim & Slender Lip Balm	69
- Find the total number of unique visitors by referring sites
  Answer: 2419
- What percentage of visitors are coming from which Channel grouing
channelgrouping	channelpercentage
  Organic Search	57.7
  Direct	19.72
  Referral	17.01
  Paid Search	3.3
  Affiliates	1.72
  Display	0.84


## Challenges 
Understanding the coulumn meaning was difficult as it does not have clear meanings and have multiple columns using same name in different sheets

Loading the data into postgre with correct data type was challlange 

## Future Goals
If i have more time i will check and ensure the correctness of the results as there are many fields which needs clear explananation
