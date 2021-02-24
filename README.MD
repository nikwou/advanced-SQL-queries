This repository is an ongoing collection effort of not-so-easy SQL query challenges I've come across.

# Pivot queries

Assume you have a table of product sales records (including columns Product_name and Transaction_date); and want to know how many products were sold per calendar quarter

    select Product_name,
        count(case when quarter(Transaction_date) = 1 then 1 end) as Q1,
        count(case when quarter(Transaction_date) = 2 then 1 end) as Q2, 
        count(case when quarter(Transaction_date) = 3 then 1 end) as Q3, 
        count(case when quarter(Transaction_date) = 4 then 1 end) as Q4
    from series_inventory where ... group by Product_name

In this example, the output is a table where each line represents a product and each column is a calendar quarter. This is only the basic skeleton, more layers of complexity can added (e.g. in the "where" part). Also, other aggregation functions like e.g. sum(), min(), max(), avg() should work as well.
