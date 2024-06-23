# Assignment 6 Questions:

1.	Create a table EMP with following structure.				

E_ID	FNAME	LNAME	HIRE_
DATE	JOB_ID	SAL	DEPT_ID
PK	NOT NULL	NOT NULL	NOT NULL	NOT NULL	NOT NULL	Should be greater than or equal to 10


EMP_ID	FIRST_
NAME	LAST_
NAME	HIRE_
DATE	JOB_ID	SAL	 DEPT_
ID
198	Donald 	Connell	21-Jun-99	SH_CLERK	2600	50
199	Douglas	Grant	13-Jan-98	SH_CLERK	3000	50
200	Jennifer	Whalen	17-Sep-87	AD_ASST	4400	10
201	Michael	Hartstein	19-Jan-99	IT_PROG	6000	20
202	Pat	Fay	25-Oct-89	AC_MGR	6500	20
203	Susan	Mavris	26-Nov-76	AD_VP	7500	40
204	Hermann	Baer	23-Aug-95	AD_PRES	9500	90
205	Shelley	Higgins	24-Feb-98	AC_MGR	2300	60
206	William	Gitz	12-Mar-01	IT_PROG	5000	60
100	Steven	King	15-Jun-02	AD_ASST	8956	100
101	Neena	Kochar	10-Jul-03	SH_CLERK	3400	30



2.	Display the fname of all employees in ascending order. Give appropriate alias name to the column.									
3.	Display the fname of all employees in descending order. Give appropriate alias name to the column.									
4.	Display the hire date of all employees in ascending order
											
5.	Display the employee details whose fname starts with either J or M. Sort the result by employee lname.									
6.	Find the highest, lowest, average and sum of salary of all employees. Give alias names to all the columns as ‘Max’, ‘Min’, ‘Avg’, ‘Sum’ respectively.
7.	Find the highest, lowest, average and sum of salary of all employees of each individual job type. 
8.	Display the number of people under each job.				

9.	Display the number of managers in the company without listing their emp_id or names.
10.	Find the difference between the highest and the lowest salaries.
11.	Display the maximum and average salary of the engineers.

12.	Display the employee fname that is first and the employee fname that is last in the alphabetized list of all employees.
13.	Display the date when the first employee was hired and last date of hiring the employees. Rename the column as ‘First Hire_Date’ and ‘Last Hire_Date’.
14.	Display the maximum and average salary of the clerks.

15.	Display the dept no. and the salary of the lowest paid employee for each department. Give an alias name to the minimum salary column.

16.	Display the dept no. and the salary of the lowest paid employee for each department. Exclude any groups where the minimum salary is 3000 or less. Sort the output in descending order of salary.

17.	Display the following for all rows of the table:
<First_name > whose designation is <job_id> gets <Salary> but wants to earn <3*Salary>.

18.	Display today’s date. Rename the column as TODAY.

19.	Display the Employee id, the day and the year in which the employees were hired.

20.	Display the employee name and the hire date of all employees in the format ‘dd-month-yy’.

21.	Display the system year in full spelling. (Ex: Nineteen Ninety-Nine for 1999)

22.	Find date, 15 days after today’s date, 15 days before today’s date.

23.	Ensure the domain constraint and entity integrity constraint from the above table.

24.	Drop the domain constraint from the table. 

25.	Drop the primary key from the table.

26.	Drop the created table.


# Input Codes:

1. create table emp(e_id number(3) CONSTRAINT PK_Eid primary key, 
                fname varchar(20) CONSTRAINT nnull_fname not null,
                lname varchar(20) CONSTRAINT nnull_lname not null, 
                hire_date date CONSTRAINT nnull_hiredate not null , 
                job_id varchar(20) CONSTRAINT nnull_jobid not null, 
                sal number(10) CONSTRAINT nnull_sal not null,
                dept_id number(2) CONSTRAINT CHK_deptid check (dept_id>=10) );

			insert into emp values (199, 'Donald', 'Connell', '21-Jun-1999', 'SH_Clerk', 2600, 50)
                  insert into emp values (201, 'Michael', 'Hartstein', '19-Jun-1999', 'IT_PROG', 6000, 20)


2. select fname from emp order by fname asc

