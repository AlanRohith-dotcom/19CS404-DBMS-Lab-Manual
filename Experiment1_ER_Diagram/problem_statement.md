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
<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/d22318eb-1c99-48cc-90ce-fc6108c37657" />




### Entities and Attributes
| Entity                        | Attributes (PK, FK)                                                                                                | Notes                                                        |
| ----------------------------- | ------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------ |
| **Member**                    | **MemberID (PK)**, Name, MembershipType, StartDate, Email, Phone                                                   | Stores registered gym members                                |
| **Program**                   | **ProgramID (PK)**, ProgramName, Description, Duration, Fee                                                        | Stores fitness programs such as Yoga, Zumba, Weight Training |
| **Trainer**                   | **TrainerID (PK)**, Name, Specialization, Phone, Email                                                             | Stores trainers assigned to fitness programs                 |
| **Personal Training Session** | **SessionID (PK)**, MemberID (FK), TrainerID (FK), SessionDate, StartTime, EndTime, Location                       | Stores personal training sessions booked by members          |
| **Payment**                   | **PaymentID (PK)**, MemberID (FK), SessionID (FK, Nullable), Amount, PaymentDate, PaymentType, PaymentMode, Status | Tracks membership and personal-training session payments     |

### Relationships and Constraints

| Relationship                                       | Cardinality | Participation                      | Notes                                                                                                          |
| -------------------------------------------------- | ----------- | ---------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| **Member — Enrolls in — Program**                  | M:N         | Member: Partial, Program: Partial  | A member can join multiple programs, and a program can have multiple members                                   |
| **Trainer — Assigned to — Program**                | M:N         | Trainer: Partial, Program: Partial | A trainer can handle multiple programs, and a program can have multiple trainers                               |
| **Member — Books — Personal Training Session**     | 1:M         | Member: Partial, Session: Total    | A member can book multiple sessions; each session belongs to one member                                        |
| **Trainer — Conducts — Personal Training Session** | 1:M         | Trainer: Partial, Session: Total   | A trainer can conduct many sessions; each session has one trainer                                              |
| **Member — Attends — Personal Training Session**   | M:N         | Partial                            | Attendance is recorded for each session; attributes can include AttendanceStatus, CheckInTime and CheckOutTime |
| **Member — Makes — Payment**                       | 1:M         | Member: Partial, Payment: Total    | A member can make multiple payments                                                                            |
| **Payment — Covers — Personal Training Session**   | 0/1:1       | Payment: Partial                   | A payment may be for a membership or a specific training session                                               |

### Assumptions
- Each member, trainer, program, session, and payment has a unique ID.
- A member can join multiple programs, and a program can have multiple members and trainers.
-	Each personal training session is booked by one member, conducted by one trainer, and can have attendance and payment records.

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
<img width="962" height="498" alt="image" src="https://github.com/user-attachments/assets/f02370bb-527c-4c3a-88f8-8bf38fffb184" />


### Entities and Attributes
| Entity     | Attributes (PK, FK)                                                                    | Notes                                                               |
| ---------- | -------------------------------------------------------------------------------------- | ------------------------------------------------------------------- |
| **BOOKS**  | **Book_code (PK)**, Book_id, ISBN no., Book_name, Author name, Edition, Subject, Price | Stores information about library books                              |
| **MEMBER** | **Member_id (PK)**, Name, Member type, Contact no., Address, Joining date              | Stores information about library members                            |
| **FINE**   | **Fine_amt**, Payment date                                                             | Stores fine/payment information for overdue books                   |
| **ISSUES** | **Book_id (FK)**, **Member_id (FK)**, Issue date, Expiry date, Return date             | Records which member issued which book and the issue/return details |
| **PAYS**   | **Member_id (FK)**, Fine_amt, Payment date                                             | Records the payment of fines by members                             |


### Relationships and Constraints
| Relationship                | Cardinality | Participation                | Notes                                                                                                                                              |
| --------------------------- | ----------- | ---------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Member — Issues — Books** | M:N         | Partial                      | A member can issue multiple books, and a book can be issued to different members over time. Issue date, expiry date, and return date are recorded. |
| **Member — Pays — Fine**    | 1:M         | Member: Partial, Fine: Total | A member can pay multiple fines, while each fine is associated with a member.                                                                      |
| **Books — Issues — Member** | M:N         | Partial                      | A book may be issued many times, but each issue record belongs to a particular member and book.                                                    |


### Assumptions
- Each member and book has a unique ID.
-	A member can issue multiple books, and a book can be issued to different members over time.
-	A fine is charged when a book is returned after its expiry date, and the member is responsible for paying the fine.

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
<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/22f29740-efc1-4811-8453-d1bbf4dd6dcc" />

### Entities and Attributes

| Entity          | Attributes (PK, FK)                                                                          | Notes                                                     |
| --------------- | -------------------------------------------------------------------------------------------- | --------------------------------------------------------- |
| **Customer**    | **CustomerID (PK)**, Name, Phone, Email, Address                                             | Stores customer information                               |
| **Reservation** | **ReservationID (PK)**, ReservationDate, ReservationTime, NumGuests, ReservationType, Status | Stores table reservations and walk-ins                    |
| **Waiter**      | **WaiterID (PK)**, Name, Phone, Email                                                        | Stores waiter information                                 |
| **Order**       | **OrderID (PK)**, OrderTime, SpecialRequest                                                  | Stores food orders linked to reservations                 |
| **Order Item**  | **OrderItemID (PK)**, Quantity, UnitPrice, Subtotal                                          | Stores individual dishes within an order                  |
| **Dish**        | **DishID (PK)**, DishName, Price, CategoryID (FK)                                            | Stores food items available for ordering                  |
| **Category**    | **CategoryID (PK)**, CategoryName                                                            | Stores dish categories such as Starter, Main, and Dessert |
| **Bill**        | **BillID (PK)**, BillDate, FoodTotal, ServiceCharge, TaxAmount, TotalAmount, PaymentStatus   | Stores the bill generated for a reservation               |


### Relationships and Constraints

| Relationship                           | Cardinality | Participation                         | Notes                                                                                        |
| -------------------------------------- | ----------- | ------------------------------------- | -------------------------------------------------------------------------------------------- |
| **Customer — Makes — Reservation**     | 1:M         | Customer: Partial, Reservation: Total | A customer can make multiple reservations, while each reservation belongs to one customer.   |
| **Reservation — Assigned To — Waiter** | M:1         | Reservation: Total, Waiter: Partial   | Each reservation is served by one waiter, while a waiter can serve multiple reservations.    |
| **Reservation — Has — Order**          | 1:M         | Reservation: Partial, Order: Total    | A reservation can have multiple food orders, and each order is linked to one reservation.    |
| **Order — Contains — Order Item**      | 1:M         | Order: Total, Order Item: Total       | Each order contains one or more order items.                                                 |
| **Order Item — Includes — Dish**       | M:1         | Order Item: Total, Dish: Partial      | An order item refers to one dish, while a dish can appear in many order items.               |
| **Dish — Belongs To — Category**       | M:1         | Dish: Total, Category: Partial        | Each dish belongs to one category; a category can contain many dishes.                       |
| **Reservation — Generates — Bill**     | 1:1         | Reservation: Total, Bill: Total       | Each reservation generates one bill containing food, service charges, tax, and total amount. |

### Assumptions
- Each customer, reservation, waiter, order, dish, and bill has a unique ID.
-	A reservation can have multiple orders, and each order can contain multiple dishes.
-	Each reservation is assigned to one waiter and generates one bill including food and service charges.
 

---

## Instructions for Students

1. Complete **all three scenarios** (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as **a single PDF**
