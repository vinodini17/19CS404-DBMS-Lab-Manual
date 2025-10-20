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
--
Write the SQL query that accomplishes the selection of the first name from the "patients" table and all columns from the "surgeries" table, with an inner join on the "patient_id" column and a condition filtering for patients with the first name 'Alice'.
--
PATIENTS TABLE:
| Name           | Type         |
|----------------|--------------|
| patient_id     | INT          |
| first_name     | VARCHAR(50)  |
| last_name      | VARCHAR(50)  |
| date_of_birth  | DATE         |
| admission_date | DATE         |
| discharge_date | DATE         |
| doctor_id      | INT          |

SURGERIES TABLE:
| Name         | Type |
|--------------|------|
| surgery_id   | INT  |
| patient_id   | INT  |
| surgeon_id   | INT  |
| surgery_date | DATE |


```sql
SELECT p.first_name, s.*
FROM patients p
INNER JOIN surgeries s 
    ON p.patient_id = s.patient_id
WHERE p.first_name = 'Alice';
```

**Output:**
<img width="1334" height="280" alt="image" src="https://github.com/user-attachments/assets/afccd115-1e30-4a17-8d30-a6120daef9fe" />


**Question 2**
---
Write the SQL query that achieves the selection of the "name" column from the "salesman" table (aliased as "s"), with a left join on the "salesman_id" column and a condition filtering for customers in the city 'London'.
---
Customer Table:

<img width="465" height="76" alt="image" src="https://github.com/user-attachments/assets/9141791c-7196-4496-add7-9b2cdabdb28f" />

Salesmen Table:

<img width="462" height="75" alt="image" src="https://github.com/user-attachments/assets/603a83ad-2834-4068-bd0e-50a9ab5ab50d" />


```sql
SELECT DISTINCT s.name
FROM salesman s
LEFT JOIN customer c 
    ON s.salesman_id = c.salesman_id
WHERE c.city = 'London';
```

**Output:**
<img width="1340" height="334" alt="image" src="https://github.com/user-attachments/assets/11b6a543-d3d2-49fd-8f61-b1427e867bbd" />

**Question 3**
---
Write the SQL query that achieves the selection of all columns from the "nurses" table (aliased as "n"), with an inner join on the "department_id" column and a condition filtering for nurses in the 'Pediatrics' department.
---
NURSES TABLE:

<img width="469" height="80" alt="image" src="https://github.com/user-attachments/assets/04f009bc-2f28-4c77-b4ba-88de5ca6b1c1" />

DEPARTMENTS TABLE:

<img width="461" height="79" alt="image" src="https://github.com/user-attachments/assets/38e334ce-8d1f-4356-9ca5-67d4b16dd9a1" />


```sql
SELECT n.*
FROM nurses n
INNER JOIN departments d
    ON n.department_id = d.department_id
WHERE d.department_name = 'Pediatrics';
```

**Output:**
<img width="1338" height="290" alt="image" src="https://github.com/user-attachments/assets/e131806e-6d24-4447-bacb-4049e22805fd" />

**Question 4**
---
Write the SQL query that achieves the selection of the "name" column from the "salesman" table (aliased as "s"), the "cust_name," "city," "grade," and "salesman_id" columns from the "customer" table (aliased as "c"), with a left join on the "salesman_id" column and a condition filtering for customers with a grade less than or equal to 100.
---
Customer Table:

<img width="1317" height="214" alt="image" src="https://github.com/user-attachments/assets/6c359f29-8fff-4c88-be94-126858430a30" />

Salesmen Table:

<img width="1311" height="210" alt="image" src="https://github.com/user-attachments/assets/19831067-a351-44d4-8c18-ffedcd4ecc3d" />


```sql
SELECT s.name,
       c.cust_name,
       c.city,
       c.grade,
       c.salesman_id
FROM salesman s
LEFT JOIN customer c
    ON s.salesman_id = c.salesman_id
WHERE c.grade <= 100;
```

**Output:**
<img width="1336" height="385" alt="image" src="https://github.com/user-attachments/assets/3d546e1c-680e-4bfc-8570-39c598aa28de" />

**Question 5**
---
From the following tables write a SQL query to find the details of an order. Return ord_no, ord_date, purch_amt, Customer Name, grade, Salesman, commission. 
---
Sample table: orders