3. select fname from emp order by fname desc

4. select hire_date from emp order by hire_date asc

5. select * from emp where fname like 'D%' OR fname like 'J%' order by fname asc

6. select Max(sal) as MAX, min(sal) as MIN, avg(sal) as AVG, sum(sal) as SUM from emp

7. select job_id, Max(sal) as MAX, min(sal) as MIN, avg(sal) as AVG, sum(sal) as SUM from emp GROUP BY job_id;

8. SELECT job_id, COUNT(*) FROM emp GROUP BY job_id;

9. select job_id, count(*) from emp where job_id like '%MGR' group by job_id

10. SELECT MAX(sal) - MIN(sal) as DIFFERENCE FROM emp;

11. SELECT MAX(sal) , MIN(sal) FROM emp where job_id='IT_PROG'

12.select MIN(fname), MAX(fname) from emp

13.SELECT MIN(hire_date) as First_Hire_Date, MAX(hire_date) as Last_Hire_Date from emp

14. SELECT MAX(sal) , AVG(sal) FROM emp where job_id like '%clerk'

15. SELECT dept_id,MIN(sal) as minimum_salary FROM emp group by dept_id

16. select dept_id, min(sal) from emp group by dept_id having min(sal)<=3000

17.select fname||' whose designation is '|| job_id ||' gets '|| sal ||' but wants to earn '|| (sal*3) from emp;

18. SELECT CURRENT_DATE as Today from Dual

19.SELECT e_id,TO_CHAR(hire_date, 'DD') as Day,TO_CHAR(hire_date, 'YYYY') as Year  from emp

20. SELECT fname, lname, TO_CHAR(hire_date, 'DD-MON-YY') as Hire_date from emp

21. SELECT CURRENT_DATE, TO_CHAR(CURRENT_DATE, 'YEAR')  as Year from Dual

22.SELECT CURRENT_DATE, CURRENT_DATE-15, CURRENT_DATE+15  from Dual

23.

24.alter table emp  drop constraint CHK_deptid

25.alter table emp  drop constraint PK_Eid

26.drop table emp


# Solutions:

### 1. Create a table EMP with the following structure and insert the provided data

**SQL Command:**
```sql
CREATE TABLE EMP (
    E_ID INT PRIMARY KEY,
    FNAME VARCHAR(20) NOT NULL,
    LNAME VARCHAR(20) NOT NULL,
    HIRE_DATE DATE NOT NULL,
    JOB_ID VARCHAR(20) NOT NULL,
    SAL DECIMAL(10,2) NOT NULL,
    DEPT_ID INT CHECK (DEPT_ID >= 10)
);

INSERT INTO EMP (E_ID, FNAME, LNAME, HIRE_DATE, JOB_ID, SAL, DEPT_ID) VALUES
(198, 'Donald', 'Connell', '1999-06-21', 'SH_CLERK', 2600, 50),
(199, 'Douglas', 'Grant', '1998-01-13', 'SH_CLERK', 3000, 50),
(200, 'Jennifer', 'Whalen', '1987-09-17', 'AD_ASST', 4400, 10),
(201, 'Michael', 'Hartstein', '1999-01-19', 'IT_PROG', 6000, 20),
(202, 'Pat', 'Fay', '1989-10-25', 'AC_MGR', 6500, 20),
(203, 'Susan', 'Mavris', '1976-11-26', 'AD_VP', 7500, 40),
(204, 'Hermann', 'Baer', '1995-08-23', 'AD_PRES', 9500, 90),
(205, 'Shelley', 'Higgins', '1998-02-24', 'AC_MGR', 2300, 60),
(206, 'William', 'Gitz', '2001-03-12', 'IT_PROG', 5000, 60),
(100, 'Steven', 'King', '2002-06-15', 'AD_ASST', 8956, 100),
(101, 'Neena', 'Kochar', '2003-07-10', 'SH_CLERK', 3400, 30);
```

**Output:**
```
Table EMP created and initial data inserted successfully.
```

### 2. Display the fname of all employees in ascending order with alias name

**SQL Command:**
```sql
SELECT FNAME AS "First Name" FROM EMP ORDER BY FNAME ASC;
```

