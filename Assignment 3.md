# Assignment-3 Questions

1) Create table EMPLOYEE with the following details.			

     FIELD NAME	     TYPE
EMPLOYEE_ID	NUMBER(6)
LAST_NAME	VARCHAR2(25)
JOB_ID	VARCHAR2(10)
SALARY	NUMBER(8,2)
COMM_PCT	NUMBER (4,2)
MGR_ID	NUMBER (6)
DEPARTMENT_ID	NUMBER (4)


2) Insert the following data into EMPLOYEE table.			          												
EMPLOYEE_ID	LAST_NAME	JOB_ID	SALARY	COMM_PCT	MGR_ID	         DEPARTMENT_ID
198	Connell	SH_CLERK	2600	2.5	124	50
199	Grant	SH_CLERK	2600	2.2	124	50
200	Whalen	AD_ASST	4400	1.3	101	10
201	Hartstein	IT_PROG	6000	null	100	20
202	Fay	AC_MGR	6500	null	210	20
203	Mavris	AD_VP	7500	null	101	40
204	Baer	AD_PRES	3500	1.5	101	90
205	Higgins	AC_MGR	2300	null	101	60
206	Gitz	IT_PROG	5000	null	103	60
100	King	AD_ASST	8956	0.3	108	100
101	Kochar	SH_CLERK	3400	1.3	118	30

3) Display last_name, job_id, employee_id for each employee with employee_id appearing first.									

4) Display the details of all employees of department 60.		


5) Display the employee details of the employee whose last_name is King				           								 

6) Display unique job_id from EMPLOYEE table. Give alias name to the column as JOB_TITLE.								
 	
7) Display last_name, salary and salary increase of Rs300. Give the new column name as ‘Increased Salary’.							

8) Display last_name, salary and annual compensation of all employees, plus a onetime bonus of Rs 100. Give an alias name to the column displaying annual compensation.										
									
9) Display the details of those employees who get commission.	

10) Display the details of those employees who do not get commission.		
									
11) Display the Employee_id, Department_id and Salary all employees whose salary is greater than 5000.							

12) Display the Last_Name and Salary of all employees whose salary is between 4000 and 7000									]

13) Display the details of all employees whose salary is either 6000 or 6500 or 7000.
										

14) 14.	Display the details of all those employees who work either in department 10 or 20 or 30 or 50.
									

15) Display the details of all employees whose salary is not equal to 5000.												

16) Display the details of all the CLERKS working in the organization.												

17) Update the job_id’s of the employees who earn more than 5000 to Grade_A. Display the table EMPLOYEE after updating.																	

18) Display the details of all those employees who are either CLERK or PROGRAMMER or ASSISTANT.								

19) Display those employees from the EMPLOYEE table whose designation is CLERK and salary is less than 3000						

20) Display those employees Last_Name, Mgr_id from the EMPLOYEE table whose salary is above 3000 and work under Manager 101.


# Input Codes:

1. create table employee (employee_id number(6),LAST_NAME VARCHAR2(25), JOB_ID VARCHAR2(10), SALARY NUMBER(8,2), COMM_PCT NUMBER (4,2), MGR_ID NUMBER (6), DEPARTMENT_ID NUMBER (4));

2. Insert into employee values (198,'Connell','SH_CLERK',2600,2.5,124,50);
   Insert into employee values (199,'Grant','SH_CLERK',2600,2.2,124,50);
   Insert into employee values (200,'Whalen','AD_ASST',4400,1.3,101,10);
   Insert into employee values (201,'Hartstein','IT_PROG',6000,null,100,20);
   Insert into employee values (202,'Fay','AC_MGR',6500,null,210,20);
   Insert into employee values (203,'Mavris','AD_VP',7500,null,101,40);
   Insert into employee values (204,'Baer','AD_PRES',3500,1.5,101,90);
   Insert into employee values (205,'Higgins','AC_MGR',2300,null,101,60);
   Insert into employee values (206,'Gitz','IT_PROG',5000,null,103,60);
   Insert into employee values (100,'King','AD_ASST',8956,0.3,108,100);
   Insert into employee values (101,'Kochar','SH_CLERK',3400,1.3,118,30);

3. select EMPLOYEE_ID,LAST_NAME,JOB_ID from employee;

