# SQL-PRACTICE-QUESTIONS

-- Script 3 :
-- New and repeated customers

CREATE DATABASE new_repeated_customers;
USE new_repeated_customers;
SELECT*FROM customer_orders;
-- For new customers: First_time: co.Order_date= MIN(order_date)
-- For repeated customers : co.order_date!= Min(order_date) = repeated

SOLUTION:

WITH First_time AS(
SELECT customer_id, MIN(order_date) AS First_time_order_dates
FROM customer_orders
GROUP BY customer_Id)
-- Fv= first_visit
-- CO= Customer_orders
SELECT co.order_date, 
SUM(CASE WHEN co.order_date= fv.First_time_order_dates THEN 1 ELSE 0 END) AS New_customer,
SUM(CASE WHEN co.order_date != fv.First_time_order_dates THEN 1 ELSE 0 END) AS Repeated_customers
FROM customer_orders co INNER JOIN First_time fv
ON co.customer_id=fv.customer_id
GROUP BY co.order_date
order by co.order_date
LIMIT 100;

FIND OUT ORDERS PER CUSTOMERS:
-- Count Orders Per Customer
SELECT*FROM customer_orders;
SELECT customer_id,COUNT(customer_Id) AS num_of_orders FROM customer_orders
GROUP BY customer_id
ORDER BY customer_Id ASC;
