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
Write a SQL statement to increase the salary of employees under the department 40, 90 and 110 according to the company rules.

Salary will be increased by 25% for the department 40, 15% for department 90 and 10% for the department 110 and the rest of the departments will remain same.

Employees table

---------------
employee_id
first_name
last_name
email
phone_number
hire_date
job_id
salary
commission_pct
manager_id
department_id
For example:

Test	Result
SELECT EMPLOYEE_ID, FIRST_NAME, SALARY, PHONE_NUMBER, EMAIL, JOB_ID FROM EMPLOYEES LIMIT 10;
EMPLOYEE_ID  FIRST_NAME  SALARY      PHONE_NUMBER  EMAIL       JOB_ID
-----------  ----------  ----------  ------------  ----------  ----------
100          Steven      27600       515.123.4567  SKING       AD_PRES
101          Neena       19550       515.123.4568  NKOCHHAR    AD_VP
102          Lex         19550       515.123.4569  LDEHAAN     AD_VP
103          Alexander   9000        590.423.4567  AHUNOLD     IT_PROG
104          Bruce       6000        590.423.4568  BERNST      IT_PROG
105          David       4800        590.423.4569  DAUSTIN     IT_PROG
106          Valli       4800        590.423.4560  VPATABAL    IT_PROG
107          Diana       4200        590.423.5567  DLORENTZ    IT_PROG
108          Nancy       12000       515.124.4569  NGREENBE    FI_MGR



```sql
update Employees
set salary = case
    when department_id = 40 then round(salary * 1.25,0)
    when department_id = 90 then round(salary * 1.15,0)
    when department_id = 110 then round(salary * 1.10,0)
    ELSE salary
end;
    
```

**Output:**

<img width="1202" height="538" alt="image" src="https://github.com/user-attachments/assets/2b966893-550a-4571-b814-d607a02c3aae" />


**Question 2**
---
Write a SQL statement to Increase quantity of all products by 10% to adjust for surplus stock counted

Products table

---------------
product_id
product_name
category
cost_price
sell_price
reorder_lvl
quantity
supplier_id

```sql
update Products 
set quantity = quantity * 1.10;
```

**Output:**

<img width="1228" height="696" alt="image" src="https://github.com/user-attachments/assets/f1e3ed96-16e8-406b-8cbb-8f69bfe13c44" />


**Question 3**
---
Write a SQL statement to change the first_name column of employees table with 'John' for those employees whose department_id is 80 and gets a commission_pct below 0.35.

Employees table

---------------
employee_id
first_name
last_name
email
phone_number
hire_date
job_id
salary
commission_pct
manager_id
department_id

```sql
update Employees
set first_name = 'John'
where department_id = 80 and commission_pct < 0.35;
```

**Output:**

<img width="1190" height="608" alt="image" src="https://github.com/user-attachments/assets/ff783f0b-ba81-4937-88f6-43c8619e44fd" />


**Question 4**
---
Write a SQL statement to Update the per_unit_price to 25 and total_price accordingly in purchases table where purchase_date is '2022-08-15' and product_id is 12.



```sql
update purchases
set per_unit_price =25,total_price = 25 * quantity
where purchase_date = '2022-08-15' and product_id =12;
```

**Output:**
<img width="1192" height="600" alt="image" src="https://github.com/user-attachments/assets/63df72c8-0d6b-4abd-bbcf-dd349f6165bb" />


**Question 5**
---
Decrease the reorder level by 30 percent where the product name contains 'cream' and quantity in stock is higher than reorder level in the products table.

PRODUCTS TABLE

name               type
-----------------  ---------------
product_id         INT
product_name       VARCHAR(100)
category           VARCHAR(50)
cost_price         DECIMAL(10,2)
sell_price         DECIMAL(10,2)
reorder_lvl        INT
quantity           INT
supplier_id        INT
 

For example:

Test	Result
select changes();
changes()
----------
3

```sql
update PRODUCTS
set reorder_lvl=reorder_lvl*0.70
where  product_name LIKE '%cream%' and quantity>reorder_lvl;
```

**Output:**

<img width="1192" height="547" alt="image" src="https://github.com/user-attachments/assets/8b5fba28-4b26-4f24-8064-7c6b04ce3584" />


**Question 6**
---
Write a SQL query to Delete customers from 'customer' table where 'OPENING_AMT' is between 4000 and 6000.

Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |

```sql
delete from Customer
where OPENING_AMT>=4000 and OPENING_AMT<=6000;

```

**Output:**

<img width="1197" height="593" alt="image" src="https://github.com/user-attachments/assets/c24c4ebc-78ae-4411-b34f-9a67997d1d46" />


**Question 7**
---
Write a SQL query to delete a doctor from Doctors table whose Specialization is 'Pediatrics' and First name is 'Michael'.

Sample table: Doctors

attributes : doctor_id, first_name, last_name, specialization

```sql
delete from Doctors
where specialization= 'Pediatrics' and first_name = 'Michael';
```

**Output:**

<img width="1181" height="452" alt="image" src="https://github.com/user-attachments/assets/2370f740-1db3-452b-a13d-d171e2950020" />


**Question 8**
---
Write a SQL query to Delete customers whose 'GRADE' is greater than 2 and have a 'PAYMENT_AMT' less than the average 'PAYMENT_AMT' for all customers, or whose 'OUTSTANDING_AMT' is greater than 8000:

Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       

```sql
delete from Customer
where (GRADE >2 and PAYMENT_AMT< (select avg(OUTSTANDING_AMT) from Customer)) or OUTSTANDING_AMT>8000;
```

**Output:**

<img width="1200" height="727" alt="image" src="https://github.com/user-attachments/assets/03d6621f-1f4e-4451-a520-0d03e93d470c" />


**Question 9**
---
Write a SQL query to Delete a Specific Surgery which was made on 28th Feb 2024.

Sample table: Surgeries

attributes: surgery_id, patient_id, surgeon_id, surgery_date

```sql
delete from Surgeries
where surgery_date = '2024-02-28';

```

**Output:**

<img width="1183" height="456" alt="image" src="https://github.com/user-attachments/assets/b47bd733-07e3-4f21-bb7b-a1de3670d6d7" />


**Question 10**
---
Write a SQL query to Delete all Doctors whose Specialization is either 'Pediatrics' or 'Cardiology' and Last Name is Brown.

Sample table: Doctors

attributes : doctor_id, first_name, last_name, specialization

```sql
delete from Doctors
where (specialization ='Pediatrics' or specialization = 'Cardiology')  and last_name ='Brown';
```

**Output:**

<img width="1197" height="845" alt="image" src="https://github.com/user-attachments/assets/0f87cd48-c9cc-44b4-932a-13f5dabd45da" />

## MODULE SEB
<img width="1018" height="75" alt="image" src="https://github.com/user-attachments/assets/8f84c39c-98b9-47ad-92ca-d8c1b478fa7c" />



## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
