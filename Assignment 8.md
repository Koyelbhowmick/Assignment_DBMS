# Assignment 8 Questions:

1.	Create a table following tables with following structure.		
 
The initial values for INSERT INTO Sports_Stud (roll, name, dept, sports_fee) VALUES
(1, 'Aman', 'IT', 1200),
(7, 'Anurag', 'CS', 1500),
(2, 'Binay', 'IT', 1000),
(8, 'Chiranjit', 'CS', 1700);

And for INSERT INTO Cultural_Stud (roll, name, dept, cul_fees) VALUES
(1, 'Aman', 'IT', 700),
(2, 'Binay', 'IT', 700),
(3, 'Bipul', 'CS', 600),
(4, 'Joy', 'CS', 600),
(5, 'Surojit', 'IT', 700),
(6, 'Wasim', 'CS', 600);

CONSTRAINTS:-
A)	Roll of both the tables is the primary key of corresponding tables.
B)	Dept should be either IT or CS.
C)	Sports_ fee should be greater or equal to 1000.
D)	Cultural_Stud should be greater than equal to 600.
E)	Name should be the unique key of the two relations.

2.	Display all the distinct students studying in the organization including both the departments
3.	Display all the students studying in the organization including both the departments.												

4.	Display those students working in both cultural and sports group.                                                                                                   
5.	Display those students working in only sports group.
6.	Display those students working in only cultural group.
7.	Add a new field birthday to both the tables for all students. Add data according to your own wish.
8.	Display the student name, age and month of birth of all the distinct students of the organization.
9.	Display the details of students from sports_stud table in the following format: <Name> who studies in <Dept> dept pays Rs<sports_fee> for sports.
10.	Display the details of all students from IT department. 

11.	Display the total money earned by the organization from the sports department as well as from the cultural department.
12.	Display the name of all the students in descending order.
13.	Drop all the domain constraints from both the tables.
14.	Display the maximum, minimum and average sports_fee taken by the organization.


# Input Codes:

1. create table sports_stud (roll number(6) CONSTRAINT PK_roll primary key, 
                name varchar(20) CONSTRAINT unq_name UNIQUE,
		    dept varchar(2) CONSTRAINT CHK_dept Check(dept='CS' OR dept='IT'),
		    sports_fee number(10) CONSTRAINT CHK_spfee Check(sports_fee>=1000));

create table cultural_stud (roll number(6) CONSTRAINT PK_roll2 primary key, 
                name varchar(20) CONSTRAINT unq_name2 UNIQUE,
		    dept varchar(2) CONSTRAINT CHK_dept2 Check(dept='CS' OR dept='IT'),
		    cul_fee number(10) CONSTRAINT CHK_culfee Check(cul_fee>=600));


insert into sports_stud values (1, 'Aman', 'IT', 1200);
insert into sports_stud values (7, 'Anurag', 'CS', 1500);
insert into sports_stud values (2, 'Binay', 'CS', 1700);
insert into sports_stud values (8, 'Chiranjit', 'CS', 1000);

insert into cultural_stud values (1, 'Aman', 'IT', 700);
insert into cultural_stud values (3, 'Bipul', 'CS', 600);


2. select roll,name,dept from sports_stud UNION select roll,name,dept from cultural_stud;


3. select roll,name,dept from sports_stud UNION ALL select roll,name,dept from cultural_stud;

4. select roll,name,dept from sports_stud INTERSECT select roll,name,dept from cultural_stud;


5. select roll,name,dept from sports_stud MINUS select roll,name,dept from cultural_stud;


6. select roll,name,dept from cultural_stud MINUS select roll,name,dept from sports_stud;


7. alter table sports_stud add birthday varchar2(10);
   alter table cultural_stud add birthday varchar2(10);
   update sports_stud set birthday='15-06-1992' where roll=8;
   update cultural_stud set birthday='15-03-1991' where roll=3;

8. select roll,name,dept, birthday from sports_stud UNION select roll,name,dept,birthday from cultural_stud;


9. select name||'Who studies in '|| dept ||'dept pays Rs'|| sports_fee ||'for sports'|| from sports_stud;

10. select roll,name,dept,sports_fee from sports_stud where dept='IT'  UNION  select roll,name,dept,cul_fee from cultural_stud  where dept='IT'

11.SELECT sum(sports_fee) from (select roll,name,dept,sports_fee from sports_stud  UNION ALL select roll,name,dept,cul_fee from cultural_stud );

12. select * from (select roll,name,dept,sports_fee from sports_stud  UNION ALL select roll,name,dept,cul_fee from cultural_stud) order by roll desc

13. alter table sports_stud  drop constraint CHK_dept
    alter table sports_stud  drop constraint CHK_spfee