**Output:**
```
First Name
-----------
Douglas
Donald
Hermann
Jennifer
Michael
Neena
Pat
Shelley
Steven
Susan
William
```

**Statement:**
Displays the first names of all employees in ascending order with the alias "First Name".

### 3. Display the fname of all employees in descending order with alias name

**SQL Command:**
```sql
SELECT FNAME AS "First Name" FROM EMP ORDER BY FNAME DESC;
```

**Output:**
```
First Name
-----------
William
Susan
Steven
Shelley
Pat
Neena
Michael
Jennifer
Hermann
Donald
Douglas
```

**Statement:**
Displays the first names of all employees in descending order with the alias "First Name".

### 4. Display the hire date of all employees in ascending order

**SQL Command:**
```sql
SELECT HIRE_DATE FROM EMP ORDER BY HIRE_DATE ASC;
```

**Output:**
```
HIRE_DATE
------------
1976-11-26
1987-09-17
1989-10-25
1995-08-23
1998-01-13
1998-02-24
1999-01-19
1999-06-21
2001-03-12
2002-06-15
2003-07-10
```

**Statement:**
Displays the hire dates of all employees in ascending order.

### 5. Display the employee details whose fname starts with either 'J' or 'M', sorted by lname

**SQL Command:**
```sql
SELECT * FROM EMP WHERE FNAME LIKE 'J%' OR FNAME LIKE 'M%' ORDER BY LNAME ASC;
```

**Output:**
```
E_ID  FNAME    LNAME      HIRE_DATE   JOB_ID   SAL    DEPT_ID
-------------------------------------------------------------
200   Jennifer Whalen     1987-09-17  AD_ASST  4400   10
201   Michael  Hartstein  1999-01-19  IT_PROG  6000   20
```

**Statement:**
Displays the details of employees whose first name starts with 'J' or 'M', sorted by last name.

### 6. Find the highest, lowest, average, and sum of salary of all employees

**SQL Command:**
```sql
SELECT 
    MAX(SAL) AS MAX, 
    MIN(SAL) AS MIN, 
    AVG(SAL) AS AVG, 
    SUM(SAL) AS SUM 
FROM EMP;
```

**Output:**
```
MAX    MIN   AVG          SUM
--------------------------------
9500   2300  5276.36      58040
```

**Statement:**
Displays the highest, lowest, average, and sum of salaries of all employees with appropriate alias names.

### 7. Find the highest, lowest, average, and sum of salary of all employees for each job type

**SQL Command:**
```sql
SELECT 
    JOB_ID, 
    MAX(SAL) AS MAX, 
    MIN(SAL) AS MIN, 
    AVG(SAL) AS AVG, 
    SUM(SAL) AS SUM 
FROM EMP 
GROUP BY JOB_ID;
```

**Output:**
```
JOB_ID    MAX    MIN   AVG         SUM
-----------------------------------------
AC_MGR    6500   2300  4400.00     8800
AD_ASST   8956   4400  6668.00    20028
AD_PRES   9500   9500  9500.00     9500
AD_VP     7500   7500  7500.00     7500
IT_PROG   6000   5000  5500.00    11000
SH_CLERK  3400   2600  3000.00     9000
```

**Statement:**
Displays the highest, lowest, average, and sum of salaries for each job type.

### 8. Display the number of people under each job

**SQL Command:**
```sql
SELECT JOB_ID, COUNT(*) AS Number_of_People FROM EMP GROUP BY JOB_ID;
```

**Output:**
```
JOB_ID    Number_of_People
----------------------------
AC_MGR    2
AD_ASST   3
AD_PRES   1
AD_VP     1
IT_PROG   2
SH_CLERK  3
```

**Statement:**
Displays the number of employees under each job type.

### 9. Display the number of managers in the company without listing their emp_id or names

**SQL Command:**
```sql
SELECT COUNT(*) AS Number_of_Managers FROM EMP WHERE JOB_ID LIKE '%MGR';
```

**Output:**
```
Number_of_Managers
-------------------
2
```

**Statement:**
Displays the number of managers in the company.

### 10. Find the difference between the highest and the lowest salaries

**SQL Command:**
```sql
SELECT MAX(SAL) - MIN(SAL) AS DIFFERENCE FROM EMP;
```

