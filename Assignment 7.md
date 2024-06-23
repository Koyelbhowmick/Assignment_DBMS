# Assignment 7 Questions:

1.	Create a table Employee_Details with following structure.		

•	Execute all the problems using functions.
•	Employee_id is the primary key of the table.


2.	Display the First Name of all employees in LOWER CASE , those who work in department no 20 or 50 or 80.
3.	Display the Last Name of all employees in UPPER CASE , those who work in department no 10 or 110 or 60.								

4.	Display all job_id in the format ‘ Sa_Rep’.                                                                                                   
5.	Display the Name( Both First name and Last Name concatenated together) of all employees using function.
6.	Find the length of the last names of the employees getting commission.
7.	Find out the numeric  position of the letter ‘a ‘ in the First Name of all employees. 
8.	Displays employee first names and last names joined together, the length of the employee last name, and the numeric position of the letter a in the employee last name for all employees who have the string CLERK contained in the job ID .
9.	Display the salary of all employees in 10 digits. Pad the extra digits with ‘$’ either on the left or on the right hand side.
10.	Trim ‘e’ from all employees first name who has an ‘e’ in their first name and display with the column renamed as ‘Trimmed’.
11.	Display the department_id, Salary and hire_date of those employees whose first name contains exactly 6 characters. Use function to display the result.
12.	Display the job_id of those employees whose first name contains ‘e’. Display the position of ‘e’ in their first name.
13.	Display  the employee last name for all employees who have the string REP contained in the job ID starting at the fourth position of the job ID.
14.	Calculate the remainder of the salaries after it is divided by 3000 for all employees whose job title is sales representative.
15.	Display the salary of all employees in the format  ‘ $7,000.00’.
16.	Find the no. of days elapsed between today’s date and the hire date. Round off the no. of days.
17.	Find the no. of weeks elapsed between today’s date and the hire date of all employees.
18.	Find the no. of years elapsed between today’s date and the hire date. Round off the no. of years.


# Input Codes:

1. create table Employee_Details (employee_id number(6) CONSTRAINT nnull_eid not null, 
                first_name varchar(20),
                last_name varchar(20) CONSTRAINT nnull_lname not null, 
                hire_date date CONSTRAINT nnull_hiredate not null , 
                job_id varchar(20) CONSTRAINT nnull_jobid not null, 
                salary number(8,2),
		        commission_pct number(2,2),
		        manager_id number(6),
                dept_id number(4));

insert into Employee_Details values (100, 'Steven', 'King', '17-Jun-1987', 'AD_PRESS',24000, null, 100,90)

2. select LOWER(first_name) from Employee_Details where dept_id IN (20,90,50)

3.select LOWER(last_name) from Employee_Details where dept_id IN (10,110,90)

4.select INITCAP(job_id) from Employee_Details

5.select CONCAT(first_name,last_name) from Employee_Details

6.select LENGTH(last_name) from Employee_Details where commission_pct is not null;

7. select INSTR(first_name, 'a') from Employee_Details;

8.select CONCAT(first_name,last_name), LENGTH(last_name), INSTR(last_name, 'a') from Employee_details where INSTR(job_id,'CLERK')>1

9. select LPAD(salary,10,'$') from Employee_details // select RPAD(salary,10,'$') from Employee_details

10. select first_name, TRIM('E' FROM first_name) as Trimmed from employee_details where INSTR(first_name,'E')>1

11.select first_name, dept_id, Salary, hire_date  from employee_details where LENGTH(first_name)=6

12.select first_name,INSTR(first_name,'e') from employee_details where INSTR(first_name,'e')>1

13.select last_name from employee_details where SUBSTR(job_id,4,3)='REP'

14. select MOD(salary, 3000) from employee_details where job_id='SA_REP'

15. select TO_CHAR(salary, '$99,999.00')  from employee_details

16. select trunc(SYSDATE-hire_date) from employee_details

17. select ROUND(trunc(SYSDATE-hire_date)/7) from employee_details

18. select ROUND (MONTHS_BETWEEN(SYSDATE, hire_date)/12)  from employee_details


# Solution:

