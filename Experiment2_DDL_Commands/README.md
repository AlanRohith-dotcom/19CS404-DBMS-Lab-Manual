# Experiment 2: DDL Commands

## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**
--
-- <img width="1120" height="515" alt="image" src="https://github.com/user-attachments/assets/94d3a200-b67a-4f63-a283-59c218c2e119" />


```sql
INSERT into Student_details SELECT * From Archived_students;
```

**Output:**
<img width="1221" height="374" alt="image" src="https://github.com/user-attachments/assets/54e4467e-f02f-4a97-8f37-c5607b1ac097" />


**Question 2**
---
-- <img width="1220" height="409" alt="image" src="https://github.com/user-attachments/assets/e26cd517-3e7a-42c3-90a4-8dccb3579025" />


```sql
create table Products(ProductID INTEGER PRIMARY KEY,
                     ProductName TEXT UNIQUE NOT NULL,
                     Price REAL check (price>0),
                     StockQuantity INTEGER CHECK (StockQuantity>=0)
);
```

**Output:**

<img width="1191" height="353" alt="image" src="https://github.com/user-attachments/assets/bb136454-c942-42ea-9247-7cad656055a0" />


**Question 3**
---
-- <img width="1250" height="378" alt="image" src="https://github.com/user-attachments/assets/c145869a-57bb-4ee0-b300-0195adc8c66b" />


```sql
ALTER Table Student_details ADD Date_of_birth Date;
```

**Output:**

<img width="1209" height="442" alt="image" src="https://github.com/user-attachments/assets/71b3b23d-a872-4f23-b9d8-70daecbffe12" />


**Question 4**
---
<img width="1237" height="395" alt="image" src="https://github.com/user-attachments/assets/9d1db3e9-f264-400d-8855-34f3102194c1" />


```sql
INSERT INTO Customers(CustomerID,Name,Address,City,Zipcode)
values
(302,'Laura Croft','456 Elm St','Seattle',98101),
(303,'Bruce Wayne','789 Oak St','Gotham',10001);
       
```

**Output:**

<img width="1199" height="445" alt="image" src="https://github.com/user-attachments/assets/7c720dae-bd1b-435e-a5b1-41491d42d9d0" />


**Question 5**
---
<img width="1381" height="610" alt="image" src="https://github.com/user-attachments/assets/bc17180f-a722-49af-aa85-942884016da3" />


```sql
ALTER TABLE customer ADD birth_date timestamp;
       
```

**Output:**
<img width="833" height="395" alt="image" src="https://github.com/user-attachments/assets/c5259407-49ba-46c0-8d47-81a0055f925c" />


**Question 6**
---
<img width="859" height="549" alt="image" src="https://github.com/user-attachments/assets/dc82fcc0-3b28-49da-be6c-8b84f73a7307" />



```sql
CREATE TABLE Invoices(InvoiceID INTEGER PRIMARY KEY,
                     InvoiceDate DATE,
                     Amount REAL check (Amount>0),
                     DueDate DATE check (DueDate>InvoiceDate),
                     OrderID INTEGER references Orders(OrderID)
);
```

**Output:**

<img width="1229" height="363" alt="image" src="https://github.com/user-attachments/assets/6a631c21-b569-40dc-9d73-68d7fd64da4d" />


**Question 7**
---
<img width="1414" height="431" alt="image" src="https://github.com/user-attachments/assets/a89573a0-f801-48e3-a999-ee3d9bdfddee" />


```sql
CREATE TABLE contacts(contact_id INTEGER PRIMARY KEY,
                     first_name TEXT NOT NULL,
                     last_name TEXT NOT NULL,
                     email TEXT,
                     phone TEXT NOT NULL check (LENGTH(phone)>=10)
);
```

**Output:**

<img width="1219" height="417" alt="image" src="https://github.com/user-attachments/assets/371c7678-e659-405a-aa57-be738846fcaf" />


**Question 8**
---
<img width="1348" height="279" alt="image" src="https://github.com/user-attachments/assets/c01c6a5e-61d8-4f77-b83e-fa51e07aaa5b" />


```sql
INSERT INTO Books(ISBN,Title,Author,Publisher,Year)
values
('978-1234567890','Data Science Essentials','Jane Doe','TechBooks',2024);
```

**Output:**

<img width="1210" height="314" alt="image" src="https://github.com/user-attachments/assets/847fce6c-7181-497b-8b34-03cc5be16ee3" />


**Question 9**
---
<img width="1208" height="366" alt="image" src="https://github.com/user-attachments/assets/5354514b-1073-4a54-b2f5-4782d40f0ebc" />


```sql
CREATE TABLE Departments(DepartmentID INTEGER,
                         DepartmentName TEXT
);
```

**Output:**

<img width="1196" height="421" alt="image" src="https://github.com/user-attachments/assets/008f67ff-fcf6-4289-a59a-fc2111e62279" />


**Question 10**
---
<img width="1410" height="386" alt="image" src="https://github.com/user-attachments/assets/d675a3fa-824f-4c30-876c-4176ee655e15" />


```sql
Create table Orders(OrderID INTEGER PRIMARY KEY,
                   OrderDate DATE NOT NULL,
                   CustomerID INTEGER references Customers(CustomerID)
);
```

**Output:**

<img width="1191" height="346" alt="image" src="https://github.com/user-attachments/assets/51c8bc9e-6e3a-4a84-850d-308961a31614" />

## MODULE COMPLETION
<img width="1169" height="263" alt="image" src="https://github.com/user-attachments/assets/8356bd58-dca3-4b4b-b16e-a46cb0eae787" />


## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
