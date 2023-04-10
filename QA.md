What are your risk areas? Identify and describe them.



QA Process:
Describe your QA process and include the SQL queries used to execute it.

1. ## Data Timeline consistency
   
   The purpose is to check if the data time line is conistent across tables.
   
   Products, Sales_by_SKU and Sales_report does not have data related to data
   
   For Analytics Table and All_Session table there are date values present

SELECT MIN(Date),
	   MAX(Date),
	   MAX(Date)-MIN(Date) AS Days
FROM analytics

Result
    MIN             MAX         Days
 "2017-05-01"	"2017-08-01"	92


SELECT MIN(Date),
	   MAX(Date),
	   MAX(Date)-MIN(Date) AS Days
FROM all_sessions

Result
 MIN                MAX         Days
"2016-08-01"	"2017-08-01"	365

Conclusion : All_session table contains data of 1 year while Analytics table contain only 3 months data while sales_report have no data for time so we cannot be sure of the timeline of sales. One Solution is to use data in both tables for the same 3 month periods to derive conclusions 


2. ## Data inconsistency in Products and All_Session Table
While trying to join Products table and all_sessions table we find that there are additional SKUs present in all_sessions table. The poducts table should contain all the SKU. Below LEFT JOIN was used to find the inconsistency.
There were 163 additional SKUs present in all_sessions table. 

SELECT DISTINCT all_sessions.productsku,v2productname,products.sku FROM all_sessions
LEFT JOIN products ON all_sessions.productsku = products.sku
WHERE  products.sku IS NULL


Some Sample results are below

| productsku     | v2productname                                     | sku  |
|----------------|---------------------------------------------------|------|
| GGOEYOLR080599 | YouTube Notebook and Pen Set                      | NULL |
| GGOEYOCR078099 | YouTube Spiral Journal with Pen                   | NULL |
| GGOEYAAB034614 | YouTube Men's Vintage Tee                         | NULL |
| GGOENEBB079399 | NestÂ® Protect Smoke + CO Black Wired Alarm-USA   | NULL |
| GGOENEBB079299 | NestÂ® Protect Smoke + CO Black Battery Alarm-USA | NULL |
| GGOEGOGA016299 | Grip Highlighter Pen 3 Pack                       | NULL |
| GGOEGOCC017699 | Compact Eco Journal                               | NULL |
| GGOEGOCC017699 | Compact Journal with Recycled Pages               | NULL |
| GGOEGOAR021999 | Color Changing Grip Pen                           | NULL |
| GGOEGOAR021899 | PaperMate Ink Joy Retractable Pen                 | NULL |
| GGOEGOAR021899 | Retractable Ballpoint Pen Red                     | NULL |
| GGOEGOAQ015999 | Bic Intensity Clic Gel Pen                        | NULL |

One approach is to add these additional SKUs in products table to make the data consistent but we need orderedquanity,stocklevel and other data to populate it products table