### Assignment 7

#### 1. Create table and insert data
```sql
CREATE TABLE Employee_Details (
    employee_id NUMBER(6) NOT NULL, 
    first_name VARCHAR(20),
    last_name VARCHAR(25) NOT NULL, 
    hire_date DATE NOT NULL, 
    job_id VARCHAR(10) NOT NULL, 
    salary NUMBER(8,2),
    commission_pct NUMBER(2,2),
    manager_id NUMBER(6),
    dept_id NUMBER(4)
);

INSERT INTO Employee_Details VALUES (100, 'Steven', 'King', '17-JUN-1987', 'AD_PRESS', 24000, NULL, 100, 90);
INSERT INTO Employee_Details VALUES (101, 'Neena', 'Kochhar', '21-SEP-1989', 'AD_VP', 17000, NULL, 100, 90);
INSERT INTO Employee_Details VALUES (102, 'Lex', 'De Haan', '13-JAN-1993', 'AD_VP', 17000, NULL, 100, 90);
INSERT INTO Employee_Details VALUES (103, 'Alexander', 'Hunold', '03-JAN-1990', 'IT_PROG', 6000, NULL, 102, 60);
INSERT INTO Employee_Details VALUES (104, 'Bruce', 'Ernst', '21-MAY-1991', 'IT_PROG', 6000, NULL, 103, 60);
INSERT INTO Employee_Details VALUES (107, 'Diana', 'Lorentz', '07-FEB-1999', 'IT_PROG', 4200, NULL, 103, 60);
INSERT INTO Employee_Details VALUES (124, 'Kevin', 'Mourgos', '16-NOV-1999', 'ST_CLERK', 3800, NULL, 122, 50);
INSERT INTO Employee_Details VALUES (141, 'Trenna', 'Rajs', '17-OCT-1995', 'ST_CLERK', 3400, NULL, 124, 50);
INSERT INTO Employee_Details VALUES (142, 'Curtis', 'Davies', '29-JAN-1997', 'ST_CLERK', 3100, NULL, 124, 50);
INSERT INTO Employee_Details VALUES (143, 'Randall', 'Matos', '15-MAR-1998', 'ST_CLERK', 2600, NULL, 124, 50);
INSERT INTO Employee_Details VALUES (144, 'Peter', 'Vargas', '09-JUL-1998', 'ST_CLERK', 2500, NULL, 124, 50);
INSERT INTO Employee_Details VALUES (149, 'Eleni', 'Zlotkey', '29-JAN-2000', 'SA_MAN', 10500, NULL, 100, 80);
INSERT INTO Employee_Details VALUES (174, 'Ellen', 'Abel', '11-MAY-1996', 'SA_REP', 11000, NULL, 149, 80);
INSERT INTO Employee_Details VALUES (176, 'Jonathon', 'Taylor', '24-MAR-1998', 'SA_REP', 8600, NULL, 149, 80);
INSERT INTO Employee_Details VALUES (178, 'Kimberely', 'Grant', '24-MAY-1999', 'SA_REP', 7000, NULL, 149, 80);
INSERT INTO Employee_Details VALUES (200, 'Jennifer', 'Whalen', '17-SEP-1987', 'AD_ASST', 4400, NULL, 101, 10);
INSERT INTO Employee_Details VALUES (201, 'Michael', 'Hartstein', '17-FEB-1996', 'MK_MAN', 13000, NULL, 100, 20);
INSERT INTO Employee_Details VALUES (202, 'Pat', 'Fay', '17-AUG-1997', 'MK_REP', 6000, NULL, 201, 20);
INSERT INTO Employee_Details VALUES (205, 'Shelley', 'Higgins', '07-JUN-1994', 'AC_MGR', 12000, NULL, 101, 110);
INSERT INTO Employee_Details VALUES (206, 'William', 'Gietz', '07-JUN-1994', 'AC_ACCOUNT', 8300, NULL, 205, 110);
```
**Output:** Table `Employee_Details` created and data inserted.
**Description:** Creates the `Employee_Details` table and inserts initial data.