| ord_no | purch_amt | ord_date   | customer_id | salesman_id |
|--------|-----------|------------|-------------|-------------|
| 70001  | 150.50    | 2012-10-05 | 3005        | 5002        |
| 70009  | 270.65    | 2012-09-10 | 3001        | 5005        |
| 70002  | 65.26     | 2012-10-05 | 3002        | 5001        |
| 70004  | 110.50    | 2012-08-17 | 3009        | 5003        |
| 70007  | 948.50    | 2012-09-10 | 3005        | 5002        |
| 70005  | 2400.60   | 2012-07-27 | 3007        | 5001        |
| 70008  | 5760.00   | 2012-09-10 | 3002        | 5001        |
| 70010  | 1983.43   | 2012-10-10 | 3004        | 5006        |
| 70003  | 2480.40   | 2012-10-10 | 3009        | 5003        |
| 70012  | 250.45    | 2012-06-27 | 3008        | 5002        |
| 70011  | 75.29     | 2012-08-17 | 3003        | 5007        |
| 70013  | 3045.60   | 2012-04-25 | 3002        | 5001        |

Sample table: customer

| customer_id | cust_name      | city       | grade | salesman_id |
|------------|----------------|------------|-------|-------------|
| 3002       | Nick Rimando   | New York   | 100   | 5001        |
| 3007       | Brad Davis     | New York   | 200   | 5001        |
| 3005       | Graham Zusi    | California | 200   | 5002        |
| 3008       | Julian Green   | London     | 300   | 5002        |
| 3004       | Fabian Johnson | Paris      | 300   | 5006        |
| 3009       | Geoff Cameron  | Berlin     | 100   | 5003        |
| 3003       | Jozy Altidor   | Moscow     | 200   | 5007        |
| 3001       | Brad Guzan     | London     |       | 5005        |

Sample table: salesman

| salesman_id | name       | city      | commission |
|------------|------------|----------|------------|
| 5001       | James Hoog | New York | 0.15       |
| 5002       | Nail Knite | Paris    | 0.13       |
| 5005       | Pit Alex   | London   | 0.11       |
| 5006       | Mc Lyon    | Paris    | 0.14       |
| 5007       | Paul Adam  | Rome     | 0.13       |
| 5003       | Lauson Hen | San Jose | 0.12       |


```sql
SELECT 
    o.ord_no,
    o.ord_date,
    o.purch_amt,
    c.cust_name AS "Customer Name",
    c.grade,
    s.name AS "Salesman",
    s.commission
FROM 
    orders o
JOIN 
    customer c ON o.customer_id = c.customer_id
JOIN 
    salesman s ON o.salesman_id = s.salesman_id;
```

**Output:**
<img width="1336" height="771" alt="image" src="https://github.com/user-attachments/assets/305791ad-9c36-448c-9557-64ffc0a7c018" />

**Question 6**
---
Write the SQL query that achieves the selection of all columns from the "patients" table, with an inner join on the "doctor_id" column, and includes a condition filtering for patients whose doctors have the first name 'John' and last name 'Smith'.
---
PATIENTS TABLE:

| Name           | Type         |
|----------------|--------------|
| patient_id     | INT          |
| first_name     | VARCHAR(50)  |
| last_name      | VARCHAR(50)  |
| date_of_birth  | DATE         |
| admission_date | DATE         |
| discharge_date | DATE         |
| doctor_id      | INT          |

DOCTORS TABLE:
| Name           | Type         |
|----------------|--------------|
| doctor_id      | INT          |
| first_name     | VARCHAR(50)  |
| last_name      | VARCHAR(50)  |
| specialization | VARCHAR(100) |

```sql
SELECT p.*
FROM patients p
INNER JOIN doctors d
  ON p.doctor_id = d.doctor_id
WHERE d.first_name = 'John'
  AND d.last_name = 'Smith';
```

**Output:**
<img width="1335" height="292" alt="image" src="https://github.com/user-attachments/assets/905d9241-a157-430d-8906-ff0c82a56dd0" />

**Question 7**
---
Write the SQL query that achieves the selection of all columns from the "patients" table (aliased as "p"), with an inner join on the "patient_id" column and conditions filtering for test results with the test name 'X-Ray' and a result of 'Normal'.
---
PATIENTS TABLE:

<img width="1250" height="207" alt="image" src="https://github.com/user-attachments/assets/e604482a-c4f8-41c7-bc3e-765b972c27be" />

TEST_RESULT TABLES:

<img width="1254" height="195" alt="image" src="https://github.com/user-attachments/assets/631bea53-e2c2-4448-b76a-df7bca6daafb" />

```sql
SELECT p.*
FROM patients p
INNER JOIN test_results t ON p.patient_id = t.patient_id
WHERE t.test_name = 'X-Ray'
  AND t.result = 'Normal';
```

**Output:**
<img width="1676" height="363" alt="image" src="https://github.com/user-attachments/assets/68ba9d98-fa88-4687-ac12-15c430234d38" />

**Question 8**
---
Write the SQL query that accomplishes the selection of the first name and last name from the "patients" table, with an inner join on the "patient_id" column and a condition filtering for surgeries with a surgery date between '2024-01-01' and '2024-01-31'.
---
PATIENTS TABLE:
| Name           | Type         |
|----------------|--------------|
| patient_id     | INT          |
| first_name     | VARCHAR(50)  |
| last_name      | VARCHAR(50)  |
| date_of_birth  | DATE         |
| admission_date | DATE         |
| discharge_date | DATE         |
| doctor_id      | INT          |


SURGERIES TABLE:
| Name         | Type |
|--------------|------|
| surgery_id   | INT  |
| patient_id   | INT  |
| surgeon_id   | INT  |
| surgery_date | DATE |

```sql
SELECT p.first_name, p.last_name
FROM patients p
INNER JOIN surgeries s
  ON p.patient_id = s.patient_id
WHERE s.surgery_date BETWEEN '2024-01-01' AND '2024-01-31';
```

**Output:**
<img width="1670" height="361" alt="image" src="https://github.com/user-attachments/assets/85d029c4-87ed-40ac-9272-2f485cc4f535" />


**Question 9**
---
Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and all columns from the "appointments" table (aliased as "a"), with an inner join on the "patient_id" column.
---
PATIENTS TABLE:

<img width="1322" height="207" alt="image" src="https://github.com/user-attachments/assets/3085d869-5b76-48f5-9c39-1d5185ad657c" />

APPOINTMENTS TABLE:

<img width="1321" height="213" alt="image" src="https://github.com/user-attachments/assets/7cb1881d-fb8e-43ab-874a-ddbbbb770cb2" />


```sql
SELECT p.first_name AS patient_name, a.*
FROM patients p
INNER JOIN appointments a
  ON p.patient_id = a.patient_id;
```

**Output:**
<img width="1437" height="404" alt="image" src="https://github.com/user-attachments/assets/797c60fd-d0e4-4d07-ba59-8ac9b83c2a95" />

**Question 10**
---
From the following tables write a SQL query to locate those salespeople who do not live in the same city where their customers live and have received a commission of more than 12% from the company. Return Customer Name, customer city, Salesman, salesman city, commission.  
---
Sample table: customer
| customer_id | cust_name      | city       | grade | salesman_id |
|------------|----------------|------------|-------|-------------|
| 3002       | Nick Rimando   | New York   | 100   | 5001        |
| 3007       | Brad Davis     | New York   | 200   | 5001        |
| 3005       | Graham Zusi    | California | 200   | 5002        |
| 3008       | Julian Green   | London     | 300   | 5002        |
| 3004       | Fabian Johnson | Paris      | 300   | 5006        |
| 3009       | Geoff Cameron  | Berlin     | 100   | 5003        |
| 3003       | Jozy Altidor   | Moscow     | 200   | 5007        |
| 3001       | Brad Guzan     | London     |       | 5005        |

Sample table: salesman
| salesman_id | name       | city      | commission |
|------------|------------|----------|------------|
| 5001       | James Hoog | New York | 0.15       |
| 5002       | Nail Knite | Paris    | 0.13       |
| 5005       | Pit Alex   | London   | 0.11       |
| 5006       | Mc Lyon    | Paris    | 0.14       |
| 5007       | Paul Adam  | Rome     | 0.13       |
| 5003       | Lauson Hen | San Jose | 0.12       |

```sql
SELECT
  c.cust_name      AS "Customer Name",
  c.city           AS "city",
  s.name           AS "Salesman",
  s.city           AS "city",
  s.commission
FROM customer c
JOIN salesman s
  ON c.salesman_id = s.salesman_id
WHERE c.city <> s.city
  AND s.commission > 0.12;
```

**Output:**
<img width="1444" height="446" alt="image" src="https://github.com/user-attachments/assets/1935dc45-86b2-403a-aa26-24ea543b4b63" />


## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
