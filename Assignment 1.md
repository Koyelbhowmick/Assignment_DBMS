# Assignment-1 Questions

1) Create a database “MAKAUT_your_roll_no”.				

2)  Create a table “Student” with following structure:		

Roll	Name	Age	Course	Math	Physics	Computer
	DoB


Details of Attributes:-
Roll		Number (5)		
Name		Varchar2 (30)		
Age		Number (5)
Course		Varchar2 (5)			
Math		Number (6, 2)
Physics	Number (6, 2)
Computer	Number (6, 2)
Dob	            Date

3) Display the structure of Student table.			          

4) Rename Course with Department and Name with First Name.    

5) Insert following records into the Student table:-			

•	1, Rahul,19,CSE,79.5,67,89,15-jun-93
•	2,Kunal,21,CS,68,76,59.5,16-aug-91
•	3,Aditi,20,DS,90,73,56,20-sep-92
•	4,Sumit,20,AIML,57.5,78,81,07-dec-91
•	5,Anirban,22,CS,80,68,63,15-sep-94
•	6,Kumkum,21,CS,72,54.5,60,08-feb-95
•	7,Suman,21,ECE,91.5,32,61,10-mar-94
•	8,Rohit,22,CS,85,76,92,19-apr-92

6) Display all the students’ details from Student table.		

7) Find out the details of the students with roll no 5 from Student table.
									
8) Show the roll, name, marks of all subjects for all students from Student table.
									
9) Display all the student details belonging to the CS department.	

10) Update the Math marks of the student with Roll no 7 from 91 to 95 in the ‘Student’ table.
				
11) Update the Name of the student with Roll no 4 from Sumit to Sumitava   the ‘Student’ table.									

12) Delete the details of the student with Roll no 2 from the ‘Student’ table.
									
13) Delete the details of all students from the ‘Student’ table.
									
14) Delete the student table.
									
15) Delete the  table MAKAUT_your_roll_no.



# Input Codes:

1. create table hit_01;

2.create table Student(Roll number(5),Name varchar2(30),Age number(3),Course varchar2(5),Math number(6,2),Physics number(6,2),Computer number(6,2),Birthday date);

3. desc student;

4. alter table studentrename column COURSE to DEPARTMENT;

5. insert into Student values(1,'Rahul',22,'CSE',79.5,67,89,'15-Jun-93');

6. select * from student;

7. select * from Student where Roll=5;

8. select Roll, Name,Math,Physics,Computer from Student;

9. select * from Student where Department='BCA';

10. update Student set Math=95 where Roll=7;

11. update Student set FIRSTNAME='Sumitava' where ROLL=4;

12. delete from Student where Roll=2;

13. delete from Student; // truncate table Student;

14. drop table Student;

15. drop database hit_01;




# Solutions:

### Assignment 1

#### 1. Create a database
```sql
CREATE DATABASE MAKAUT_your_roll_no;
```
**Description:** Creates a new database named `MAKAUT_your_roll_no`.

#### 2. Create a table “Student”
```sql
CREATE TABLE Student (
    Roll NUMBER(5),
    Name VARCHAR(30),
    Age NUMBER(3),
    Course VARCHAR(5),
    Math NUMBER(6, 2),
    Physics NUMBER(6, 2),
    Computer NUMBER(6, 2),
    Dob DATE
);
```
**Description:** Creates a table `Student` with specified columns and data types.

#### 3. Display the structure of the Student table
```sql
DESC Student;
```
**Description:** Displays the structure of the `Student` table.

**Output:**
```
Field      Type
---------- ---------------
Roll       NUMBER(5)
Name       VARCHAR(30)
Age        NUMBER(3)
Course     VARCHAR(5)
Math       NUMBER(6, 2)
Physics    NUMBER(6, 2)
Computer   NUMBER(6, 2)
Dob        DATE
```

#### 4. Rename Course to Department and Name to First Name
```sql
ALTER TABLE Student RENAME COLUMN Course TO Department;
ALTER TABLE Student RENAME COLUMN Name TO FirstName;
```
**Description:** Renames the column `Course` to `Department` and `Name` to `FirstName`.

#### 5. Insert records into the Student table
```sql
INSERT INTO Student VALUES 
(1, 'Rahul', 19, 'CSE', 79.5, 67, 89, '1993-06-15'),
(2, 'Kunal', 21, 'CS', 68, 76, 59.5, '1991-08-16'),
(3, 'Aditi', 20, 'DS', 90, 73, 56, '1992-09-20'),
(4, 'Sumit', 20, 'AIML', 57.5, 78, 81, '1991-12-07'),
(5, 'Anirban', 22, 'CS', 80, 68, 63, '1994-09-15'),
(6, 'Kumkum', 21, 'CS', 72, 54.5, 60, '1995-02-08'),
(7, 'Suman', 21, 'ECE', 91.5, 32, 61, '1994-03-10'),
(8, 'Rohit', 22, 'CS', 85, 76, 92, '1992-04-19');
```
**Description:** Inserts specified records into the `Student` table.

