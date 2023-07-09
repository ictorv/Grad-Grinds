![img](https://images.prismic.io/nightborn/7e215705-8aa6-4ff4-94bf-5a6a801b92a4_thumbnail_website2.jpg?auto=compress,format)

# Day 1

### <center>Q1
Create table emp with attributes emp_id, emp_name, hire_date, job_id, salary and commission.

```sql
CREATE TABLE emp (
  emp_id NUMBER,
  emp_name VARCHAR2(50),
  hire_date DATE,
  job_id NUMBER,
  salary NUMBER,
  commission NUMBER
);
```
### <center>Q2
a) Show the structure of the emp table. Select all data from the emp table.  
```sql
DESC emp;
SELECT * FROM emp;
```

b) Create a query to display the name, job_id, hire date, and employee number for each employee, with employee number appearing first. Provide an alias STARTDATE for the hire date column.
```sql
SELECT emp_name, job_id, hire_date, emp_id FROM emp;
SELECT emp_id, emp_name, job_id, hire_date FROM emp;
SELECT emp_id, emp_name, job_id, hire_date AS STARTDATE FROM emp;
```

c) Create a query to display the unique dept id from the employee table.
```sql
SELECT DISTINCT job_id 
FROM emp;
```

d) Display the name concatenated with dept id, separated by a comma and space and name the column Employee and Title.
```sql
SELECT emp_name || ', ' || job_id AS "Employee and Title" 
FROM emp;
```

e) Write a query to find out the annual salary of each employee.
```sql
SELECT emp_id, emp_name, salary * 12 AS annual_salary
FROM emp;
```
# Day 2

### <center>Q1
a) Display the names of employees who have an ‘a’ and an ‘e’ in their names.
```sql
SELECT emp_name
FROM emp
WHERE emp_name LIKE '%a%' AND emp_name LIKE '%e%';
```
b) Display the name and dept of all employees who do not earn a commission.
```sql
SELECT emp_name, dept
FROM emp
WHERE commission IS NULL;
```
c) Display the last name and salary of employees who earn between Rs. 5000 and Rs.12000, and are in department 10 or 20. Label the columns Employee and Monthly Salary.
```sql
SELECT
    SUBSTR(emp_name, INSTR(emp_name, ' ') + 1) AS Employee,
    salary AS "Monthly Salary"
FROM
    emp
WHERE
    salary BETWEEN 5000 AND 12000
    AND job_id IN (10, 20);
```
### <center>Q2
Write a query that displays all employee’s whose names starts with J,A or M. Sort the results by the employee’s name.

```sql
SELECT
    emp_name
FROM
    emp
WHERE
    emp_name LIKE 'J%'
    OR emp_name LIKE 'A%'
    OR emp_name LIKE 'M%'
ORDER BY
    emp_name;
```
### <center>Q3
a) For each employee display the employee number, salary and salary increased by 15%. Label the column New_salary.
```sql
SELECT emp_id, salary, (salary * 1.15) AS New_salary FROM emp;
```
b) Modify the query to add a column that subtracts the old salary from the new salary. Label the column as Increment.
```sql
SELECT
    emp_id,
    salary,
    (salary * 1.15) AS New_salary,
    (salary * 0.15) AS Increment
FROM
    emp;
```

### <center>Q4
Write a query that produces the following for each employee.
<employee last name> earns <salary> monthly but wants <3 times salary>. Label the column as Dream Salaries.
```sql
SELECT
    SUBSTR(emp_name, INSTR(emp_name, ' ') + 1) || ' earns ' ||
    salary || ' monthly but wants ' || 3 * salary AS "Dream Salaries"
FROM
    emp;
```

### <center>Q5
For each employee, display the employee number, employee name, salary, and salary increased by 15% and expressed as a whole number. Label the column as New_Salary.
```sql
SELECT
    emp_id,
    emp_name,
    salary,
    ROUND(salary * 1.15) AS New_Salary
FROM
    emp;
```

### <center>Q6
Display the name, total monthly salary of each employees i.e. salary along with commission of all those employees whose name starts with ‘A’.
```sql
SELECT
    emp_name,
    salary + commission AS "Total monthly salary"
FROM
    emp
WHERE
    emp_name LIKE 'A%';
```

# Day 3