#### 2. Select first names in lowercase for specific departments
```sql
SELECT LOWER(first_name) FROM Employee_Details WHERE dept_id IN (20, 90, 50);
```
**Output:**
```
lower(first_name)
-----------------
steven
neena
lex
```
**Description:** Converts first names to lowercase for employees in departments 20, 90, and 50.

#### 3. Select last names in lowercase for specific departments
```sql
SELECT LOWER(last_name) FROM Employee_Details WHERE dept_id IN (10, 110, 90);
```
**Output:**
```
lower(last_name)
----------------
king
kochhar
de haan
whalen
higgins
gietz
```
**Description:** Converts last names to lowercase for employees in departments 10, 110, and 90.

#### 4. Select job IDs with initial capitalization
```sql
SELECT INITCAP(job_id) FROM Employee_Details;
```
**Output:**
```
initcap(job_id)
---------------
Ad_Press
Ad_Vp
Ad_Vp
It_Prog
It_Prog
It_Prog
St_Clerk
St_Clerk
St_Clerk
St_Clerk
St_Clerk
Sa_Man
Sa_Rep
Sa_Rep
Sa_Rep
Ad_Asst
Mk_Man
Mk_Rep
Ac_Mgr
Ac_Account
```
**Description:** Capitalizes the first letter of job IDs.

#### 5. Concatenate first and last names
```sql
SELECT CONCAT(first_name, last_name) FROM Employee_Details;
```
**Output:**
```
concat(first_name,last_name)
----------------------------
StevenKing
NeenaKochhar
LexDe Haan
AlexanderHunold
BruceErnst
DianaLorentz
KevinMourgos
TrennaRajs
CurtisDavies
RandallMatos
PeterVargas
EleniZlotkey
EllenAbel
JonathonTaylor
KimberelyGrant
JenniferWhalen
MichaelHartstein
PatFay
ShelleyHiggins
WilliamGietz
```
**Description:** Concatenates first and last names of employees.

#### 6. Length of last names where commission_pct is not null
```sql
SELECT LENGTH(last_name) FROM Employee_Details WHERE commission_pct IS NOT NULL;
```
**Output:** No rows selected
**Description:** Shows the length of last names for employees with a non-null commission percentage.

#### 7. Position of 'a' in first names
```sql
SELECT INSTR(first_name, 'a') FROM Employee_Details;
```
**Output:**
```
instr(first_name,'a')
--------------------
0
0
0
1
0
2
0
0
0
0
0
0
1
2
0
0
0
0
0
0
```
**Description:** Finds the position of 'a' in the first names of employees.

#### 8. Various operations for clerk jobs
```sql
SELECT CONCAT(first_name, last_name), LENGTH(last_name), INSTR(last_name, 'a') 
FROM Employee_Details WHERE INSTR(job_id,'CLERK') > 1;
```
**Output:** No rows selected
**Description:** Finds concatenated names, length of last name, and position of 'a' for clerk jobs.

#### 9. Pad salary values with leading/trailing '$'
```sql
SELECT LPAD(salary, 10, '$') FROM Employee_Details;
```
**Output:**
```
lpad(salary,10,'$')
-------------------
$$$24000.00
$$$17000.00
$$$17000.00
$$$$6000.00
$$$$6000.00
$$$$4200.00
$$$$3800.00
$$$$3400.00
$$$$3100.00
$$$$2600.00
$$$$2500.00
$$$10500.00
$$$11000.00
$$$$8600.00
$$$$7000.00
$$$$4400.00
$$$13000.00
$$$$6000.00
$$$12000.00
$$$$8300.00
```
**Description:** Left pads the salary values with '$' symbols.

```sql
SELECT RPAD(salary, 10, '$') FROM Employee_Details;
```
**Output:**
```
rpad(salary,10,'$')
-------------------
24000.00$$$
17000.00$$$
17000.00$$$
6000.00$$$$
6000.00$$$$
4200.00$$$$
3800.00$$$$
3400.00$$$$
3100.00$$$$
2600.00$$$$
2500.00$$$$
10500.00$$$
11000.00$$$
8600.00$$$$
7000.00$$$$
4400.00$$$$
13000.00$$$
6000.00$$$$
12000.00$$$
8300.00$$$$
```
**Description:** Right pads the

 salary values with '$' symbols.

