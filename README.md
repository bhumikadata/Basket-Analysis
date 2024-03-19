# Basket-Analysis

## Description
This SQL script provides a solution for basic product recommendation based on basket analysis. It finds product pairs along with the count of times they have been purchased together,
which can be used to make recommendations to new users on an e-commerce website.

Here's a breakdown of your SQL query:

-- I gave alias to the orders table as o1 and o2 to differentiate between the two instances of the table in the self-join.

-- then selected product_id from both the orders table as product_1 and product_2.

-- Counted the number of occurrences of each pair of products as purchase_frequency.

-- In the ON clause of the join condition, I matched orders based on their order_id.

-- In the WHERE clause, I ensured that product_id of the first order is greater than product_id of the second order to avoid duplicate pairs.

-- Finally, I grouped the results by product_id of the first order and product_id of the second order.

## Table Structure
The script assumes the existence of a table named `orders` with the following columns:
- `order_id` (int): Primary key for orders
- `customer_id` (int): ID of the customer who placed the order
- `product_id` (varchar(2)): ID of the product purchased

![Day17sql](https://github.com/bhumikadata/Basket-Analysis/assets/131578649/93c30e3d-2d2f-46b6-b449-6251b5ab7055)


## SQL Solution
```sql
SELECT
  o1.product_id AS product_1,
  o2.product_id AS product_2,
  COUNT(o1.order_id) AS purchase_frequency
FROM 
  orders o1
JOIN
  orders o2
ON o1.order_id = o2.order_id
WHERE 
  o1.product_id > o2.product_id    
GROUP BY 
  o1.product_id,
  o2.product_id 