### <center>Q1
a) Create a table Depart with the columns dept_id, dept_name, location_name where dept_id is primary key.
```sql
CREATE TABLE Depart (
  dept_id INT,
  dept_name VARCHAR(255),
  location_name VARCHAR(255),
  CONSTRAINT pk_dept_id PRIMARY KEY(dept_id),
  CONSTRAINT uq_dept_name UNIQUE (dept_name)
);
```
b) Create another table Employ with the columns empid, name, salary, hire_date, department_no where empid is primary key.

N.B.
- Make a referential integrity between department_no and dept_id. 
- Also make sure that salary must contain some values in all rows and each department’s name is different.
- Give appropriate names to all the constraints being imposed on both the tables.
- Insert at least 3 rows in departments table.
- Insert at least 5 rows in the employees table with different department names.
```sql
CREATE TABLE Employ (
  empid INT,
  name VARCHAR(255),
  salary DECIMAL(10, 2) CONSTRAINT nn_salary NOT NULL,
  hire_date DATE,
  department_no INT,
  CONSTRAINT pk_empid PRIMARY KEY (empid),
  CONSTRAINT fk_dept_no FOREIGN KEY (department_no) REFERENCES Depart(dept_id)
);
```
### <center>Q2
a)   Create a table Person with the columns person_id, first_name, last_name, phone where person_id is primary key.
```sql
CREATE TABLE Person (
    person_id NUMBER,
    first_name VARCHAR(15),
    last_name VARCHAR(15),
    phone NUMBER,
    CONSTRAINT pk_person_id PRIMARY KEY (person_id)
);
```
b)   Create another table Orders with the columns order_id, order_date, p_id where order_id is primary key.
- Make a referential integrity between person_id of Person table and p_id of Orders table.
- Give appropriate names to all the constraints being imposed on the tables. Insert at least three rows in both the tables.
- Add a new constraint such that phone number of Person is always unique.
```sql
CREATE TABLE Orders (
    order_id NUMBER,
    order_date DATE,
    p_id NUMBER,
    CONSTRAINT pk_order_id PRIMARY KEY (order_id),
    CONSTRAINT fk_p_id FOREIGN KEY (p_id) REFERENCES Person (person_id)
);
```
```sql
ALTER TABLE Person ADD CONSTRAINT uc_phone UNIQUE (phone);
```
### <center>Q3
Create a table emp_new with columns name, age, dept_name, loc with the check constraints that names must start with capital S, dept_names should be in upper case only, locations should be in lower case only and age should be more than 18 years.
```sql
CREATE TABLE emp_new (
    name VARCHAR(25) CHECK (REGEXP_LIKE(name, '[A-Z]%')),
    age NUMBER CHECK (age > 18),
    dept_name VARCHAR(25) CHECK (dept_name = UPPER(dept_name)),
    loc VARCHAR(50) CHECK (loc = LOWER(loc))
);
```
### <center>Q4
Create a table Employees with the columns empid, name, salary, address, hire_date, mgr_no,dept_name where empid is primary key. Make a referential integrity between emp_id and mgr_no.
```sql
CREATE TABLE emp_new (
    name VARCHAR(25) CHECK (REGEXP_LIKE(name, '[A-Z]%')),
    age NUMBER CHECK (age > 18),
    dept_name VARCHAR(25) CHECK (dept_name = UPPER(dept_name)),
    loc VARCHAR(50) CHECK (loc = LOWER(loc))
);
```
### <center>Q5
Create table teacher with columns eid,name,salary,dept_name where empid is primary key. Make a referential integrity between eid and mgr_no of Employees table. Name cannot be left empty. The department name must be in uppercase
```sql
CREATE TABLE teacher (
    eid NUMBER,
    name VARCHAR(50) NOT NULL,
    salary NUMBER,
    dept_name VARCHAR(25) CHECK (REGEXP_LIKE(dept_name, '[A-Z]%')),
    CONSTRAINT pk_eid PRIMARY KEY (eid),
    CONSTRAINT fk_eid_teacher FOREIGN KEY (eid) REFERENCES Employees(empid)
);
```
# Day 4

### <center>Q1
a) Create the EMPP table based on the following table instance chart.
| Column   | Data Type | Length |
|----------|-----------|--------|
| Id       | Number    | 5      |
| EName    | Varchar2  | 20     |
| Dept_id  | Varchar2  | 5      |

