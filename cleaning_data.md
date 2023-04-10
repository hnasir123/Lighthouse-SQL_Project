What issues will you address by cleaning the data?


Queries:
Below, provide the SQL queries you used to clean your data.



## Correct the scale for price and revenue in Analytics table 

UPDATE analytics 
SET unit_price = unit_price /1000000

UPDATE analytics 
SET revenue = revenue /1000000

## Delete the bounces , userid column from Analytics Table as they mostly have blanks

ALTER TABLE analytics DROP COLUMN userid
ALTER TABLE analytics DROP COLUMN bounces


## Correct the scale for price and revenue in All Sessions Table 

UPDATE all_sessions 
SET totaltransactionrevenue = totaltransactionrevenue /1000000


## Delete unnecesary columns containing Blanks

ALTER TABLE all_sessions 
DROP COLUMN searchKeyword,
DROP COLUMN itemQuantity,
DROP COLUMN itemRevenue,
DROP COLUMN transactionRevenue,
DROP COLUMN sessionQualityDim,
DROP COLUMN productRefundAmount,
DROP COLUMN eCommerceAction_type,
DROP COLUMN eCommerceAction_step,
DROP COLUMN eCommerceAction_option

## Finding Duplicated

-- ALL Sesssion table

SELECT *, 
    ROW_NUMBER() OVER ( 
        PARTITION BY visitId, fullVisitorId
        ORDER BY visitId, fullVisitorId
        ) AS Row_Number
FROM all_sessions LIMIT 5

-- Analytics table 


SELECT *, 
    ROW_NUMBER() OVER ( 
        PARTITION BY visitId, fullVisitorId
        ORDER BY visitId, fullVisitorId
        ) AS Row_Number
FROM analytics;