4. select * from employee where DEPARTMENT_ID=60;

5. select * from employee where Last_name='King';

6. select distinct job_id AS JOB_TITLE from employee;

7. select last_name, salary, (salary+300) as Increased_salary from employee;

8. select last_name, salary, ((salary*12)+100) as  annual_compensation from employee;

9. select * from employee where COMM_PCT IS NOT NULL;

10. select * from employee where COMM_PCT IS  NULL;

11. select * from employee where salary>5000;

12. select * from employee where salary BETWEEN 4000 and 7000;

13. select * from employee WHERE (salary =6000) OR (salary = 6500) OR (salary = 7000);
    // select * from employee WHERE Salary in (6000,6500,7000);

14. select * from employee WHERE (DEPARTMENT_ID=10) OR (DEPARTMENT_ID=20) OR (DEPARTMENT_ID=30) OR (DEPARTMENT_ID=50);
    // select * from employee WHERE DEPARTMENT_ID IN (10,20,30,50);

15. select * from employee where salary!=5000;

16. select * from employee where JOB_ID='SH_CLERK';

17. update employee set Job_id='Grade_A' where salary>5000;

18. select * from employee WHERE (JOB_ID='SH_CLERK') OR (JOB_ID='IT_PROG') OR (JOB_ID='AD_ASST');
    // select * from employee WHERE JOB_ID IN ('SH_CLERK','IT_PROG','AD_ASST'); 

19. select * from employee WHERE JOB_ID='SH_CLERK' AND salary<3000;

20. select LAST_NAME,Mgr_id  from employee WHERE MGR_ID='101' AND salary>3000;


# Solutions:

Sure, here are the steps with their corresponding SQL commands, outputs, and one or two-sentence descriptions.

### Step 1: Create table EMPLOYEE

**Standard SQL:**
```sql
CREATE TABLE EMPLOYEE (
    EMPLOYEE_ID INT,
    LAST_NAME VARCHAR(25),
    JOB_ID VARCHAR(10),
    SALARY DECIMAL(8,2),
    COMM_PCT DECIMAL(4,2),
    MGR_ID INT,
    DEPARTMENT_ID INT
);
```

**Output:**
```
Table EMPLOYEE created.
```

**Statement:**
This SQL command creates a table named EMPLOYEE with specified columns and data types.

### Step 2: Insert data into EMPLOYEE table

**Standard SQL:**
```sql
INSERT INTO EMPLOYEE (EMPLOYEE_ID, LAST_NAME, JOB_ID, SALARY, COMM_PCT, MGR_ID, DEPARTMENT_ID) VALUES 
(198, 'Connell', 'SH_CLERK', 2600, 2.5, 124, 50),
(199, 'Grant', 'SH_CLERK', 2600, 2.2, 124, 50),
(200, 'Whalen', 'AD_ASST', 4400, 1.3, 101, 10),
(201, 'Hartstein', 'IT_PROG', 6000, NULL, 100, 20),
(202, 'Fay', 'AC_MGR', 6500, NULL, 210, 20),
(203, 'Mavris', 'AD_VP', 7500, NULL, 101, 40),
(204, 'Baer', 'AD_PRES', 3500, 1.5, 101, 90),
(205, 'Higgins', 'AC_MGR', 2300, NULL, 101, 60),
(206, 'Gitz', 'IT_PROG', 5000, NULL, 103, 60),
(100, 'King', 'AD_ASST', 8956, 0.3, 108, 100),
(101, 'Kochar', 'SH_CLERK', 3400, 1.3, 118, 30);
```

**Output:**
```
11 rows inserted into EMPLOYEE.
```

**Statement:**
These SQL commands insert eleven rows of data into the EMPLOYEE table with specified values for each column.

### Step 3: Display last_name, job_id, employee_id for each employee with employee_id appearing first

**Standard SQL:**
```sql
SELECT EMPLOYEE_ID, LAST_NAME, JOB_ID FROM EMPLOYEE;
```

**Output:**
```
EMPLOYEE_ID LAST_NAME  JOB_ID  
198         Connell    SH_CLERK
199         Grant      SH_CLERK
200         Whalen     AD_ASST
201         Hartstein  IT_PROG
202         Fay        AC_MGR
203         Mavris     AD_VP
204         Baer       AD_PRES
205         Higgins    AC_MGR
206         Gitz       IT_PROG
100         King       AD_ASST
101         Kochar     SH_CLERK
```