```sql
CREATE TABLE EMPP (
    Id NUMBER(5),
    EName VARCHAR2(20),
    Dept_id VARCHAR2(5)
);
```
b) Modify the EMPP table to allow for longer employee names (25). Confirm your modification.
```sql
ALTER TABLE EMPP MODIFY Ename VARCHAR2(25);
```
```sql
SELECT column_name, data_type, data_length
FROM user_tab_columns
WHERE table_name = 'EMPP';
```
c) Modify the EMPP table to add a Commission column of number data type, precision 2.
```sql
ALTER TABLE EMPP ADD Commission NUMBER(5,2);
```
d) Rename the EMPP table to EMP_old.
```sql
ALTER TABLE EMPP RENAME TO EMP_old;
```
e) Drop the EMPP table
```sql
DROP TABLE EMP_old;
```
### <center>Q2
a)   Create a table emp_day4 with columns empid, ename, sal from emp_xx.
```sql
CREATE TABLE emp_xx (
    empid NUMBER,
    ename VARCHAR(25),
    sal NUMBER,
    hire_date DATE,
    comm NUMBER
);
```
```sql
CREATE TABLE emp_day4 AS
SELECT empid, ename, sal
FROM emp_xx;
```
b) Increase the salaries of all employees of emp_day4 by Rs. 1000 if salary is less than Rs. 5000.
```sql
UPDATE emp_day4
SET sal = sal + 1000
WHERE sal < 5000;
```
c) Add a new column job_id to emp_day4 and populate it with data.
```sql
ALTER TABLE emp_id ADD job_id NUMBER;
```
```sql
UPDATE emp_day4
SET job_id = 5
WHERE empid = 1;

UPDATE emp_day4
SET job_id = 6
WHERE empid = 2;

UPDATE emp_day4
SET job_id = 7
WHERE empid = 3;

UPDATE emp_day4
SET job_id = 8
WHERE empid = 4;

UPDATE emp_day4
SET job_id = 9
WHERE empid = 5;

UPDATE emp_day4
SET job_id = 10
WHERE empid = 6;

UPDATE emp_day4
SET job_id = 11
WHERE empid = 7;
```
d) Increase the size of ename to 25.
```sql
ALTER TABLE emp_day4 MODIFY ename VARCHAR(25);
```
e) Delete all rows of emp_day4 whose salary is more than Rs. 10000.
```sql
DELETE FROM emp_day4
WHERE sal > 10000;
```
f) Rename the table to emp_d4.
```sql
ALTER TABLE emp_day4 RENAME TO emp_d4;
```
# Day 5

### <center>Q1
Write a query to display the number of people with the same dept.
```sql
select job_id from emp group by job_id;
select job_id, count(*) from emp group by job_id;
select job_id, count(*) as num_people from emp group by job_id;
```
### <center>Q2
a) Determine the number of managers without listing them. Label the column as Number of Managers
```sql
select count(*) as emp_number from emp where is_mgr=1;
```
b) Write a query that displays the difference between the highest and lowest salaries. Label the column Difference.
```sql
select max(salary)-min(salary) as Difference from emp ;
```

### <center>Q3
Display the manager number and the salary of the lowest paid employee for that manager. Exclude anyone whose manager is not known. Sort the output in descending order of salary.
```sql
SELECT mgr_num, MIN(salary) AS minimum_salary
FROM emp
GROUP BY mgr_num;
```
```sql
SELECT mgr_num, MIN(salary) AS minimum_salary
FROM emp
WHERE mgr_num IS NOT NULL
GROUP BY mgr_num;
```
```sql
SELECT mgr_num, MIN(salary) AS minimum_salary
FROM emp
WHERE mgr_num IS NOT NULL
GROUP BY mgr_num
ORDER BY minimum_salary;
```
```sql
SELECT mgr_num, MIN(salary) AS minimum_salary
FROM emp
WHERE mgr_num IS NOT NULL
GROUP BY mgr_num
ORDER BY minimum_salary DESC;
```
### <center>Q4
a) Display the highest, lowest, sum, and average salary of all employees. Label the columns Maximum, Minimum, Sum, and Average, respectively. Round your results to the nearest whole number.
```sql
SELECT
  ROUND(MAX(salary)) AS Max_Salary,
  ROUND(MIN(salary)) AS Min_Salary,
  ROUND(SUM(salary)) AS Sum,
  ROUND(AVG(salary)) AS Average
FROM emp;
```
b) Modify the query to display the minimum, maximum, sum, and average salary for each department.
```sql
SELECT
  job_id,
  ROUND(MAX(salary)) AS Max_Salary,
  ROUND(MIN(salary)) AS Min_Salary,
  ROUND(SUM(salary)) AS Sum,
  ROUND(AVG(salary)) AS Average
FROM emp
GROUP BY job_id;
```
 
