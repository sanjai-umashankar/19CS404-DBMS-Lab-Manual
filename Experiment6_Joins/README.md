# Experiment 6: Joins

## AIM
To study and implement different types of joins.

## THEORY

SQL Joins are used to combine records from two or more tables based on a related column.

### 1. INNER JOIN
Returns records with matching values in both tables.

**Syntax:**
```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

### 2. LEFT JOIN
Returns all records from the left table, and matched records from the right.

**Syntax:**

```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```
### 3. RIGHT JOIN
Returns all records from the right table, and matched records from the left.

**Syntax:**

```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.column = table2.column;
```
### 4. FULL OUTER JOIN
Returns all records when there is a match in either left or right table.

**Syntax:**

```sql
SELECT columns
FROM table1
FULL OUTER JOIN table2
ON table1.column = table2.column;
```

**Question 1**


<img width="1294" height="631" alt="image" src="https://github.com/user-attachments/assets/fd0df853-8d90-4a7c-b6e0-264d364c9dd9" />


```sql
SELECT p.*
FROM patients p, test_results t
WHERE p.patient_id = t.patient_id
  AND t.test_name IN ('Blood Test','Blood Pressure')
  AND t.result NOT LIKE '%Normal%';

```

**Output:**


<img width="1352" height="261" alt="image" src="https://github.com/user-attachments/assets/2b02cc96-1f50-40e1-9d04-aab3d58c50b0" />


**Question 2**


<img width="1349" height="465" alt="image" src="https://github.com/user-attachments/assets/6f1b720c-1025-4600-b5d1-3258736c6966" />


```sql
SELECT p.first_name AS patient_name, d.first_name AS doctor_name
FROM patients p
JOIN doctors d ON p.doctor_id = d.doctor_id
WHERE p.discharge_date IS NOT NULL;

```

**Output:**


<img width="1362" height="251" alt="image" src="https://github.com/user-attachments/assets/4fbbf387-d051-40fd-8da7-d36f4b2dc965" />


**Question 3**


<img width="1353" height="546" alt="image" src="https://github.com/user-attachments/assets/fe26170c-9f74-4234-9c59-71721f5d35bc" />


```sql
SELECT c.cust_name AS "Customer Name", c.city AS "city",
       s.name AS "Salesman", s.city AS "city", s.commission AS "commission"
FROM customer c
JOIN salesman s ON c.salesman_id = s.salesman_id
WHERE c.city <> s.city AND s.commission > 0.12;

```

**Output:**


<img width="1360" height="383" alt="image" src="https://github.com/user-attachments/assets/86027c40-315d-4190-8244-8ddb32d19164" />


**Question 4**


<img width="1353" height="192" alt="image" src="https://github.com/user-attachments/assets/deff6039-3222-43d7-a487-ce03f0423b93" />


```sql
SELECT s.name
FROM salesman s
LEFT JOIN customer c ON s.salesman_id = c.salesman_id
WHERE c.city = 'New York';

```

**Output:**


<img width="1366" height="251" alt="image" src="https://github.com/user-attachments/assets/90abff0c-7326-429d-a550-55af607a674f" />


**Question 5**


<img width="1350" height="554" alt="image" src="https://github.com/user-attachments/assets/092b88a0-2a20-4981-b326-907b5631c99e" />


```sql
SELECT c.cust_name AS "Customer Name", c.city AS "city",
       s.name AS "Salesman", s.commission AS "commission"
FROM customer c
JOIN salesman s ON c.salesman_id = s.salesman_id
WHERE s.commission > 0.12;

```

**Output:**


<img width="1361" height="474" alt="image" src="https://github.com/user-attachments/assets/a170a4cc-20fb-4448-b007-78be80494f4b" />


**Question 6**


<img width="1358" height="289" alt="image" src="https://github.com/user-attachments/assets/040b000c-9d8e-4646-9680-18afe618b166" />


```sql
SELECT c.*
FROM customer c
LEFT JOIN orders o ON c.customer_id = o.customer_id
WHERE o.ord_date > '2012-08-17';

```

**Output:**


<img width="1359" height="518" alt="image" src="https://github.com/user-attachments/assets/c224ff62-3715-425b-a9f5-004c309be6c4" />


**Question 7**


<img width="1372" height="594" alt="image" src="https://github.com/user-attachments/assets/1dbb23e8-25a3-418f-a4da-a4d16f8c0ddc" />


```sql
SELECT a.cust_name, a.city, b.ord_no,
       b.ord_date, b.purch_amt AS "Order Amount", 
       c.name, c.commission 
-- Specifying the tables to retrieve data from ('customer' as 'a', 'orders' as 'b', and 'salesman' as 'c')
FROM customer a 
-- Performing a left outer join based on the customer_id, including unmatched rows from 'customer'
LEFT OUTER JOIN orders b 
ON a.customer_id = b.customer_id 
-- Performing another left outer join with the result of the previous join and the 'salesman' table based on salesman_id
LEFT OUTER JOIN salesman c 
ON c.salesman_id = b.salesman_id;
```

**Output:**


<img width="1366" height="740" alt="image" src="https://github.com/user-attachments/assets/f38c2aa8-a313-4d49-9cbf-25c554b4a25c" />


**Question 8**


<img width="1337" height="598" alt="image" src="https://github.com/user-attachments/assets/a1bb12e1-f839-48b5-a049-f7433ed60e77" />


```sql
SELECT 
    o.ord_no,
    o.purch_amt,
    o.ord_date,
    c.cust_name,
    c.city AS customer_city,
    c.grade,
    s.name AS salesman_name,
    s.city AS salesman_city,
    s.commission
FROM 
    orders o
JOIN 
    customer c ON o.customer_id = c.customer_id
JOIN 
    salesman s ON o.salesman_id = s.salesman_id;

```

**Output:**


<img width="1408" height="496" alt="image" src="https://github.com/user-attachments/assets/c34b3660-549d-46e4-93ee-575326d456cf" />


**Question 9**


<img width="1328" height="586" alt="image" src="https://github.com/user-attachments/assets/0f6b7c5a-0108-4225-b887-5fe937bfa387" />


```sql
SELECT a.cust_name, a.city, a.grade, 
       b.name AS "Salesman", b.city 
FROM customer a 
LEFT JOIN salesman b 
ON a.salesman_id = b.salesman_id 
ORDER BY a.customer_id;
```

**Output:**


<img width="1368" height="561" alt="image" src="https://github.com/user-attachments/assets/38521ad1-746f-47be-aa68-78b20ac4fb8d" />


**Question 10**


<img width="1358" height="434" alt="image" src="https://github.com/user-attachments/assets/8459b40f-279d-4ea5-9785-27692eb7d6d2" />


```sql
SELECT 
    p.first_name AS patient_name,
    t.test_name
FROM patients p
INNER JOIN test_results t 
    ON p.patient_id = t.patient_id;

```

**Output:**


<img width="1369" height="341" alt="image" src="https://github.com/user-attachments/assets/a89a393a-5feb-4f24-8b17-ca0d9aca724c" />



## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