**Statement:**
This SQL command selects and displays the employee_id, last_name, and job_id columns for each employee from the EMPLOYEE table.

### Step 4: Display the details of all employees of department 60

**Standard SQL:**
```sql
SELECT * FROM EMPLOYEE WHERE DEPARTMENT_ID = 60;
```

**Output:**
```
EMPLOYEE_ID LAST_NAME JOB_ID   SALARY  COMM_PCT MGR_ID DEPARTMENT_ID
205         Higgins   AC_MGR   2300    NULL     101    60
206         Gitz      IT_PROG  5000    NULL     103    60
```

**Statement:**
This SQL command selects and displays all columns for employees who belong to department 60.

### Step 5: Display the employee details of the employee whose last_name is King

**Standard SQL:**
```sql
SELECT * FROM EMPLOYEE WHERE LAST_NAME = 'King';
```

**Output:**
```
EMPLOYEE_ID LAST_NAME JOB_ID   SALARY  COMM_PCT MGR_ID DEPARTMENT_ID
100         King      AD_ASST  8956    0.3      108    100
```

**Statement:**
This SQL command selects and displays all columns for the employee whose last_name is King.

### Step 6: Display unique job_id from EMPLOYEE table with alias JOB_TITLE

**Standard SQL:**
```sql
SELECT DISTINCT JOB_ID AS JOB_TITLE FROM EMPLOYEE;
```

**Output:**
```
JOB_TITLE  
SH_CLERK
AD_ASST
IT_PROG
AC_MGR
AD_VP
AD_PRES
```

**Statement:**
This SQL command selects and displays unique job_id values from the EMPLOYEE table with an alias of JOB_TITLE.

### Step 7: Display last_name, salary, and salary increase of Rs300 with alias ‘Increased Salary’

**Standard SQL:**
```sql
SELECT LAST_NAME, SALARY, (SALARY + 300) AS Increased_Salary FROM EMPLOYEE;
```

**Output:**
```
LAST_NAME  SALARY  Increased_Salary
Connell    2600    2900
Grant      2600    2900
Whalen     4400    4700
Hartstein  6000    6300
Fay        6500    6800
Mavris     7500    7800
Baer       3500    3800
Higgins    2300    2600
Gitz       5000    5300
King       8956    9256
Kochar     3400    3700
```

**Statement:**
This SQL command selects and displays last_name, salary, and the increased salary (salary + 300) with an alias of Increased_Salary.

### Step 8: Display last_name, salary, and annual compensation of all employees plus a one-time bonus of Rs 100 with alias

**Standard SQL:**
```sql
SELECT LAST_NAME, SALARY, ((SALARY * 12) + 100) AS Annual_Compensation FROM EMPLOYEE;
```

**Output:**
```
LAST_NAME  SALARY  Annual_Compensation
Connell    2600    31300
Grant      2600    31300
Whalen     4400    52900
Hartstein  6000    72100
Fay        6500    78100
Mavris     7500    90100
Baer       3500    42100
Higgins    2300    27700
Gitz       5000    60100
King       8956    107572
Kochar     3400    40900
```

**Statement:**
This SQL command selects and displays last_name, salary, and the annual compensation (salary * 12 + 100) with an alias of Annual_Compensation.

### Step 9: Display the details of those employees who get commission

**Standard SQL:**
```sql
SELECT * FROM EMPLOYEE WHERE COMM_PCT IS NOT NULL;
```

**Output:**
```
EMPLOYEE_ID LAST_NAME JOB_ID   SALARY  COMM_PCT MGR_ID DEPARTMENT_ID
198         Connell    SH_CLERK 2600   2.5      124    50
199         Grant      SH_CLERK 2600   2.2      124    50
200         Whalen     AD_ASST  4400   1.3      101    10
204         Baer       AD_PRES  3500   1.5      101    90
100         King       AD_ASST  8956   0.3      108    100
101         Kochar     SH_CLERK 3400   1.3      118    30
```

**Statement:**
This SQL command selects and displays all columns for employees who receive a commission.

### Step 10: Display the details of those employees who do not get commission

