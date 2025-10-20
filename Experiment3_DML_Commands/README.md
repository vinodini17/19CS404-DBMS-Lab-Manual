# Experiment 3: DML Commands

## AIM
To study and implement DML (Data Manipulation Language) commands.

## THEORY

### 1. INSERT INTO
Used to add records into a relation.
These are three type of INSERT INTO queries which are as
A)Inserting a single record
**Syntax (Single Row):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES (value_1, value_2, ...);
```
**Syntax (Multiple Rows):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES
(value_1, value_2, ...),
(value_3, value_4, ...);
```
**Syntax (Insert from another table):**
```sql
INSERT INTO table_name SELECT * FROM other_table WHERE condition;
```
### 2. UPDATE
Used to modify records in a relation.
Syntax:
```sql
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
```
### 3. DELETE
Used to delete records from a relation.
**Syntax (All rows):**
```sql
DELETE FROM table_name;
```
**Syntax (Specific condition):**
```sql
DELETE FROM table_name WHERE condition;
```
### 4. SELECT
Used to retrieve records from a table.
**Syntax:**
```sql
SELECT column1, column2 FROM table_name WHERE condition;
```
**Question 1**
--
Write a SQL query to Delete customers from 'customer' table where 'CUST_NAME' contains the substring 'Holmes'.
---
Sample table: Customer

| CUST_CODE | CUST_NAME | CUST_CITY | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT | OUTSTANDING_AMT | PHONE_NO | AGENT_CODE |
|------------|------------|------------|---------------|---------------|--------|--------------|--------------|--------------|----------------|-----------|-------------|
| C00013 | Holmes | London | London | UK | 2 | 6000.00 | 5000.00 | 7000.00 | 4000.00 | BBBBBBB | A003 |
| C00001 | Micheal | New York | New York | USA | 2 | 3000.00 | 5000.00 | 2000.00 | 6000.00 | CCCCCCC | A008 |
| C00020 | Albert | New York | New York | USA | 3 | 5000.00 | 7000.00 | 6000.00 | 6000.00 | BBBBSBB | A008 |

```sql
DELETE FROM Customer
WHERE CUST_NAME LIKE '%Holmes%';

```

**Output:**
<img width="1393" height="245" alt="image" src="https://github.com/user-attachments/assets/b479ae52-1a8a-4eaa-97d2-6ac9380ed6df" />

**Question 2**
---
Write a SQL query to Delete All Doctors whose ID ranges from 2 to 4.
---
Sample table: Doctors

attributes : doctor_id, first_name, last_name, specialization
```sql
DELETE FROM doctors
WHERE doctor_id BETWEEN 2 AND 4;
```

**Output:**
<img width="1392" height="360" alt="image" src="https://github.com/user-attachments/assets/76efd421-d3bd-4325-b87e-6b1a6eb4670c" />

**Question 3**
---
Write a SQL query to find all orders that meet the following conditions. Exclude combinations of order date equal to '2012-08-17' or customer ID greater than 3005 and purchase amount less than 1000.
---
Sample table : orders
| ord_no | purch_amt | ord_date   | customer_id | salesman_id |
|---------|------------|------------|--------------|--------------|
| 70001 | 150.50 | 2012-10-05 | 3005 | 5002 |
| 70009 | 270.65 | 2012-09-10 | 3001 | 5005 |
| 70002 | 65.26 | 2012-10-05 | 3002 | 5001 |
```sql
SELECT *
FROM orders
WHERE NOT (
      ord_date = '2012-08-17'
      OR (customer_id > 3005 AND purch_amt < 1000)
);
```

**Output:**
<img width="1393" height="351" alt="image" src="https://github.com/user-attachments/assets/e2a4cf92-5ecf-494e-8c54-16e7d73243dd" />

**Question 4**
---
write a SQL query to find customers who are either from the city 'New York' or who do not have a grade greater than 100. Return customer_id, cust_name, city, grade, and salesman_id.
---
Sample table: customer
| customer_id | cust_name    | city        | grade | salesman_id |
|--------------|--------------|-------------|--------|--------------|
| 3002 | Nick Rimando | New York | 100 | 5001 |
| 3007 | Brad Davis | New York | 200 | 5001 |
| 3005 | Graham Zusi | California | 200 | 5002 |