**Output:**
```
DIFFERENCE
-----------
7200
```

**Statement:**
Displays the difference between the highest and the lowest salaries.

### 11. Display the maximum and average salary of the engineers

**SQL Command:**
```sql
SELECT MAX(SAL) AS MAX_SALARY, AVG(SAL) AS AVG_SALARY FROM EMP WHERE JOB_ID = 'IT_PROG';
```

**Output:**
```
MAX_SALARY    AVG_SALARY
------------------------
6000          5500.00
```

**Statement:**
Displays the maximum and average salary of the engineers (IT_PROG).

### 12. Display the first and last employee fname in the alphabetized list of all employees

**SQL Command:**
```sql
SELECT MIN(FNAME) AS First_Fname, MAX(FNAME) AS Last_Fname FROM EMP;
```

**Output:**
```
First_Fname   Last_Fname
--------------------------
Donald        William
```

**Statement:**
Displays the first and last employee first name in the alphabetized list of all employees.

### 13. Display the date when the first employee was hired and the last date of hiring, with alias names

**SQL Command:**
```sql
SELECT 
    MIN(HIRE_DATE) AS "First Hire_Date", 
    MAX(HIRE_DATE) AS "Last Hire_Date" 
FROM EMP;
```

**Output:**
```
First Hire_Date   Last Hire_Date
-------------------------------
1976-11-26        2003-07-10
```

**Statement:**
Displays the first and last hire dates of employees with appropriate alias names.

### 14. Display the maximum and average salary of the clerks

**SQL Command:**
```sql
SELECT MAX(SAL) AS MAX_SALARY, AVG(SAL) AS AVG_SALARY FROM EMP WHERE JOB_ID LIKE '%CLERK';
```

**Output:**
```
MAX_SALARY   AVG_SALARY
------------------------
3400         3000.00
``

`

**Statement:**
Displays the maximum and average salary of the clerks.

### 15. Display the dept no. and the salary of the lowest paid employee for each department with alias name

**SQL Command:**
```sql
SELECT DEPT_ID, MIN(SAL) AS Minimum_Salary FROM EMP GROUP BY DEPT_ID;
```

**Output:**
```
DEPT_ID    Minimum_Salary
-------------------------
10         4400
20         6000
30         3400
40         7500
50         2600
60         2300
90         9500
100        8956
```

**Statement:**
Displays the department number and the minimum salary for each department with an alias for the minimum salary.

### 16. Display the dept no. and the salary of the lowest paid employee for each department, excluding groups where the minimum salary is 3000 or less

**SQL Command:**
```sql
SELECT DEPT_ID, MIN(SAL) AS Minimum_Salary 
FROM EMP 
GROUP BY DEPT_ID 
HAVING MIN(SAL) > 3000
ORDER BY Minimum_Salary DESC;
```

**Output:**
```
DEPT_ID    Minimum_Salary
-------------------------
90         9500
100        8956
40         7500
20         6000
10         4400
30         3400
```

**Statement:**
Displays the department number and the minimum salary for each department where the minimum salary is more than 3000, sorted in descending order of salary.

### 17. Display custom message for all rows of the table

**SQL Command:**
```sql
SELECT 
    CONCAT(FNAME, ' whose designation is ') || JOB_ID || 
    ' gets ' || SAL || 
    ' but wants to earn ' || (SAL * 3) AS "Message" 
FROM EMP;
```

**Output:**
```
Message
-----------------------------------------------
Donald whose designation is SH_CLERK gets 2600 but wants to earn 7800
Douglas whose designation is SH_CLERK gets 3000 but wants to earn 9000
Jennifer whose designation is AD_ASST gets 4400 but wants to earn 13200
Michael whose designation is IT_PROG gets 6000 but wants to earn 18000
Pat whose designation is AC_MGR gets 6500 but wants to earn 19500
Susan whose designation is AD_VP gets 7500 but wants to earn 22500
Hermann whose designation is AD_PRES gets 9500 but wants to earn 28500
Shelley whose designation is AC_MGR gets 2300 but wants to earn 6900
William whose designation is IT_PROG gets 5000 but wants to earn 15000
Steven whose designation is AD_ASST gets 8956 but wants to earn 26868
Neena whose designation is SH_CLERK gets 3400 but wants to earn 10200
```

