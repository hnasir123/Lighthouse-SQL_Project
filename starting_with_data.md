#Question 1: find all duplicate records

SQL Queries:


-- All Session table

SELECT *, 
    ROW_NUMBER() OVER ( 
        PARTITION BY visitId, fullVisitorId
        ORDER BY visitId, fullVisitorId
        ) AS Row_Number
FROM all_sessions;

-- Analytics table 


SELECT *, 
    ROW_NUMBER() OVER ( 
        PARTITION BY visitId, fullVisitorId
        ORDER BY visitId, fullVisitorId
        ) AS Row_Number
FROM analytics;



Answer: 


row_number
1
1
1
2
1


Question 2: find the total number of unique visitors

SQL Queries:

SELECT COUNT(DISTINCT fullvisitorid) FROM all_sessions


Answer:
14223

Question 3:  find the total number of unique visitors by referring sites


SQL Queries:

SELECT COUNT(DISTINCT fullvisitorid)
FROM all_sessions
WHERE channelGrouping = 'Referral'

Answer:

2419

Question 4:

SQL Queries: find each unique product viewed by each visitor



Answer:

|        v2productname                               | fullvisitorid       |
|----------------------------------------------------|---------------------|
| "Google Men's Convertible Vest-Jacket Pewter"      | 9365250589515174000 |
  "Nest® Protect Smoke + CO White Battery Alarm-USA" | 1671520825516375600 |
| "Google 2200mAh Micro Charger"                     | 5637452152421961000 |
| "YouTube Wool Heather Cap Heather/Black"           | 3595256255415152600 |
| "YouTube Onesie Heather"                           | 6227810681298183000 |
| "Nest® Protect Smoke + CO White Battery Alarm-USA" | 3001118138260716500 |
| "Nest® Protect Smoke + CO White Battery Alarm-USA" | 6851990928086818000 |
| "Galaxy Screen Cleaning Cloth"                     | 972604507813539200  |
| "Google Device Stand"                              | 6158093821579367000 |
| "Google 5-Panel Cap"                               | 5888354745869407000 |



Question 5:  compute the percentage of visitors to the site that actually makes a purchase

SQL Queries:

SELECT
 100.0*SUM(case when transactions = 1 then 1 else 0 end)/count(*) AS PercentageConversion
FROM all_sessions 

Answer:

0.5352187128320338

Question 6:  What percentage of visitors are coming from which Channel grouing

SQL Queries:

SELECT channelGrouping,
	    ROUND(count(DISTINCT fullvisitorid) * 100.0 / (select count(DISTINCT fullvisitorid) from all_sessions),2) AS ChannelPercentage
FROM all_sessions
GROUP by channelGrouping
ORDER BY ChannelPercentage DESC


Answer:

| channelgrouping | channelpercentage |
|-----------------|-------------------|
| Organic Search  | 57.7              |
| Direct          | 19.72             |
| Referral        | 17.01             |
| Paid Search     | 3.3               |
| Affiliates      | 1.72              |
| Display         | 0.84              |
| (Other)         | 0.04              |