#### 6. Display all the students’ details from the Student table
```sql
SELECT * FROM Student;
```
**Description:** Retrieves all records from the `Student` table.

**Output:**
```
Roll FirstName Age Department Math  Physics Computer Dob
---- ---------- --- ---------- ----- ------- -------- ----------
1    Rahul      19  CSE        79.5  67      89       1993-06-15
2    Kunal      21  CS         68.0  76      59.5     1991-08-16
3    Aditi      20  DS         90.0  73      56       1992-09-20
4    Sumit      20  AIML       57.5  78      81       1991-12-07
5    Anirban    22  CS         80.0  68      63       1994-09-15
6    Kumkum     21  CS         72.0  54.5    60       1995-02-08
7    Suman      21  ECE        91.5  32      61       1994-03-10
8    Rohit      22  CS         85.0  76      92       1992-04-19
```

#### 7. Find details of the student with roll no 5
```sql
SELECT * FROM Student WHERE Roll = 5;
```
**Description:** Retrieves the record of the student with roll number 5.

**Output:**
```
Roll FirstName Age Department Math  Physics Computer Dob
---- ---------- --- ---------- ----- ------- -------- ----------
5    Anirban    22  CS         80.0  68      63       1994-09-15
```

#### 8. Show the roll, name, and marks of all subjects for all students
```sql
SELECT Roll, FirstName, Math, Physics, Computer FROM Student;
```
**Description:** Retrieves roll number, first name, and marks of all subjects for all students.

**Output:**
```
Roll FirstName Math  Physics Computer
---- ---------- ----- ------- --------
1    Rahul      79.5  67      89
2    Kunal      68.0  76      59.5
3    Aditi      90.0  73      56
4    Sumit      57.5  78      81
5    Anirban    80.0  68      63
6    Kumkum     72.0  54.5    60
7    Suman      91.5  32      61
8    Rohit      85.0  76      92
```

#### 9. Display all student details belonging to the CS department
```sql
SELECT * FROM Student WHERE Department = 'CS';
```
**Description:** Retrieves records of students belonging to the CS department.

**Output:**
```
Roll FirstName Age Department Math  Physics Computer Dob
---- ---------- --- ---------- ----- ------- -------- ----------
2    Kunal      21  CS         68.0  76      59.5     1991-08-16
5    Anirban    22  CS         80.0  68      63       1994-09-15
6    Kumkum     21  CS         72.0  54.5    60       1995-02-08
8    Rohit      22  CS         85.0  76      92       1992-04-19
```

#### 10. Update the Math marks of the student with Roll no 7 from 91 to 95
```sql
UPDATE Student SET Math = 95 WHERE Roll = 7;
```
**Description:** Updates the Math marks of the student with roll number 7 to 95.

**Output:**
```
Roll FirstName Age Department Math Physics Computer Dob
---- ---------- --- ---------- ---- ------- -------- ----------
7    Suman      21  ECE        95.0 32      61       1994-03-10
```

#### 11. Update the Name of the student with Roll no 4 from Sumit to Sumitava
```sql
UPDATE Student SET FirstName = 'Sumitava' WHERE Roll = 4;
```
**Description:** Updates the first name of the student with roll number 4 to Sumitava.

**Output:**
```
Roll FirstName Age Department Math Physics Computer Dob
---- ---------- --- ---------- ----- ------- -------- ----------
4    Sumitava   20  AIML       57.5 78      81       1991-12-07
```

#### 12. Delete the details of the student with Roll no 2
```sql
DELETE FROM Student WHERE Roll = 2;
```
**Description:** Deletes the record of the student with roll number 2.

**Output:**
```
Roll FirstName Age Department Math Physics Computer Dob
---- ---------- --- ---------- ----- ------- -------- ----------
1    Rahul      19  CSE        79.5 67      89       1993-06-15
3    Aditi      20  DS         90.0 73      56       1992-09-20
4    Sumitava   20  AIML       57.5 78      81       1991-12-07
5    Anirban    22  CS         80.0 68      63       1994-09-15
6    Kumkum     21  CS         72.0 54.5    60       1995-02-08
7    Suman      21  ECE        95.0 32      61       1994-03-10
8    Rohit      22  CS         85.0 76      92       1992-04-19
```

#### 13. Delete the details of all students
```sql
TRUNCATE TABLE Student;
```
**Description:** Deletes all records from the `Student` table.

**Output:**
```
Roll FirstName Age Department Math Physics Computer Dob
---- ---------- --- ---------- ---- ------- -------- ---
```

#### 14. Delete the student table
```sql
DROP TABLE Student;
```
**Description:** Deletes the `Student` table from the database.

#### 15. Delete the database
```sql
DROP DATABASE MAKAUT_your_roll_no;
```
**Description:** Deletes the database `MAKAUT_your_roll_no`.