**Standard SQL:**
```sql
SELECT * FROM EMPLOYEE WHERE COMM_PCT IS NULL;
```

**Output:**
```
EMPLOYEE_ID LAST_NAME JOB_ID   SALARY  COMM_PCT MGR_ID DEPARTMENT_ID
201         Hartstein  IT_PROG  6000   NULL     100    20
202         Fay        AC_MGR   6500   NULL     210    20
203         Mavris     AD_VP    7500   NULL     101    40
205         Higgins    AC_MGR   2300   NULL     101    60
206         Gitz       IT_PROG  5000   NULL     103    60
```

**Statement:**
This SQL command selects and displays all columns for employees who do not receive a commission.

### Step 11: Display the Employee_id, Department_id, and Salary of all employees whose salary is greater than 5000

**Standard SQL:**
```sql
SELECT EMPLOYEE_ID, DEPARTMENT_ID, SALARY FROM EMPLOYEE WHERE SALARY > 5000;
```

**Output:**
```
EMPLOYEE_ID DEPARTMENT_ID SALARY
201         20            6000
202         20            6500
203         40            7500
100         100           8956
```



**Statement:**
This SQL command selects and displays employee_id, department_id, and salary for employees whose salary is greater than 5000.

### Step 12: Display the Last_Name and Salary of all employees whose salary is between 4000 and 7000

**Standard SQL:**
```sql
SELECT LAST_NAME, SALARY FROM EMPLOYEE WHERE SALARY BETWEEN 4000 AND 7000;
```

**Output:**
```
LAST_NAME SALARY
Whalen    4400
Hartstein 6000
Fay       6500
Gitz      5000
```

**Statement:**
This SQL command selects and displays last_name and salary for employees whose salary is between 4000 and 7000.

### Step 13: Display the details of all employees whose salary is either 6000, 6500, or 7000

**Standard SQL:**
```sql
SELECT * FROM EMPLOYEE WHERE SALARY IN (6000, 6500, 7000);
```

**Output:**
```
EMPLOYEE_ID LAST_NAME  JOB_ID   SALARY  COMM_PCT MGR_ID DEPARTMENT_ID
201         Hartstein  IT_PROG  6000    NULL     100    20
202         Fay        AC_MGR   6500    NULL     210    20
```

**Statement:**
This SQL command selects and displays all columns for employees whose salary is either 6000, 6500, or 7000.

### Step 14: Display the details of all those employees who work either in department 10, 20, 30, or 50

**Standard SQL:**
```sql
SELECT * FROM EMPLOYEE WHERE DEPARTMENT_ID IN (10, 20, 30, 50);
```

**Output:**
```
EMPLOYEE_ID LAST_NAME  JOB_ID   SALARY  COMM_PCT MGR_ID DEPARTMENT_ID
200         Whalen     AD_ASST  4400    1.3      101    10
201         Hartstein  IT_PROG  6000    NULL     100    20
202         Fay        AC_MGR   6500    NULL     210    20
101         Kochar     SH_CLERK 3400    1.3      118    30
198         Connell    SH_CLERK 2600    2.5      124    50
199         Grant      SH_CLERK 2600    2.2      124    50
```

**Statement:**
This SQL command selects and displays all columns for employees who work in department 10, 20, 30, or 50.

### Step 15: Display the details of all employees whose salary is not equal to 5000

**Standard SQL:**
```sql
SELECT * FROM EMPLOYEE WHERE SALARY != 5000;
```

**Output:**
```
EMPLOYEE_ID LAST_NAME  JOB_ID   SALARY  COMM_PCT MGR_ID DEPARTMENT_ID
198         Connell    SH_CLERK 2600    2.5      124    50
199         Grant      SH_CLERK 2600    2.2      124    50
200         Whalen     AD_ASST  4400    1.3      101    10
201         Hartstein  IT_PROG  6000    NULL     100    20
202         Fay        AC_MGR   6500    NULL     210    20
203         Mavris     AD_VP    7500    NULL     101    40
204         Baer       AD_PRES  3500    1.5      101    90
205         Higgins    AC_MGR   2300    NULL     101    60
100         King       AD_ASST  8956    0.3      108    100
101         Kochar     SH_CLERK 3400    1.3      118    30
```