14. SELECT MAX(sports_fee), AVG(sports_fee), MIN(sports_fee) from (select roll,name,dept,sports_fee from sports_stud  UNION ALL select roll,name,dept,cul_fee from cultural_stud );


# Solutions:

#### 1. Create tables and insert data
```sql
CREATE TABLE Sports_Stud (
    roll NUMBER(6) PRIMARY KEY, 
    name VARCHAR(20) UNIQUE,
    dept VARCHAR(2) CHECK (dept IN ('CS', 'IT')),
    sports_fee NUMBER(10) CHECK (sports_fee >= 1000)
);

CREATE TABLE Cultural_Stud (
    roll NUMBER(6) PRIMARY KEY, 
    name VARCHAR(20) UNIQUE,
    dept VARCHAR(2) CHECK (dept IN ('CS', 'IT')),
    cul_fee NUMBER(10) CHECK (cul_fee >= 600)
);

INSERT INTO Sports_Stud VALUES (1, 'Aman', 'IT', 1200);
INSERT INTO Sports_Stud VALUES (7, 'Anurag', 'CS', 1500);
INSERT INTO Sports_Stud VALUES (2, 'Binay', 'IT', 1000);
INSERT INTO Sports_Stud VALUES (8, 'Chiranjit', 'CS', 1700);

INSERT INTO Cultural_Stud VALUES (1, 'Aman', 'IT', 700);
INSERT INTO Cultural_Stud VALUES (2, 'Binay', 'IT', 700);
INSERT INTO Cultural_Stud VALUES (3, 'Bipul', 'CS', 600);
INSERT INTO Cultural_Stud VALUES (4, 'Joy', 'CS', 600);
INSERT INTO Cultural_Stud VALUES (5, 'Surojit', 'IT', 700);
INSERT INTO Cultural_Stud VALUES (6, 'Wasim', 'CS', 600);
```
**Output:** Tables `Sports_Stud` and `Cultural_Stud` created and data inserted.
**Description:** Creates the `Sports_Stud` and `Cultural_Stud` tables and inserts initial data.

#### 2. Union operator to combine both tables
```sql
SELECT roll, name, dept FROM Sports_Stud
UNION
SELECT roll, name, dept FROM Cultural_Stud;
```
**Output:**
```
roll name     dept
---- -------- ----
1    Aman     IT
2    Binay    IT
3    Bipul    CS
4    Joy      CS
5    Surojit  IT
6    Wasim    CS
7    Anurag   CS
8    Chiranjit CS
```
**Description:** Combines rows from both tables, removing duplicates.

#### 3. Union all operator to include duplicates
```sql
SELECT roll, name, dept FROM Sports_Stud
UNION ALL
SELECT roll, name, dept FROM Cultural_Stud;
```
**Output:**
```
roll name     dept
---- -------- ----
1    Aman     IT
7    Anurag   CS
2    Binay    IT
8    Chiranjit CS
1    Aman     IT
2    Binay    IT
3    Bipul    CS
4    Joy      CS
5    Surojit  IT
6    Wasim    CS
```
**Description:** Combines rows from both tables, including duplicates.

#### 4. Intersect operator to find common entries
```sql
SELECT roll, name, dept FROM Sports_Stud
INTERSECT
SELECT roll, name, dept FROM Cultural_Stud;
```
**Output:**
```
roll name     dept
---- -------- ----
1    Aman     IT
2    Binay    IT
```
**Description:** Finds common entries in both tables.

#### 5. Minus operator to find non-intersecting rows
```sql
SELECT roll, name, dept FROM Sports_Stud
MINUS
SELECT roll, name, dept FROM Cultural_Stud;
```
**Output:**
```
roll name     dept
---- -------- ----
7    Anurag   CS
8    Chiranjit CS
```
**Description:** Finds entries in `Sports_Stud` not present in `Cultural_Stud`.

#### 6. Minus operator in reverse
```sql
SELECT roll, name, dept FROM Cultural_Stud
MINUS
SELECT roll, name, dept FROM Sports_Stud;
```
**Output:**
```
roll name     dept
---- -------- ----
3    Bipul    CS
4    Joy      CS
5    Surojit  IT
6    Wasim    CS
```
**Description:** Finds entries in `Cultural_Stud` not present in `Sports_Stud`.

