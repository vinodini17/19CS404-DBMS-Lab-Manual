# ER Diagram Workshop – Submission Template

## Objective
To understand and apply ER modeling concepts by creating ER diagrams for real-world applications.

## Purpose
Gain hands-on experience in designing ER diagrams that represent database structure including entities, relationships, attributes, and constraints.

---

# Scenario A: City Fitness Club Management

**Business Context:**  
FlexiFit Gym wants a database to manage its members, trainers, and fitness programs.

**Requirements:**  
- Members register with name, membership type, and start date.  
- Each member can join multiple programs (Yoga, Zumba, Weight Training).  
- Trainers assigned to programs; a program may have multiple trainers.  
- Members may book personal training sessions with trainers.  
- Attendance recorded for each session.  
- Payments tracked for memberships and sessions.

### ER Diagram:
<img width="752" height="489" alt="image" src="https://github.com/user-attachments/assets/7849e7bd-65e8-47d4-a10c-146a80788283" />


### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
|Members |Member_ID (PK), Name,Contact_Number, Address|Members enroll in programs and make payments|
|Programs|Program_ID (PK), Type, Duration, Fees|Programs are conducted by trainers and joined by members|
|Trainers|Trainer_ID (PK), Name, Specialization, Contact_Number|Trainers conduct programs and handle payments|
|Payments|Payment_ID (PK), Trainer_ID (FK), Amount, Payment_Type, Due_Date|Records payments made through trainers for duties|
|Joins|Member_ID (FK), Program_ID (FK)|Represents relationship between Members and Programs|
|Conducts|Trainer_ID (FK), Program_ID (FK)|Represents relationship between Trainers and Programs|
|Duty|Trainer_ID (FK), Payment_ID (FK)|Represents the relationship between Trainers and Payments|

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
| **Member – Program** (Joins)     | M:N             | Partial           | Handled via **Joins** relationship between Members and Programs                |
| **Program – Trainer** (Conducts) | M:N             | Partial           | Handled via **Conducts** relationship between Programs and Trainers            |
| **Trainer – Payment** (Duty)     | 1:N             | Partial           | A trainer can have multiple payments for duties                                |
| **Member – Payment**             | 1:N             | Total             | Each member can make multiple payments, but each payment belongs to one member |


### Assumptions
- Each member can join multiple programs.

- Each program can be conducted by one or more trainers.

- Each trainer can receive multiple payments.

- Each member can make multiple payments.

- Every payment record is linked to only one member and one trainer.

---

# Scenario B: City Library Event & Book Lending System

**Business Context:**  
The Central Library wants to manage book lending and cultural events.

**Requirements:**  
- Members borrow books, with loan and return dates tracked.  
- Each book has title, author, and category.  
- Library organizes events; members can register.  
- Each event has one or more speakers/authors.  
- Rooms are booked for events and study.  
- Overdue fines apply for late returns.

### ER Diagram:
<img width="751" height="450" alt="image" src="https://github.com/user-attachments/assets/88613cc9-f48e-40bf-8d6b-128354936ae8" />


### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
| **Member**  | Memb_ID (PK), Memb_Name, Contact_No, Date                                        | Members can borrow books and register for events    |
| **Book**    | Book_ID (PK), Title, Author, Category                                            | Books can be borrowed by members through loans      |
| **Loan**    | Loan_ID (PK), Memb_ID (FK), Book_ID (FK), Loan_Date, Return_Date, Due_Date, Fine | Records details of book loans by members            |
| **Event**   | Event_ID (PK), Event_Name, Event_Date                                            | Events conducted in rooms and registered by members |
| **Room**    | Room_ID (PK), Room_Name, Capacity, Purpose                                       | Rooms host events and are associated with speakers  |
| **Speaker** | Speaker_ID (PK), Name                                                            | Speakers are assigned to rooms for events           |


### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
| **Member – Loan** (Can Have)      | 1:N             | Total             | Each member can have multiple loans                 |
| **Book – Loan** (Have)            | 1:N             | Total             | Each book can be issued in multiple loans over time |
| **Member – Event** (Can Register) | M:N             | Partial           | A member can register for multiple events           |
| **Event – Room** (Occurs)         | 1:N             | Total             | Each event occurs in one room                       |
| **Room – Speaker** (Have)         | 1:N             | Partial           | Each room can have multiple speakers                |

### Assumptions
-Each member can borrow multiple books.

-Each loan is linked to one member and one book.

-Each event occurs in one room.

-Each room can have multiple speakers.

- Fines are applied if books are returned late.
---

# Scenario C: Restaurant Table Reservation & Ordering

**Business Context:**  
A popular restaurant wants to manage reservations, orders, and billing.

**Requirements:**  
- Customers can reserve tables or walk in.  
- Each reservation includes date, time, and number of guests.  
- Customers place food orders linked to reservations.  
- Each order contains multiple dishes; dishes belong to categories (starter, main, dessert).  
- Bills generated per reservation, including food and service charges.  
- Waiters assigned to serve reservations.

### ER Diagram:
<img width="725" height="432" alt="image" src="https://github.com/user-attachments/assets/0e9049ae-8ac6-42ec-bbb4-6606f3caffe9" />


### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
| **Customer**    | CustomerID (PK), Name, Phone_No                                          | Customers make reservations and place orders.                        |
| **Reservation** | ReservationID (PK), Reservation_Date_Time, CustomerID (FK), TableID (FK) | Records reservation details and links customers to tables.           |
| **Table**       | TableID (PK), Table_Number, Capacity, CategoryID (FK)                    | Each table belongs to a category and can have multiple reservations. |
| **Category**    | CategoryID (PK), Category_Name                                           | Describes the category of a table (e.g., VIP, Family, Outdoor).      |
| **Waiter**      | WaiterID (PK), Name, Phone_No                                            | Waiters serve customer orders.                                       |
| **Order**       | OrderID (PK), Order_Time, ReservationID (FK), WaiterID (FK)              | Represents a customer’s order, linked to reservation and waiter.     |
| **Dish**        | DishID (PK), Name, Price, CategoryID (FK)                                | Dishes belong to categories and are listed in the order.             |
| **Bill**        | BillID (PK), OrderID (FK), Total_Amount                                  | Generated for each order.                                            |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
| **Customer – Reservation (books)**    | Customer ↔ Reservation | 1 : N           | Total on Reservation | A customer can make multiple reservations.     |
| **Reservation – Table (assigned to)** | Reservation ↔ Table    | N : 1           | Total on Reservation | Each reservation is assigned to one table.     |
| **Reservation – Order (generates)**   | Reservation ↔ Order    | 1 : N           | Total on Order       | Each reservation can generate multiple orders. |
| **Order – Waiter (serves)**           | Order ↔ Waiter         | N : 1           | Total on Order       | Each order is served by one waiter.            |
| **Order – Bill (produces)**           | Order ↔ Bill           | 1 : 1           | Total on both        | Each order generates exactly one bill.         |
| **Bill – Dish (contains)**            | Bill ↔ Dish            | M : N           | Partial              | Each bill can contain multiple dishes.         |
| **Dish – Category (belongs to)**      | Dish ↔ Category        | N : 1           | Total on Dish        | Each dish belongs to one category.             |
| **Table – Category (classified as)**  | Table ↔ Category       | N : 1           | Total on Table       | Each table belongs to one category.            |


### Assumptions
-Each customer can make multiple reservations, but each reservation is for one table only.

-Every reservation can generate one or more orders.

-Each order is handled by a single waiter and produces one bill.

-Each bill can include multiple dishes.

- Every dish and table belongs to one category.
---

## Instructions for Students

1. Complete **all three scenarios** (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as **a single PDF**