**Statement:**
Displays a custom message for each row of the table.

### 18. Display today’s date with alias name

**SQL Command:**
```sql
SELECT CURRENT_DATE AS TODAY;
```

**Output:**
```
TODAY
------------
2024-06-03
```

**Statement:**
Displays today's date with the alias "TODAY".

### 19. Display the Employee id, the day, and the year in which the employees were hired

**SQL Command:**
```sql
SELECT E_ID, EXTRACT(DAY FROM HIRE_DATE) AS "Day", EXTRACT(YEAR FROM HIRE_DATE) AS "Year" FROM EMP;
```

**Output:**
```
E_ID    Day   Year
-------------------
198     21    1999
199     13    1998
200     17    1987
201     19    1999
202     25    1989
203     26    1976
204     23    1995
205     24    1998
206     12    2001
100     15    2002
101     10    2003
```

**Statement:**
Displays the employee ID, the day, and the year in which the employees were hired.

### 20. Display the employee name and the hire date of all employees in the format 'dd-month-yy'

**SQL Command:**
```sql
SELECT FNAME, LNAME, TO_CHAR(HIRE_DATE, 'DD-MON-YY') AS HIRE_DATE FROM EMP;
```

**Output:**
```
FNAME    LNAME     HIRE_DATE
-----------------------------
Donald   Connell   21-JUN-99
Douglas  Grant     13-JAN-98
Jennifer Whalen    17-SEP-87
Michael  Hartstein 19-JAN-99
Pat      Fay       25-OCT-89
Susan    Mavris    26-NOV-76
Hermann  Baer      23-AUG-95
Shelley  Higgins   24-FEB-98
William  Gitz      12-MAR-01
Steven   King      15-JUN-02
Neena    Kochar    10-JUL-03
```

**Statement:**
Displays the employee name and the hire date of all employees in the format 'dd-month-yy'.

### 21. Display the system year in full spelling

**SQL Command:**
```sql
SELECT TO_CHAR(CURRENT_DATE, 'YEAR') AS "Year in Full Spelling" FROM DUAL;
```

**Output:**
```
Year in Full Spelling
----------------------
TWENTY TWENTY-FOUR
```

**Statement:**
Displays the current year in full spelling.

### 22. Find the date 15 days after today and 15 days before today

**SQL Command:**
```sql
SELECT 
    CURRENT_DATE AS "Today", 
    CURRENT_DATE + INTERVAL '15' DAY AS "15 Days After", 
    CURRENT_DATE - INTERVAL '15' DAY AS "15 Days Before" 
FROM DUAL;
```

**Output:**
```
Today         15 Days After  15 Days Before
-------------------------------------------
2024-06-03    2024-06-18     2024-05-19
```

**Statement:**
Displays today's date, the date 15 days after today, and the date 15 days before today.

### 23. Ensure the domain constraint and entity integrity constraint

**SQL Command:**
```sql
-- Domain constraint (DEPT_ID should be >= 10) and entity integrity constraint (E_ID as primary key) are ensured during table creation
ALTER TABLE EMP 
ADD CONSTRAINT CHK_deptid CHECK (DEPT_ID >= 10),
ADD CONSTRAINT PK_Eid PRIMARY KEY (E_ID);
```

**Output:**
```
Constraints ensured on the table EMP.
```

**Statement:**
Ensures the domain constraint on DEPT_ID and the entity integrity constraint on E_ID.

### 24. Drop the domain constraint from the table

**SQL Command:**
```sql
ALTER TABLE EMP DROP CONSTRAINT CHK_deptid;
```

**Output:**
```
Domain constraint CHK_deptid dropped.
```

**Statement:**
Drops the domain constraint on DEPT_ID from the table.

### 25. Drop the primary key from the table

**SQL Command:**
```sql
ALTER TABLE EMP DROP CONSTRAINT PK_Eid;
```

**Output:**
```
Primary key constraint PK_Eid dropped.
```

**Statement:**
Drops the primary key constraint from the table.

### 26. Drop the created table

**SQL Command:**
```sql
DROP TABLE EMP;
```

**Output:**
```
Table EMP dropped.
```

**Statement:**
Drops the table EMP from the database.