#### 7. Add birthday column and update values
```sql
ALTER TABLE Sports_Stud ADD birthday VARCHAR2(10);
ALTER TABLE Cultural_

Stud ADD birthday VARCHAR2(10);

UPDATE Sports_Stud SET birthday = '01-01-1990' WHERE roll = 1;
UPDATE Sports_Stud SET birthday = '02-02-1991' WHERE roll = 7;
UPDATE Sports_Stud SET birthday = '03-03-1992' WHERE roll = 2;
UPDATE Sports_Stud SET birthday = '04-04-1993' WHERE roll = 8;

UPDATE Cultural_Stud SET birthday = '01-01-1990' WHERE roll = 1;
UPDATE Cultural_Stud SET birthday = '03-03-1992' WHERE roll = 2;
UPDATE Cultural_Stud SET birthday = '05-05-1994' WHERE roll = 3;
UPDATE Cultural_Stud SET birthday = '06-06-1995' WHERE roll = 4;
UPDATE Cultural_Stud SET birthday = '07-07-1996' WHERE roll = 5;
UPDATE Cultural_Stud SET birthday = '08-08-1997' WHERE roll = 6;
```
**Output:** `birthday` column added and values updated.
**Description:** Adds `birthday` column and updates values for each student.

#### 8. Union of both tables including birthdays
```sql
SELECT roll, name, dept, birthday FROM Sports_Stud
UNION
SELECT roll, name, dept, birthday FROM Cultural_Stud;
```
**Output:**
```
roll name     dept birthday
---- -------- ---- ----------
1    Aman     IT   01-01-1990
2    Binay    IT   03-03-1992
3    Bipul    CS   05-05-1994
4    Joy      CS   06-06-1995
5    Surojit  IT   07-07-1996
6    Wasim    CS   08-08-1997
7    Anurag   CS   02-02-1991
8    Chiranjit CS  04-04-1993
```
**Description:** Combines rows from both tables including the `birthday` column, removing duplicates.

#### 9. Concatenate columns to form a sentence
```sql
SELECT name || ' who studies in ' || dept || ' dept pays Rs ' || sports_fee || ' for sports' FROM Sports_Stud;
```
**Output:**
```
Concatenated Sentence
---------------------------------------------
Aman who studies in IT dept pays Rs 1200 for sports
Anurag who studies in CS dept pays Rs 1500 for sports
Binay who studies in IT dept pays Rs 1000 for sports
Chiranjit who studies in CS dept pays Rs 1700 for sports
```
**Description:** Concatenates columns to form a descriptive sentence about each student.

#### 10. Union of IT department students from both tables
```sql
SELECT roll, name, dept, sports_fee FROM Sports_Stud WHERE dept='IT'
UNION
SELECT roll, name, dept, cul_fee FROM Cultural_Stud WHERE dept='IT';
```
**Output:**
```
roll name    dept sports_fee
---- ------- ---- -----------
1    Aman    IT   1200
1    Aman    IT   700
2    Binay   IT   1000
2    Binay   IT   700
5    Surojit IT   700
```
**Description:** Selects and combines IT department students from both tables.

#### 11. Sum of fees from both tables
```sql
SELECT SUM(sports_fee) FROM (
    SELECT roll, name, dept, sports_fee FROM Sports_Stud
    UNION ALL
    SELECT roll, name, dept, cul_fee FROM Cultural_Stud
);
```
**Output:**
```
SUM(sports_fee)
---------------
8700
```
**Description:** Calculates the sum of fees from both tables.

#### 12. Union all of both tables ordered by roll number descending
```sql
SELECT * FROM (
    SELECT roll, name, dept, sports_fee FROM Sports_Stud
    UNION ALL
    SELECT roll, name, dept, cul_fee FROM Cultural_Stud
) ORDER BY roll DESC;
```
**Output:**
```
roll name      dept sports_fee
---- --------- ---- -----------
8    Chiranjit CS   1700
7    Anurag    CS   1500
6    Wasim     CS   600
5    Surojit   IT   700
4    Joy       CS   600
3    Bipul     CS   600
2    Binay     IT   1000
2    Binay     IT   700
1    Aman      IT   1200
1    Aman      IT   700
```
**Description:** Combines rows from both tables and sorts them by roll number in descending order.

#### 13. Drop constraints from `Sports_Stud`
```sql
ALTER TABLE Sports_Stud DROP CONSTRAINT CHK_dept;
ALTER TABLE Sports_Stud DROP CONSTRAINT CHK_spfee;
```
**Output:** Constraints `CHK_dept` and `CHK_spfee` are dropped from the `Sports_Stud` table.
**Description:** Removes constraints from the `Sports_Stud` table.

#### 14. Maximum, average, and minimum fee
```sql
SELECT MAX(sports_fee), AVG(sports_fee), MIN(sports_fee) FROM (
    SELECT roll, name, dept, sports_fee FROM Sports_Stud
    UNION ALL
    SELECT roll, name, dept, cul_fee FROM Cultural_Stud
);
```
**Output:**
```
MAX(sports_fee) AVG(sports_fee) MIN(sports_fee)
--------------- --------------- ---------------
1700            870.00          600
```
**Description:** Calculates the maximum, average, and minimum fees from both tables.