### <center>Q5
a) Create a query to display the last name and salary for all employees. Format the salary to be 15 characters long, left padded with $.
```sql
SELECT
  SUBSTR(emp_name, INSTR(emp_name, ' ')+1) AS Name,
  LPAD(salary, 15, '$') AS Salary
FROM emp;
```

b) Display each employees last name and commission amounts. If an employee does not earn a commission put “no commission”.
```sql
SELECT SUBSTR(emp_name, INSTR(emp_name, ' ') + 1) AS Name,
       CASE
           WHEN commission IS NULL THEN 'No Commission'
           ELSE TO_CHAR(commission)
       END AS commission_amount
FROM emp;
```
# Day 6

### <center>Q1
a) Display the employee name and department name for all employees who have an ‘a’ (lowercase) in their names. 
```sql
SELECT emp_name, dept_name
FROM emp
WHERE emp_name LIKE '%a%';
```
b) Write a query to display the employee name, department name, location of employees who earn a commission.
```sql
SELECT emp_name, dept_name, location
FROM emp
WHERE commission IS NOT NULL;
```

### <center>Q2
a) Display the employee name and employee number along with their manager’s name and manager number. Label the columns employee, emp#, manager, and mgr# resp.
```sql
SELECT emp_name AS employee, emp_number AS emp#, mgr_name AS mgr#, mgr_number AS mgr#
FROM emp
WHERE mgr_name IS NOT NULL;
```

b) Modify the above query to display all employees including king who has no manager. Order the results by the employee number.
```sql
SELECT emp_name AS employee, emp_number AS emp#, mgr_name AS mgr#, mgr_number AS mgr#
FROM emp
ORDER BY emp_number;
```
### <center>Q3
a) Create a query that displays employee name, department numbers and all the employees who work in the same department as the given employee. Give each column an appropriate label.
```sql
SELECT
     e2.emp_name AS "Employee",
     e1.dept_number AS "Department Number"
FROM
    emp e1
JOIN
    emp e2 ON e1.dept_number = e2.dept_number
WHERE
    e1.emp_name = 'Alice' ; --Change Alice accordingly
```
b) Create a query to display the name and hire date of any employee hired after employee David.
```sql
SELECT
    e1.emp_name,
    e1.hire_date
FROM
    emp e1
JOIN
    emp e2 ON e1.hire_date > e2.hire_date
WHERE
    e2.emp_name = 'David';
```
### <center>Q4
Display the names and hire date for all employees who were hired before their managers, along with their manager’s names and hire dates. (Hint: Use self join)
```sql
SELECT
    e.emp_name,
    e.hire_date,
    m.emp_name AS "Manager Name",
    m.hire_date
FROM
    emp e
JOIN
    emp m ON e.mgr_number = m.emp_number
WHERE
    e.hire_date < m.hire_date;
```
### <center>Q5
Write a query to display the last name, department number, and department name for all employees.
```sql
SELECT SUBSTR(emp_name, INSTR(emp_name, ' ')+1) AS Name, dept_number, dept_name
FROM emp;
```
### <center>Q6
a) Create a unique listing of all jobs that are in department 80. Include the location of the department in the output.
```sql
SELECT DISTINCT e.dept_name, d.location
FROM emp e
JOIN emp d ON e.dept_number = d.dept_number
WHERE d.dept_number = 80;
```
b) Write a query to display the last name, job, department number, and department name for all employees who work in Toronto.
```sql
SELECT SUBSTR(emp_name, INSTR(emp_name, ' ')+1), dept_number, dept_number
FROM emp
WHERE location = 'Toronto';
```
# Day 7

