# Case Study #1 - Danny's Diner

![image.png](Danny's_Diner_files/image.png)

## Introduction

Danny seriously loves Japanese food so in the beginning of 2021, he decides to embark upon a risky venture and opens up a cute little restaurant that sells his 3 favourite foods: sushi, curry and ramen.

Danny’s Diner is in need of your assistance to help the restaurant stay afloat - the restaurant has captured some very basic data from their few months of operation but have no idea how to use their data to help them run the business.

## Problem Statement

Danny wants to use the data to answer a few simple questions about his customers, especially about their visiting patterns, how much money they’ve spent and also which menu items are their favourite. Having this deeper connection with his customers will help him deliver a better and more personalised experience for his loyal customers.

He plans on using these insights to help him decide whether he should expand the existing customer loyalty program - additionally he needs help to generate some basic datasets so his team can easily inspect the data without needing to use SQL.

Danny has provided you with a sample of his overall customer data due to privacy issues - but he hopes that these examples are enough for you to write fully functioning SQL queries to help him answer his questions!

Danny has shared with you 3 key datasets for this case study:

- sales
- menu
- members

## Entity Relationship Diagram
![image-2.png](attachment:image-2.png)

## Example Datasets
All datasets exist within the dannys_diner database schema - be sure to include this reference within your SQL scripts as you start exploring the data and answering the case study questions.

Table 1: sales
The sales table captures all customer_id level purchases with an corresponding order_date and product_id information for when and what menu items were ordered.

customer_id | order_date | product_id
------------|------------|-----------
A | 2021-01-01 | 1
A | 2021-01-01 | 2
A | 2021-01-07 | 2
A | 2021-01-10 | 3
A | 2021-01-11 | 3
A | 2021-01-11 | 3
B | 2021-01-01 | 2
B | 2021-01-02 | 2
B | 2021-01-04 | 1
B | 2021-01-11 | 1
B | 2021-01-16 | 3
B | 2021-02-01 | 3
C | 2021-01-01 | 3
C | 2021-01-01 | 3
C | 2021-01-07 | 3


Table 2: menu
The menu table maps the product_id to the actual product_name and price of each menu item.

product_id | product_name | price
-----------|--------------|------
1 | sushi | 10
2 | curry | 15
3 | ramen | 12


Table 3: members
The final members table captures the join_date when a customer_id joined the beta version of the Danny’s Diner loyalty program.

customer_id | join_date
------------|----------
A | 2021-01-07
B | 2021-01-09

### Interactive SQL Session

You can use Online Platform like DB Fiddle to have interactive session in minutes or You can use Jupter Notebook to solve this case study or use any IDEA  like VS code, Snowflake, Databrick or BigQuery Practise as you wish.

Most of time i work with VS code and Juypter Notebook, so I am Solving the Query using this Way

- ipython-sql or jupysql
- psycopg2
- sqlalchemy




```python
# to connect the Database we need to invoke the SQL magic function %%sql
%load_ext sql

# to connect to database
%sql postgresql://postgres:krish@127.0.0.1:5432/kanna
```

Loading Schema into the postgresql database from juypter notebook itself.


```sql
%%sql

CREATE SCHEMA dannys_diner;
SET search_path = dannys_diner;

CREATE TABLE sales (
  "customer_id" VARCHAR(1),
  "order_date" DATE,
  "product_id" INTEGER
);

INSERT INTO sales
  ("customer_id", "order_date", "product_id")
VALUES
  ('A', '2021-01-01', '1'),
  ('A', '2021-01-01', '2'),
  ('A', '2021-01-07', '2'),
  ('A', '2021-01-10', '3'),
  ('A', '2021-01-11', '3'),
  ('A', '2021-01-11', '3'),
  ('B', '2021-01-01', '2'),
  ('B', '2021-01-02', '2'),
  ('B', '2021-01-04', '1'),
  ('B', '2021-01-11', '1'),
  ('B', '2021-01-16', '3'),
  ('B', '2021-02-01', '3'),
  ('C', '2021-01-01', '3'),
  ('C', '2021-01-01', '3'),
  ('C', '2021-01-07', '3');
 

CREATE TABLE menu (
  "product_id" INTEGER,
  "product_name" VARCHAR(5),
  "price" INTEGER
);

INSERT INTO menu
  ("product_id", "product_name", "price")
VALUES
  ('1', 'sushi', '10'),
  ('2', 'curry', '15'),
  ('3', 'ramen', '12');
  

CREATE TABLE members (
  "customer_id" VARCHAR(1),
  "join_date" DATE
);

INSERT INTO members
  ("customer_id", "join_date")
VALUES
  ('A', '2021-01-07'),
  ('B', '2021-01-09');
```


<span style="None">Running query in &#x27;postgresql://postgres:***@127.0.0.1:5432/kanna&#x27;</span>



<span style="color: green">15 rows affected.</span>



<span style="color: green">3 rows affected.</span>



<span style="color: green">2 rows affected.</span>





<table>
    <thead>
        <tr>
        </tr>
    </thead>
    <tbody>
    </tbody>
</table>




```sql
%%sql

SELECT * FROM dannys_diner.menu
```


<span style="None">Running query in &#x27;postgresql://postgres:***@127.0.0.1:5432/kanna&#x27;</span>



<span style="color: green">3 rows affected.</span>





<table>
    <thead>
        <tr>
            <th>product_id</th>
            <th>product_name</th>
            <th>price</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>1</td>
            <td>sushi</td>
            <td>10</td>
        </tr>
        <tr>
            <td>2</td>
            <td>curry</td>
            <td>15</td>
        </tr>
        <tr>
            <td>3</td>
            <td>ramen</td>
            <td>12</td>
        </tr>
    </tbody>
</table>




```sql
%%sql

SELECT * FROM dannys_diner.sales
```


<span style="None">Running query in &#x27;postgresql://postgres:***@127.0.0.1:5432/kanna&#x27;</span>



<span style="color: green">15 rows affected.</span>





<table>
    <thead>
        <tr>
            <th>customer_id</th>
            <th>order_date</th>
            <th>product_id</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>A</td>
            <td>2021-01-01</td>
            <td>1</td>
        </tr>
        <tr>
            <td>A</td>
            <td>2021-01-01</td>
            <td>2</td>
        </tr>
        <tr>
            <td>A</td>
            <td>2021-01-07</td>
            <td>2</td>
        </tr>
        <tr>
            <td>A</td>
            <td>2021-01-10</td>
            <td>3</td>
        </tr>
        <tr>
            <td>A</td>
            <td>2021-01-11</td>
            <td>3</td>
        </tr>
        <tr>
            <td>A</td>
            <td>2021-01-11</td>
            <td>3</td>
        </tr>
        <tr>
            <td>B</td>
            <td>2021-01-01</td>
            <td>2</td>
        </tr>
        <tr>
            <td>B</td>
            <td>2021-01-02</td>
            <td>2</td>
        </tr>
        <tr>
            <td>B</td>
            <td>2021-01-04</td>
            <td>1</td>
        </tr>
        <tr>
            <td>B</td>
            <td>2021-01-11</td>
            <td>1</td>
        </tr>
    </tbody>
</table>
<span style="font-style:italic;text-align:center;">Truncated to <a href="https://jupysql.ploomber.io/en/latest/api/configuration.html#displaylimit">displaylimit</a> of 10.</span>




```sql
%%sql

SELECT * FROM dannys_diner.members
```


<span style="None">Running query in &#x27;postgresql://postgres:***@127.0.0.1:5432/kanna&#x27;</span>



<span style="color: green">2 rows affected.</span>





<table>
    <thead>
        <tr>
            <th>customer_id</th>
            <th>join_date</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>A</td>
            <td>2021-01-07</td>
        </tr>
        <tr>
            <td>B</td>
            <td>2021-01-09</td>
        </tr>
    </tbody>
</table>



## Case Study Questions
Each of the following case study questions can be answered using a single SQL statement:

1. What is the total amount each customer spent at the restaurant?
2. How many days has each customer visited the restaurant?
3. What was the first item from the menu purchased by each customer?
4. What is the most purchased item on the menu and how many times was it purchased by all customers?
5. Which item was the most popular for each customer?
6. Which item was purchased first by the customer after they became a member?
7. Which item was purchased just before the customer became a member?
8. What is the total items and amount spent for each member before they became a member?
9. If each $1 spent equates to 10 points and sushi has a 2x points multiplier - how many points would each customer have?
10. In the first week after a customer joins the program (including their join date) they earn 2x points on all items, not just sushi - how many points do customer A and B have at the end of January?

## 1. What is the total amount each customer spent at the restaurant?

How you can approach this SQL problem,
- step 1 - choose column you need,
    - `customer_id`, `price`
    - `dannys_diner.sales` is not enough to answer this question, you need `dannys_diner.menu` tables as well cause price column available. 

- step 2 - choose what type of join you gone use?
    - Use **JOIN** to merge `dannys_diner.sales` and `dannys_diner.menu` tables as `sales.customer_id` and `menu.price` are from both tables.
- step 3 - how to get total amount of each customer?
    - Use **SUM** to calculate the total sales contributed by each customer.
    - Group the aggregated results by `sales.customer_id`.


```sql
%%sql

SELECT s.customer_id, sum(m.price)
FROM dannys_diner.sales s 
JOIN dannys_diner.menu m 
ON s.product_id = m.product_id
GROUP BY s.customer_id
ORDER BY s.customer_id ASC
```


<span style="None">Running query in &#x27;postgresql://postgres:***@127.0.0.1:5432/kanna&#x27;</span>



<span style="color: green">3 rows affected.</span>





<table>
    <thead>
        <tr>
            <th>customer_id</th>
            <th>sum</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>A</td>
            <td>76</td>
        </tr>
        <tr>
            <td>B</td>
            <td>74</td>
        </tr>
        <tr>
            <td>C</td>
            <td>36</td>
        </tr>
    </tbody>
</table>



## 2. How many days has each customer visited the restaurant?

How you can approach this SQL problem,
- step 1 - choose column you need,
    - `customer_id`, new column which display count of customer visited `count`
    - `dannys_diner.sales` is enough to answer this question. 

- step 2 - choose which SQL keyword will be useful to solve the problem
    - `DISTINCT` prevents overcounting: This keyword ensures that each unique order date is counted only once, even if a customer made multiple visits on the same day.
    - Accurate visit count: This approach provides a precise representation of how many different days each customer has visited.
    - Use `COUNT` keyword to count distinct order_date

- **NOTE:**
    - as customer visited count is calculated based on order_date, so consider customer visited single time in a day, even though we have multiple order, it is not make valueable sense to consider each order_date as each time customer visited.


```sql
%%sql

SELECT s.customer_id, COUNT(DISTINCT(s.order_date))
from dannys_diner.sales as s
GROUP BY s.customer_id

```


<span style="None">Running query in &#x27;postgresql://postgres:***@127.0.0.1:5432/kanna&#x27;</span>



<span style="color: green">3 rows affected.</span>





<table>
    <thead>
        <tr>
            <th>customer_id</th>
            <th>count</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>A</td>
            <td>4</td>
        </tr>
        <tr>
            <td>B</td>
            <td>6</td>
        </tr>
        <tr>
            <td>C</td>
            <td>2</td>
        </tr>
    </tbody>
</table>



## 3.What was the first item from the menu purchased by each customer?

How to approach this SQL Problem,

- Step 1: Choose Necessary Columns
- [ ] We need `customer_id` and product_name from the `dannys_diner.sales` and `dannys_diner.menu` tables, respectively.
- [ ] Also, we require the `_order_date_` from the `dannys_diner.sales` table to identify the earliest purchase date.
- Step 2: Determine the Join Type
- [ ] Perform an INNER JOIN to merge the `dannys_diner.sales` and `dannys_diner.menu` tables based on the common column `product_id`.
- Step 3: Rank and Filter to Identify the First Item
- [ ] Use a ranking function like `ROW_NUMBER()` or `DENSE_RANK()` to assign a sequential number to each product purchased by a customer, ordered by the order_date.
- [ ] Filter the results to fetch only the rows where the ranking is 1 for each customer, indicating their first purchase.

Method 1 - using DENSE RANK


```sql
%%sql

WITH ordered_sales AS (
  SELECT 
    sales.customer_id, 
    sales.order_date, 
    menu.product_name,
    DENSE_RANK() OVER (
      PARTITION BY sales.customer_id 
      ORDER BY sales.order_date) AS rank
  FROM dannys_diner.sales
  INNER JOIN dannys_diner.menu
    ON sales.product_id = menu.product_id
)

SELECT 
  customer_id, 
  product_name
FROM ordered_sales
WHERE rank = 1
GROUP BY customer_id, product_name;
```


<span style="None">Running query in &#x27;postgresql://postgres:***@127.0.0.1:5432/kanna&#x27;</span>



<span style="color: green">4 rows affected.</span>





<table>
    <thead>
        <tr>
            <th>customer_id</th>
            <th>product_name</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>A</td>
            <td>curry</td>
        </tr>
        <tr>
            <td>A</td>
            <td>sushi</td>
        </tr>
        <tr>
            <td>B</td>
            <td>curry</td>
        </tr>
        <tr>
            <td>C</td>
            <td>ramen</td>
        </tr>
    </tbody>
</table>



Method 2 - Using ROW_NUMBER


```sql
%%sql
WITH ranked_sales AS (
    SELECT 
        s.customer_id, 
        m.product_name,
        ROW_NUMBER() OVER (PARTITION BY s.customer_id ORDER BY s.order_date) AS rank
    FROM 
        dannys_diner.sales s
    INNER JOIN 
        dannys_diner.menu m ON s.product_id = m.product_id
)

SELECT 
    customer_id, 
    product_name
FROM 
    ranked_sales
WHERE 
    rank = 1;

```


<span style="None">Running query in &#x27;postgresql://postgres:***@127.0.0.1:5432/kanna&#x27;</span>



<span style="color: green">3 rows affected.</span>





<table>
    <thead>
        <tr>
            <th>customer_id</th>
            <th>product_name</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>A</td>
            <td>curry</td>
        </tr>
        <tr>
            <td>B</td>
            <td>curry</td>
        </tr>
        <tr>
            <td>C</td>
            <td>ramen</td>
        </tr>
    </tbody>
</table>



As you can see there is huge difference using `ROW_NUMBER` and `DENSE RANK`,

`ROW_NUMBER` simply assigns a sequential number to each row within each partition (defined by customer_id) based on the order of order_date. It doesn't care about ties in the ordering column. So, even if two customers have the same first order date, they might not both get the same rank of 1.

`DENSE_RANK,` on the other hand, does care about ties. If two customers have the same first order date, they will both get the same rank of 1. However, it ensures no gaps in the ranking sequence. So, the next customer (after the two tied customers) will get a rank of 3, not 2, to maintain the dense sequence.


### Method 3: Finding the First Purchase for Each Customer

#### Explanation:

1. **Selecting Necessary Columns:**
   - The query aims to retrieve `customer_id` from the `sales` table and `product_name` from the `menu` table.

2. **Determining the Join Type:**
   - The query performs an **INNER JOIN** between the `sales` and `menu` tables, utilizing the common `product_id`.

3. **Identifying the First Purchase for Each Customer:**
   - The `WHERE` clause within the query filters rows from the `sales` table based on the condition that the `order_date` matches the earliest `order_date` found for each `customer_id`. This is achieved by using a subquery that finds the minimum `order_date` for each `customer_id`.



```sql
%%sql

SELECT 
  s.customer_id,
  m.product_name
FROM dannys_diner.sales s
INNER JOIN dannys_diner.menu m ON s.product_id = m.product_id
WHERE s.order_date = (
  SELECT MIN(order_date)
  FROM dannys_diner.sales s2
  WHERE s2.customer_id = s.customer_id
)
GROUP BY s.customer_id, m.product_name;

```


<span style="None">Running query in &#x27;postgresql://postgres:***@127.0.0.1:5432/kanna&#x27;</span>



<span style="color: green">4 rows affected.</span>





<table>
    <thead>
        <tr>
            <th>customer_id</th>
            <th>product_name</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>A</td>
            <td>curry</td>
        </tr>
        <tr>
            <td>A</td>
            <td>sushi</td>
        </tr>
        <tr>
            <td>B</td>
            <td>curry</td>
        </tr>
        <tr>
            <td>C</td>
            <td>ramen</td>
        </tr>
    </tbody>
</table>



## 4.What is the most purchased item on the menu and how many times was it purchased by all customers?

How to approach the Problem

#### Step 1: Choose Necessary Columns

*   Select `product_name` from the `dannys_diner.menu` table.
*   Count the occurrences of each product from the `dannys_diner.sales` table.

#### Step 2: Determine the Join Type

*   Utilize an **INNER JOIN** to merge the `dannys_diner.sales` and `dannys_diner.menu` tables based on the common column `product_id`.

#### Step 3: Count Purchase Frequencies

*   Use the **COUNT** function to calculate the number of times each item was purchased.
*   Group the results by `menu.product_name` to count purchases for each item.

#### Step 4: Find the Most Purchased Item

*   Order the results in descending order of purchase count (`most_purchased_item`).
*   Retrieve the top row (item) with the highest purchase count.



```sql
%%sql

SELECT 
    menu.product_name,
    COUNT(sales.product_id) AS most_purchased_item
FROM 
    dannys_diner.sales
INNER JOIN 
    dannys_diner.menu ON sales.product_id = menu.product_id
GROUP BY 
    menu.product_name
ORDER BY 
    most_purchased_item DESC
LIMIT 1;

```


<span style="None">Running query in &#x27;postgresql://postgres:***@127.0.0.1:5432/kanna&#x27;</span>



<span style="color: green">1 rows affected.</span>





<table>
    <thead>
        <tr>
            <th>product_name</th>
            <th>most_purchased_item</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>ramen</td>
            <td>8</td>
        </tr>
    </tbody>
</table>



## 5. Which item was the most popular for each customer?

How to approach the Problem,

To find the most popular item for each customer, the approach involves the following steps:

### Approach to Finding the Most Popular Item for Each Customer

1. **Choose Necessary Columns:**
   - Select `customer_id` and `product_name` columns.

2. **Determine Join Type:**
   - Utilize an **INNER JOIN** to merge the `sales` and `menu` tables based on the common column `product_id`.

3. **Count Each Item's Occurrences for Every Customer:**
   - Use the **COUNT** function to determine how many times each item was purchased by each customer.
   - Group the results by both `customer_id` and `product_name`.

4. **Identify the Most Popular Item for Each Customer:**
   - Apply a ranking function (`ROW_NUMBER()`, `RANK()`, or `DENSE_RANK()`) partitioned by `customer_id` and ordered by the count of purchases (`most_popular_item`).
   - Retrieve the rows where the ranking is 1 for each `customer_id`, indicating the most popular item.

5. **Retrieve the Most Popular Item for Each Customer:**
   - Construct a query to fetch the `customer_id`, `product_name`, and their respective counts or ranks to identify the most popular item for each customer.


Method 1 - using `ROW_NUMBER`


```sql
%%sql

SELECT 
    customer_id,
    product_name,
    most_popular_item
FROM (
    SELECT 
        s.customer_id,
        m.product_name,
        COUNT(*) AS most_popular_item,
        ROW_NUMBER() OVER (PARTITION BY s.customer_id ORDER BY COUNT(*) DESC) AS popularity_rank
    FROM 
        dannys_diner.sales s
    INNER JOIN 
        dannys_diner.menu m ON s.product_id = m.product_id
    GROUP BY 
        s.customer_id, m.product_name
) AS popular_items
WHERE 
    popularity_rank = 1;
```


<span style="None">Running query in &#x27;postgresql://postgres:***@127.0.0.1:5432/kanna&#x27;</span>



<span style="color: green">3 rows affected.</span>





<table>
    <thead>
        <tr>
            <th>customer_id</th>
            <th>product_name</th>
            <th>most_popular_item</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>A</td>
            <td>ramen</td>
            <td>3</td>
        </tr>
        <tr>
            <td>B</td>
            <td>sushi</td>
            <td>2</td>
        </tr>
        <tr>
            <td>C</td>
            <td>ramen</td>
            <td>3</td>
        </tr>
    </tbody>
</table>




```sql
%%sql

SELECT 
    customer_id,
    product_name,
    most_popular_item
FROM (
    SELECT 
        s.customer_id,
        m.product_name,
        COUNT(*) AS most_popular_item,
        RANK() OVER (PARTITION BY s.customer_id ORDER BY COUNT(*) DESC) AS popularity_rank
    FROM 
        dannys_diner.sales s
    INNER JOIN 
        dannys_diner.menu m ON s.product_id = m.product_id
    GROUP BY 
        s.customer_id, m.product_name
) AS popular_items
WHERE 
    popularity_rank = 1;
```


<span style="None">Running query in &#x27;postgresql://postgres:***@127.0.0.1:5432/kanna&#x27;</span>



<span style="color: green">5 rows affected.</span>





<table>
    <thead>
        <tr>
            <th>customer_id</th>
            <th>product_name</th>
            <th>most_popular_item</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>A</td>
            <td>ramen</td>
            <td>3</td>
        </tr>
        <tr>
            <td>B</td>
            <td>sushi</td>
            <td>2</td>
        </tr>
        <tr>
            <td>B</td>
            <td>curry</td>
            <td>2</td>
        </tr>
        <tr>
            <td>B</td>
            <td>ramen</td>
            <td>2</td>
        </tr>
        <tr>
            <td>C</td>
            <td>ramen</td>
            <td>3</td>
        </tr>
    </tbody>
</table>




```sql
%%sql

SELECT 
    customer_id,
    product_name,
    most_popular_item
FROM (
    SELECT 
        s.customer_id,
        m.product_name,
        COUNT(*) AS most_popular_item,
        DENSE_RANK() OVER (PARTITION BY s.customer_id ORDER BY COUNT(*) DESC) AS popularity_rank
    FROM 
        dannys_diner.sales s
    INNER JOIN 
        dannys_diner.menu m ON s.product_id = m.product_id
    GROUP BY 
        s.customer_id, m.product_name
) AS popular_items
WHERE 
    popularity_rank = 1;
```


<span style="None">Running query in &#x27;postgresql://postgres:***@127.0.0.1:5432/kanna&#x27;</span>



<span style="color: green">5 rows affected.</span>





<table>
    <thead>
        <tr>
            <th>customer_id</th>
            <th>product_name</th>
            <th>most_popular_item</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>A</td>
            <td>ramen</td>
            <td>3</td>
        </tr>
        <tr>
            <td>B</td>
            <td>sushi</td>
            <td>2</td>
        </tr>
        <tr>
            <td>B</td>
            <td>curry</td>
            <td>2</td>
        </tr>
        <tr>
            <td>B</td>
            <td>ramen</td>
            <td>2</td>
        </tr>
        <tr>
            <td>C</td>
            <td>ramen</td>
            <td>3</td>
        </tr>
    </tbody>
</table>




```python

```
