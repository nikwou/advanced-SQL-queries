# Advanced SQL queries

This repository is a living collection of SQL query challenges I've come across.

## Pivot queries

Assume you have a table of product sales records (including columns Product_name and Transaction_date). You want to know how many products were sold per calendar quarter.

    select Product_name,
        count(case when quarter(Transaction_date) = 1 then 1 end) as Q1,
        count(case when quarter(Transaction_date) = 2 then 1 end) as Q2, 
        count(case when quarter(Transaction_date) = 3 then 1 end) as Q3, 
        count(case when quarter(Transaction_date) = 4 then 1 end) as Q4
    from table where ... group by Product_name

Resulting output should be a table where each line represents a product and each column shows the number of products sold during the respective calendar quarter. This is only the basic skeleton, more layers of complexity can added (e.g. in the "where" part). Also, other aggregation functions like e.g. sum(), min(), max(), avg() should work as well.

## Window queries

Assume you have a table that stores e.g. closing prices for various stock-listed securities in three columns (Ticker, Date, Close). You want to calculate the percentage change between two Dates. In the example below, it is the percentage change between today and 60 rows earlier. This will correspond to "60 days earlier" only if a closing price is recorded each day - including weekend days. As this is rarely true, the timeframe will be longer (10 weeks assuming 5 rows per week for Monday to Friday).

    SELECT 
        Ticker, Close, 
        ROUND((Close/(FIRST_VALUE(Close) OVER (PARTITION BY Ticker ORDER BY Date ROWS 60 PRECEDING))-1)*100,2) as diffpct60
    FROM table 

A where clause may be added for additional filtering.

... to be continued ...