### <center>Q1
Write a query to display the employee numbers and names of all employees who earn more than average salary. Sort results in ascending order of salary.
```sql
SELECT emp_number, emp_name
FROM emp
WHERE salary > (SELECT AVG(salary) FROM emp)
ORDER BY salary ASC;
```
### <center>Q2
a) Write a query that displays the employee numbers and names of all employees who work in a department with any employee whose name contains a ‘u’.
```sql
SELECT e.emp_number, e.emp_name
FROM emp e
WHERE e.dept_number IN (
    SELECT dept_number
    FROM emp
    WHERE emp_name LIKE '%u%'
);
```
b) Modify the query above to display the employee numbers, names, and salaries of all employees who earn more than the average salary and who work in a department with any employee with a u in their name.
```sql
SELECT e.emp_name, e.emp_number
FROM emp e
WHERE e.dept_name IN (
    SELECT dept_name
    FROM emp
    WHERE emp_name LIKE '%u%'
)
AND e.salary > (
    SELECT AVG(salary)
    FROM emp
);
```
c) Display the name, department number, and department name of all employees whose department location is Bangalore.
```sql
SELECT emp_name, dept_number, dept_name
FROM emp
WHERE location = 'Bangalore';
```
d) Display the name and salary of every employee who reports to Thomas.
```sql

```
e) Display the department number, name and location for every employee in the Executive department.
```sql

```
f) Display the name of the 4th highest paid employee.
```sql
SELECT emp_name, salary
FROM emp
ORDER BY salary DESC
OFFSET 3 ROW
FETCH NEXT 1 ROW ONLY;
```
### <center>Q3
Display the department and its average salary whose average salary is minimum among all the departments.
```sql

```
### <center>Q4
Display employee names and their salary whose salary is greater than at least one employee of department no 50.
```sql

```
### <center>Q5
Display employee names and their salary whose salary is greater than all employees of department no  50
```sql

```
# Day 8
### <center>Q1
Write a pl/sql code block that will accept an account number from the user and debit an amount of Rs. 2000 from the account if the account has a minimum balance of 500 after the amount is debited. The process is fired on accounts table

| ACCOUNT_ID  | NAME   |  BALANCE |
|-------------|----------|--------|
| AC001       | ANUJ      |   5000  |
| AC002       | MITA      |   2400|
```sql

```
### <center>Q2
Write a Pl/SQL code block to calculate the area of a circle for a value of radius varying from 3 to 7. Store the radius and the corresponding values of calculated area in a table AREAS

|RADIUS | AREA|
|-----|-------|
|-------|-------|
|-------|-------|
|-------|-------|
```sql

```

### <center>Q3
Write a PL/SQL code to calculate the factorial of a number entered by the user
```sql

```
### <center>Q4
Write a PL/SQL block of code that first inserts a record in an Emp table. Update the salaries of Blake and Clark by Rs 2000 and Rs 1500. Then check to see that the total salary does not exceed 20000. If the total salary is greater than 20000 then undo the updates made to the salaries of Blake and Clark.
| Emp_No | Emp_Name | Sal  |
|--------|----------|------|
| E001   | Harry    | 5000 |
| E002   | Blake    | 1000 |
| E003   | Jack     | 5000 |
| E004   | Clark    | 1000 |
```sql

```
# Day 9

### <center>Q1
Create a table student with attributes (sid,name) and a table course with attributes (cid,studentid). studentid in course table is the foreign key referring to sid of student table.
Create a trigger such that if anybody wants to delete a row from parent table then the corresponding row in child is first deleted then the row from parent is allowed to be deleted.
```sql

```
### <center>Q2
Create a transparent audit system for a table client_master. The system must keep track of the records that are being deleted or update done on client_master table .The functionality being when a record is deleted or modified the original record details and the date of operation are stored in the audit table, then the delete or update is allowed to go through.
- Table 1: Client_master

Description:
 Used to store information about clients. Against this table auditing must be performed. Attributes are (client_no, name, city, balance)

- Table 2: auditclient

Description: This is the table which keeps track of the records deleted or updated when such operations are carried out. Records in the table will be inserted when the database trigger fires due to an update or delete statement on client_master (client_no, name, balance, operation, user_id, operation_date)
```sql

```