```sql
SELECT customer_id, cust_name, city, grade, salesman_id
FROM customer
WHERE city = 'New York'
   OR NOT (grade > 100);
```
**Output:**
<img width="1399" height="197" alt="image" src="https://github.com/user-attachments/assets/f401f895-5156-4d85-904f-19501a85b0f4" />

**Question 5**
---
Write a SQL query to Delete customers from 'customer' table where 'OPENING_AMT' is between 4000 and 6000.
---
Sample table: Customer
| CUST_CODE | CUST_NAME | CUST_CITY | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT | OUTSTANDING_AMT | PHONE_NO | AGENT_CODE |
|------------|------------|------------|---------------|---------------|--------|--------------|--------------|--------------|----------------|-----------|-------------|
| C00013 | Holmes | London | London | UK | 2 | 6000.00 | 5000.00 | 7000.00 | 4000.00 | BBBBBBB | A003 |
| C00001 | Micheal | New York | New York | USA | 2 | 3000.00 | 5000.00 | 2000.00 | 6000.00 | CCCCCCC | A008 |
| C00020 | Albert | New York | New York | USA | 3 | 5000.00 | 7000.00 | 6000.00 | 6000.00 | BBBBSBB | A008 |

```sql
DELETE FROM Customer
WHERE OPENING_AMT BETWEEN 4000 AND 6000;
```
**Output:**
<img width="1390" height="276" alt="image" src="https://github.com/user-attachments/assets/7a34640e-7ce1-4416-bbc4-172360a5f4de" />

**Question 6**
---
Write a SQL statement to change the EMAIL and COMMISSION_PCT column of the following EMPLOYEES table with 'not available' and 0.55 for those employees whose DEPARTMENT_ID is 110.
---
|Employees table|
|---------------|
|employee_id|
|first_name|
|last_name|
|email|
|phone_number|
|hire_date|
|job_id|
|salary|
|commission_pct|
|manager_id|
|department_id|
```sql
UPDATE Employees
SET email = 'not available',
    commission_pct = 0.55
WHERE department_id = 110;
```

**Output:**
<img width="1396" height="176" alt="image" src="https://github.com/user-attachments/assets/8fc75e06-52e4-435c-b69c-d1bbb51cbca8" />

**Question 7**
---
Show the categoryName and description from the categories table sorted by categoryName.
---
| Name         | Type        |
|--------------|------------|
| CategoryID   | INTEGER    |
| CategoryName | VARCHAR(25)|
| Description  | VARCHAR(255)|

```sql
SELECT 
    CategoryName, 
    Description
FROM categories
ORDER BY CategoryName;
```
**Output:**
<img width="1395" height="254" alt="image" src="https://github.com/user-attachments/assets/495aaea7-96ae-4914-ac21-9c589f14c81c" />

**Question 8**
---
Write a SQL query to retrieve the year, month, and day from the hiredate column in the emp table.
---
```sql
SELECT 
    strftime('%Y', hiredate) AS Year,
    strftime('%m', hiredate) AS Month,
    strftime('%d', hiredate) AS Day
FROM emp;
```

**Output:**
<img width="1399" height="185" alt="image" src="https://github.com/user-attachments/assets/b7c55493-1d44-472c-bab3-983142da0df9" />

**Question 9**
---
Write a SQL statement to Update the per_unit_price to 25 and total_price accordingly in purchases table where purchase_date is '2022-08-15' and product_id is 12.
---
<img width="310" height="291" alt="image" src="https://github.com/user-attachments/assets/c2acac8d-9ac0-4789-8ffa-3921b8b2d4e1" />

```sql
UPDATE purchases
SET per_unit_price = 25,
    total_price = quantity * 25
WHERE purchase_date = '2022-08-15'
  AND product_id = 12;
```

**Output:**
<img width="1398" height="235" alt="image" src="https://github.com/user-attachments/assets/244212e8-24fb-4b22-9cf1-00822e0db146" />

**Question 10**
---
Write a SQL statement to update the product_name as 'Grapefruit' whose product_id is 4 in the products table.
---
|products table|
|---------------|
|product_id|
|product_name|
|category_id|
|availability|
```sql
UPDATE products
SET product_name = 'Grapefruit'
WHERE product_id = 4;
```
**Output:**
<img width="1394" height="121" alt="image" src="https://github.com/user-attachments/assets/ce793c0b-18d4-4485-9141-42ad4d9f4157" />

## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
