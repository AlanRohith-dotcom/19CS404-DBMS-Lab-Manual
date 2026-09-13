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
How many medical records are there for each patient?

Sample table:MedicalRecords Table
For example:

Result
PatientID   TotalRecords
----------  ------------
4           4
5           1
6           1
7           1
8           1
10          2

```sql
select patientID, count(*) as TotalRecords
from MedicalRecords
group by patientID;
```

**Output:**

<img width="701" height="722" alt="image" src="https://github.com/user-attachments/assets/4db8d38a-38b5-4fa6-9b9b-dc08bd4bc740" />


**Question 2**
---
What is the total number of medications prescribed for each patient?
Sample tablePrescriptions Table
For example:

Result
PatientID   TotalMedications
----------  ----------------
1           1
2           1
3           1
4           1
5           1
6           1
7           1
8           1
9           1
10          1

```sql
select PatientID, count(*) as TotalMedications
from Prescriptions
group by PatientID;
```

**Output:**

<img width="678" height="787" alt="image" src="https://github.com/user-attachments/assets/a483f9b7-856c-4d10-b27d-686217ecb093" />


**Question 3**
---
How many patients have expired insurance coverage for each insurance company?
Sample table:Insurance Table
For example:
Result
InsuranceCompany  TotalExpiredPatients
----------------  --------------------
ABC Insurance     1
DEF Insurance     1
GHI Insurance     1
JKL Insurance     1
MNO Insurance     1
PQR Insurance     1
STU Insurance     1
VWX Insurance     1
XYZ Insurance     1
YZA Insurance     1

```sql
select InsuranceCompany, count(*) as  TotalExpiredPatients
from Insurance
group by InsuranceCompany;
```

**Output:**

<img width="855" height="815" alt="image" src="https://github.com/user-attachments/assets/4329a132-0a7b-4a0a-a51e-fd07b63645f1" />


**Question 4**
---
Write a SQL query to Calculate the average email length (in characters) for people who lives in Mumbai city
Table: customer

name        type
----------  ----------
id          INTEGER
name        TEXT   
city        TEXT
email       TEXT
phone       INTEGER


```sql
select avg(length(email)) as avg_email_length_below_30
from customer
where city = 'Mumbai';
```

**Output:**

<img width="660" height="392" alt="Screenshot 2026-08-28 084512" src="https://github.com/user-attachments/assets/c3830e08-d84e-4646-8ca6-dd78f933b22b" />

**Question 5**
---
Write a SQL query to find the difference between the maximum and minimum price of fruits?

Table: fruits
name        type
----------  ----------
id          INTEGER
name        TEXT
unit        TEXT
inventory   INTEGER
price       REAL
 

```sql
select max(price)-min(price) as price_diff
from fruits;
```

**Output:**

<img width="402" height="381" alt="image" src="https://github.com/user-attachments/assets/68bd12d4-6cea-4f51-a792-04896648c5b3" />


**Question 6**
---
Write a SQL query to Calculate the average income of the employees with names starting with 'A': 

Table: employee
name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER
For example:
Result
avg_income
----------
5000000.0


```sql
select avg(income) as avg_income
from employee
where name like 'A%';
```

**Output:**

<img width="327" height="382" alt="image" src="https://github.com/user-attachments/assets/ac1f3fc7-91fa-4814-942f-9998fe4b6039" />


**Question 7**
---
Write a SQL query to find the youngest employee in the company?

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER

```sql
select name as Employee_Name, age as Age
from employee
order by age asc, name desc
limit 1;
```

**Output:**

<img width="640" height="385" alt="image" src="https://github.com/user-attachments/assets/0f25f63b-5978-4831-b872-39d06023aabf" />


**Question 8**
---
Write the SQL query that accomplishes the grouping of data by age, calculates the total income for each age group, and includes only those age groups where the total income sum is greater than 1,000,000.
Sample table: employee
For example:

Result
age         SUM(income)
----------  -----------
35          10000000
40          1350000


```sql
select age, SUM(income)
from employee
group by age
having SUM(income)>1000000;
```

**Output:**

<img width="612" height="486" alt="image" src="https://github.com/user-attachments/assets/7594a837-d3fa-442a-966d-306618f5141a" />


**Question 9**
---
Write the SQL query that achieves the grouping of data by age, calculates the minimum income for each age group, and includes only those age groups where the minimum income is less than 1,000,000.
Sample table: employee
For example:

Result
age         Income
----------  ----------
32          200000
40          350000
45          450000


```sql
select age, MIN(Income) as Income
from employee
group by age
having MIN(Income)<1000000; 
```

**Output:**

<img width="602" height="505" alt="image" src="https://github.com/user-attachments/assets/c3152dc2-7589-4741-aea2-a43fbc5ad4cd" />


**Question 10**
---
Write the SQL query that accomplishes the grouping of data by joining date (jdate), calculates the minimum work hours for each date, and excludes dates where the minimum work hour is not less than 10.
Sample table: employee1
For example:

Result
jdate       MIN(workhour)
----------  -------------
2002.0      9
2004.0      9
2006.0      9

```sql
select jdate, MIN(workhour) 
from employee1
group by jdate
having MIN(workhour) < 10;
```

**Output:**
<img width="608" height="516" alt="image" src="https://github.com/user-attachments/assets/ccf6103f-eae1-43ee-88f1-29b08be6ec33" />


## MODULE SEB
<img width="1047" height="106" alt="image" src="https://github.com/user-attachments/assets/0c0f786e-70a9-4081-87ad-d1dcee347337" />


## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
