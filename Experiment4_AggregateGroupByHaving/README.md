# Experiment 4: Aggregate Functions, Group By and Having Clause

## AIM
To study and implement aggregate functions, GROUP BY, and HAVING clause with suitable examples.

## THEORY

### Aggregate Functions
These perform calculations on a set of values and return a single value.

- **MIN()** – Smallest value  
- **MAX()** – Largest value  
- **COUNT()** – Number of rows  
- **SUM()** – Total of values  
- **AVG()** – Average of values

**Syntax:**
```sql
SELECT AGG_FUNC(column_name) FROM table_name WHERE condition;
```
### GROUP BY
Groups records with the same values in specified columns.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name;
```
### HAVING
Filters the grouped records based on aggregate conditions.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

**Question 1**
--
Write a SQL query to find the average length of email addresses (in characters):
--
Table: customer
| Name  | Type    |
|-------|---------|
| id    | INTEGER |
| name  | TEXT    |
| city  | TEXT    |
| email | TEXT    |
| phone | INTEGER |
```sql
SELECT AVG(LENGTH(email)) AS avg_email_length
FROM customer;
```
**Output:**
<img width="1146" height="455" alt="image" src="https://github.com/user-attachments/assets/eb9c4e66-8e6b-4bbd-b2ef-62d1020d22f9" />

**Question 2**
---
Write a SQL query that counts the number of unique salespeople. Return number of salespeople.
---
Sample table: orders
| ord_no | purch_amt | ord_date   | customer_id | salesman_id |
|--------|-----------|------------|-------------|-------------|
| 70001  | 150.50    | 2012-10-05 | 3005        | 5002        |
| 70009  | 270.65    | 2012-09-10 | 3001        | 5005        |
| 70002  | 65.26     | 2012-10-05 | 3002        | 5001        |
```sql
SELECT COUNT(DISTINCT salesman_id) AS COUNT
FROM orders;
```
**Output:**
<img width="1155" height="458" alt="image" src="https://github.com/user-attachments/assets/ba8a2c8c-d90f-4caa-b1f4-99228f7b3d33" />

**Question 3**
---
Write a SQL query to find the minimum purchase amount.
---
| ord_no | purch_amt | ord_date   | customer_id | salesman_id |
|--------|-----------|------------|-------------|-------------|
| 70001  | 150.50    | 2012-10-05 | 3005        | 5002        |
| 70009  | 270.65    | 2012-09-10 | 3001        | 5005        |
| 70002  | 65.26     | 2012-10-05 | 3002        | 5001        |
```sql
SELECT MIN(purch_amt) AS MINIMUM
FROM orders;
```
**Output:**
<img width="1150" height="463" alt="image" src="https://github.com/user-attachments/assets/bc6c01d5-a54f-42ac-9030-b1beec5bf900" />

**Question 4**
---
How many medical records are there for each patient?
---
Sample table:MedicalRecords Table
<img width="1151" height="175" alt="image" src="https://github.com/user-attachments/assets/3b35ab9e-7ffd-45f3-b537-cda18b46784d" />
```sql
SELECT PatientID, COUNT(*) AS TotalRecords
FROM MedicalRecords
GROUP BY PatientID;
```
**Output:**
<img width="1157" height="870" alt="image" src="https://github.com/user-attachments/assets/3594dc33-57f3-4c2f-a2c9-0f181e131442" />

**Question 5**
---
What is the average dosage prescribed for each medication?
---
Sample tablePrescriptions Table
<img width="1136" height="166" alt="image" src="https://github.com/user-attachments/assets/c969c6d3-b012-4f4e-b33a-61fab2a5977e" />
```sql
SELECT Medication, AVG(Dosage) AS AvgDosage
FROM Prescriptions
GROUP BY Medication;
```
**Output:**
<img width="1235" height="800" alt="image" src="https://github.com/user-attachments/assets/36b0085a-4465-4c07-8196-9e04b8fcfd61" />

**Question 6**
---
How many patients are there in each city?
---
Sample table: Patients Table
<img width="922" height="143" alt="image" src="https://github.com/user-attachments/assets/d8196b0f-8840-4ce9-81d4-7f4430d571d2" />
```sql
SELECT Address, COUNT(*) AS TotalPatients
FROM Patients
GROUP BY Address;
```
**Output:**
<img width="1221" height="458" alt="image" src="https://github.com/user-attachments/assets/068f057a-b073-4df1-89cd-d4e449761dbe" />

**Question 7**
---
Write the SQL query to find how many patients have more than 3 medical records?.
---
Sample table: MedicalRecords
| Name       | Type     |
|------------|----------|
| RecordID   | INTEGER  |
| PatientID  | INTEGER  |
| DoctorID   | INTEGER  |
| Date       | DATE     |
| Diagnosis  | TEXT     |
| Treatment  | TEXT     |
| Medication | TEXT     |
```sql
SELECT PatientID, COUNT(*) AS TotalRecords
FROM MedicalRecords
GROUP BY PatientID
HAVING COUNT(*) > 3;
```
**Output:**
<img width="1221" height="382" alt="image" src="https://github.com/user-attachments/assets/1bfb123b-b760-47db-9d15-f004ab41dec9" />

**Question 8**
---
Write the SQL query that achieves the grouping of data by age intervals using the expression (age/5)5, calculates the total salary sum for each group, and excludes groups where the total salary sum is not greater than 5000.
---
Sample table: customer1
<img width="746" height="127" alt="image" src="https://github.com/user-attachments/assets/98a2aa33-e353-4a2d-9d55-4322b77c928d" />
```sql
SELECT (age/5)*5 AS age_group, SUM(salary) AS "SUM(salary)"
FROM customer1
GROUP BY (age/5)*5
HAVING SUM(salary) > 5000;
```
**Output:**
<img width="1224" height="409" alt="image" src="https://github.com/user-attachments/assets/d9679e60-7134-4b7b-a7ae-9ea98581312f" />

**Question 9**
---
Write the SQL query that performs grouping by age groups and displays the maximum salary for each group, excluding groups where the maximum salary is not greater than 8000. 
---
Note: Calculate the age group as multiples of 5.

Eg., 20,22,23 comes in age group 20. 

25,27,29 comes in age group 25.

Sample table: customer1
<img width="752" height="136" alt="image" src="https://github.com/user-attachments/assets/f9403edd-d1da-4f36-86b2-fff53e83d2cf" />
```sql
SELECT (age/5)*5 AS age_group, MAX(salary) AS "MAX(salary)"
FROM customer1
GROUP BY (age/5)*5
HAVING MAX(salary) > 8000;
```
**Output:**
<img width="1218" height="408" alt="image" src="https://github.com/user-attachments/assets/f19fe645-168f-437f-b318-c9810034c657" />

**Question 10**
---
Write the SQL query that achieves the grouping of data by age intervals using the expression (age/5)5, calculates the average age for each group, and excludes groups where the average age is not less than 24.
---
Sample table: customer1
<img width="741" height="127" alt="image" src="https://github.com/user-attachments/assets/8d986137-e866-476c-b60e-1d32b8ad8e37" />
```sql
SELECT (age/5)*5 AS age_group, AVG(age) AS "AVG(age)"
FROM customer1
GROUP BY (age/5)*5
HAVING AVG(age) < 24;
```
**Output:**
<img width="1228" height="369" alt="image" src="https://github.com/user-attachments/assets/9e2c89f9-04b8-424e-87ac-d7ed56c51301" />

## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