**Statement:**
This SQL command selects and displays all columns for employees whose salary is not equal to 5000.

### Step 16: Display the details of all the CLERKS working in the organization

**Standard SQL:**
```sql
SELECT * FROM EMPLOYEE WHERE JOB_ID = 'SH_CLERK';
```

**Output:**
```
EMPLOYEE_ID LAST_NAME  JOB_ID   SALARY  COMM_PCT MGR_ID DEPARTMENT_ID
198         Connell    SH_CLERK 2600    2.5      124    50
199         Grant      SH_CLERK 2600    2.2      124    50
101         Kochar     SH_CLERK 3400    1.3      118    30
```

**Statement:**
This SQL command selects and displays all columns for employees with the job_id 'SH_CLERK'.

### Step 17: Update the job_id’s of the employees who earn more than 5000 to Grade_A. Display the table EMPLOYEE after updating

**Standard SQL:**
```sql
UPDATE EMPLOYEE SET JOB_ID = 'Grade_A' WHERE SALARY > 5000;
```

**Output:**
```
4 rows updated in EMPLOYEE.
```

**Standard SQL to Display Updated Table:**
```sql
SELECT * FROM EMPLOYEE;
```

**Output:**
```
EMPLOYEE_ID LAST_NAME  JOB_ID   SALARY  COMM_PCT MGR_ID DEPARTMENT_ID
198         Connell    SH_CLERK 2600    2.5      124    50
199         Grant      SH_CLERK 2600    2.2      124    50
200         Whalen     AD_ASST  4400    1.3      101    10
201         Hartstein  Grade_A  6000    NULL     100    20
202         Fay        Grade_A  6500    NULL     210    20
203         Mavris     Grade_A  7500    NULL     101    40
204         Baer       AD_PRES  3500    1.5      101    90
205         Higgins    AC_MGR   2300    NULL     101    60
206         Gitz       IT_PROG  5000    NULL     103    60
100         King       Grade_A  8956    0.3      108    100
101         Kochar     SH_CLERK 3400    1.3      118    30
```

**Statement:**
This SQL command updates the job_id to 'Grade_A' for employees earning more than 5000 and displays the updated EMPLOYEE table.

### Step 18: Display the details of all those employees who are either CLERK, PROGRAMMER, or ASSISTANT

**Standard SQL:**
```sql
SELECT * FROM EMPLOYEE WHERE JOB_ID IN ('SH_CLERK', 'IT_PROG', 'AD_ASST');
```

**Output:**
```
EMPLOYEE_ID LAST_NAME  JOB_ID   SALARY  COMM_PCT MGR_ID DEPARTMENT_ID
198         Connell    SH_CLERK 2600    2.5      124    50
199         Grant      SH_CLERK 2600    2.2      124    50
200         Whalen     AD_ASST  4400    1.3      101    10
206         Gitz       IT_PROG  5000    NULL     103    60
101         Kochar     SH_CLERK 3400    1.3      118    30
```

**Statement:**
This SQL command selects and displays all columns for employees whose job_id is either 'SH_CLERK', 'IT_PROG', or 'AD_ASST'.

### Step 19: Display those employees whose designation is CLERK and salary is less than 3000

**Standard SQL:**
```sql
SELECT * FROM EMPLOYEE WHERE JOB_ID = 'SH_CLERK' AND SALARY < 3000;
```

**Output:**
```
EMPLOYEE_ID LAST_NAME JOB_ID   SALARY COMM_PCT MGR_ID DEPARTMENT_ID
198         Connell   SH_CLERK 2600   2.5      124    50
199         Grant     SH_CLERK 2600   2.2      124    50
```

**Statement:**
This SQL command selects and displays all columns for employees with the job_id 'SH_CLERK' and a salary less than 3000.

### Step 20: Display those employees Last_Name and Mgr_id whose salary is above 3000 and work under Manager 101

**Standard SQL:**
```sql
SELECT LAST_NAME, MGR_ID FROM EMPLOYEE WHERE SALARY > 3000 AND MGR_ID = 101;
```

**Output:**
```
LAST_NAME  MGR_ID
Whalen     101
Mavris     101
Baer       101
```

**Statement:**
This SQL command selects and displays the last_name and mgr_id for employees whose salary is above 3000 and who work under manager 101.