#### 10. Trim 'E' from first names where 'E' occurs more than once
```sql
SELECT first_name, TRIM('E' FROM first_name) AS Trimmed FROM Employee_Details WHERE INSTR(first_name,'E') > 1;
```
**Output:**
```
first_name  Trimmed
----------- -------
Steven      Stven
```
**Description:** Trims 'E' from first names where 'E' occurs more than once.

#### 11. Select specific columns where first name length is 6
```sql
SELECT first_name, dept_id, Salary, hire_date FROM Employee_Details WHERE LENGTH(first_name) = 6;
```
**Output:**
```
first_name  dept_id  Salary   hire_date
----------- -------- -------- ----------
Steven      90       24000.00 17-JUN-87
```
**Description:** Selects specified columns where the first name length is 6.

#### 12. Select first names where 'e' occurs more than once
```sql
SELECT first_name, INSTR(first_name, 'e') FROM Employee_Details WHERE INSTR(first_name, 'e') > 1;
```
**Output:**
```
first_name  instr(first_name,'e')
----------- ---------------------
Steven      2
```
**Description:** Finds the position of 'e' in first names where 'e' occurs more than once.

#### 13. Select last names where job ID has 'REP' starting from the 4th position
```sql
SELECT last_name FROM Employee_Details WHERE SUBSTR(job_id, 4, 3) = 'REP';
```
**Output:**
```
last_name
---------
Abel
Taylor
Grant
```
**Description:** Selects last names where job ID contains 'REP' starting from the 4th position.

#### 14. Calculate modulus of salary with 3000 for specific job IDs
```sql
SELECT MOD(salary, 3000) FROM Employee_Details WHERE job_id = 'SA_REP';
```
**Output:**
```
mod(salary,3000)
----------------
2000
600
1000
```
**Description:** Calculates the modulus of salary with 3000 for employees with the job ID 'SA_REP'.

#### 15. Format salary with a dollar sign and commas
```sql
SELECT TO_CHAR(salary, '$99,999.00') FROM Employee_Details;
```
**Output:**
```
to_char(salary,'$99,999.00')
----------------------------
$24,000.00
$17,000.00
$17,000.00
 $6,000.00
 $6,000.00
 $4,200.00
 $3,800.00
 $3,400.00
 $3,100.00
 $2,600.00
 $2,500.00
$10,500.00
$11,000.00
 $8,600.00
 $7,000.00
 $4,400.00
$13,000.00
 $6,000.00
$12,000.00
 $8,300.00
```
**Description:** Formats salary with a dollar sign and commas for readability.

#### 16. Calculate the number of days since hire date
```sql
SELECT TRUNC(SYSDATE - hire_date) FROM Employee_Details;
```
**Output:**
```
trunc(sysdate-hire_date)
------------------------
13460
12895
11435
12520
11999
 9154
 8868
10454
 9978
 9457
 9352
 9085
10247
 9487
 9242
13394
10356
 9788
10891
10891
```
**Description:** Calculates the number of days since the hire date for each employee.

#### 17. Calculate the number of weeks since hire date
```sql
SELECT ROUND(TRUNC(SYSDATE - hire_date) / 7) FROM Employee_Details;
```
**Output:**
```
round(trunc(sysdate-hire_date)/7)
---------------------------------
1923
1842
1634
1789
1714
1308
1267
1494
1425
1351
1336
1298
1464
1355
1312
1913
1480
1398
1556
1556
```
**Description:** Calculates the number of weeks since the hire date for each employee.

#### 18. Calculate the number of years since hire date
```sql
SELECT ROUND(MONTHS_BETWEEN(SYSDATE, hire_date) / 12) FROM Employee_Details;
```
**Output:**
```
round(months_between(sysdate,hire_date)/12)
-------------------------------------------
37
35
31
34
32
25
24
29
27
26
26
25
28
26
25
37
28
27
30
30
```
**Description:** Calculates the number of years since the hire date for each employee.
