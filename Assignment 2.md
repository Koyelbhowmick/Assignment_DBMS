# Assignment 2 Questions

1) Create a table EMP1 with following structure.			

ID	Name	Basic	Designation	Age

Details of Attributes:-
ID		Number (2)		
Name		Varchar2 (10)		
Basic		Number (6, 2)		
Designation	Varchar2 (20)					
Age		Number (2)

2) Change the data type of the field Basic from float to integer with required size of the EMP1 table			          					

3) Change the field size of Name column of the EMP1 table from 10 to 15. 

4) Create another table EMP_trainee with the same (changed) structure. The column ID to be renamed as Emp_id in the EMP_trainee table.			


5) Insert following data in EMP1 table:-			           

(1, Rohit, 6700, Manager, 24)
(2, Sunil, 6200, Engineer, 27)
(3, Payal, 6300, Engineer, 25)
(4, Kunal, 6700, Trainee, 28)
(5, Sunita, 6230, Trainee, 26)
(6, Bimal, 7000, Trainee, 25)

6) Insert all rows with the designation ‘trainee’ from the EMP1 table to EMP_trainee table.									
 	
7) Change the designation of all trainees in EMP_trainee table to ‘Programmer _Trainee’.
									

8) Display the structure of both the tables.				
									

9) Add columns Skills (data type-varchar2 and size-10) and DOJ(data type-date) to the EMP1 table and add data for the Skills and DOJ columns according to your own wish.	


10) Display both the tables EMP1 and EMP_trainee.		
									

11) Delete the details of all the trainees from the EMP1 table.													

12) Drop the Age column from the EMP_trainee table.
									

13) Drop two columns in one query from EMP_trainee table.
										

14) Rename the table EMP1 to EMP_Mgr_Engr.
									

15) Drop the table EMP_Trainee.					

16) Truncate EMP_Mgr_Engr table.


# Input Codes:

1. Create table EMP1(ID Number(2), Name Varchar2(10),Basic Number(6,2),Designation Varchar2(10), Age Number(2));

2. ALTER TABLE EMP1 MODIFY Basic NUMBER(10); 

3. ALTER TABLE EMP1 MODIFY Name varchar2(15);

4. create table EMP_trainee as select * from EMP1 where 1=0;
   alter table EMP_trainee rename column ID to Emp_id;

5. insert into emp1 values (1, 'Rohit', 6700, 'Manager', 24);
   insert into emp1 values (2, 'Sunil', 6200, 'Engineer', 27);
   insert into emp1 values (3, 'Payal', 6300, 'Engineer', 25);
   insert into emp1 values (4, 'Kunal', 6700, 'Trainee', 28);
   insert into emp1 values (5, 'Sunita', 6230, 'Trainee', 26);
   insert into emp1 values (6, 'Bimal', 7000, 'Trainee', 25);

6. INSERT INTO EMP_trainee SELECT * FROM emp1 WHERE Designation='Trainee';

7. update emp_trainee set designation='Programmer _Trainee';

8. desc emp1;
   desc emp_trainee

9.alter table emp1 add skills varchar2(10);

10.update emp1 set skills='SQL';
   update emp1 set DOJ='02/08/2022';

11. delete from emp1 where designation='Trainee';

12. alter table emp_trainee drop column age;

13. alter table emp_trainee drop (basic, designation);

14. rename  emp1 to EMP2;

15. drop table emp_trainee;

16. truncate emp2;

# Solutions

### Step 1: Create a table EMP1 with following structure.

```sql
CREATE TABLE EMP1 (
    ID INT,
    Name VARCHAR(10),
    Basic DECIMAL(6, 2),
    Designation VARCHAR(20),
    Age INT
);
```

**Output:**
```
Table EMP1 created.
```

**Statement:**
This SQL command creates a taSure, here are the steps with their corresponding outputs and one or two-sentence descriptions:

### Step 2: Change the data type of the field Basic from float to integer with required size of the EMP1 table

**Standard SQL:**
```sql
ALTER TABLE EMP1 ALTER COLUMN Basic INT;
```

**Output:**
```
Table EMP1 altered.
```

**Statement:**
This SQL command alters the EMP1 table by changing the data type of the Basic column to integer.

### Step 3: Change the field size of the Name column of the EMP1 table from 10 to 15

**Standard SQL:**
```sql
ALTER TABLE EMP1 ALTER COLUMN Name VARCHAR(15);
```

**Output:**
```
Table EMP1 altered.
```

**Statement:**
This SQL command alters the EMP1 table by increasing the size of the Name column from 10 to 15 characters.

### Step 4: Create another table EMP_trainee with the same (changed) structure and rename the column ID to Emp_id

**Standard SQL:**
```sql
CREATE TABLE EMP_trainee LIKE EMP1;
ALTER TABLE EMP_trainee CHANGE COLUMN ID Emp_id INT;
```

**Output:**
```
Table EMP_trainee created.
Table EMP_trainee altered.
```

**Statement:**
This SQL command creates a new table EMP_trainee with the same structure as EMP1 and renames the ID column to Emp_id.

### Step 5: Insert data into EMP1 table

**Standard SQL:**
```sql
INSERT INTO EMP1 (ID, Name, Basic, Designation, Age) VALUES (1, 'Rohit', 6700, 'Manager', 24);
INSERT INTO EMP1 (ID, Name, Basic, Designation, Age) VALUES (2, 'Sunil', 6200, 'Engineer', 27);
INSERT INTO EMP1 (ID, Name, Basic, Designation, Age) VALUES (3, 'Payal', 6300, 'Engineer', 25);
INSERT INTO EMP1 (ID, Name, Basic, Designation, Age) VALUES (4, 'Kunal', 6700, 'Trainee', 28);
INSERT INTO EMP1 (ID, Name, Basic, Designation, Age) VALUES (5, 'Sunita', 6230, 'Trainee', 26);
INSERT INTO EMP1 (ID, Name, Basic, Designation, Age) VALUES (6, 'Bimal', 7000, 'Trainee', 25);
```

**Output:**
```
6 rows inserted into EMP1.
```

**Statement:**
These SQL commands insert six rows of data into the EMP1 table with specified values for each column.

### Step 6: Insert all rows with the designation ‘trainee’ from the EMP1 table to EMP_trainee table

**Standard SQL:**
```sql
INSERT INTO EMP_trainee (Emp_id, Name, Basic, Designation, Age)
SELECT ID, Name, Basic, Designation, Age FROM EMP1 WHERE Designation = 'Trainee';
```

**Output:**
```
3 rows inserted into EMP_trainee.
```

**Statement:**
This SQL command inserts all rows with the designation 'Trainee' from EMP1 into EMP_trainee.

### Step 7: Change the designation of all trainees in EMP_trainee table to ‘Programmer_Trainee’

**Standard SQL:**
```sql
UPDATE EMP_trainee SET Designation = 'Programmer_Trainee';
```

**Output:**
```
3 rows updated in EMP_trainee.
```

**Statement:**
This SQL command updates the designation of all trainees in the EMP_trainee table to 'Programmer_Trainee'.

### Step 8: Display the structure of both the tables

**Standard SQL:**
```sql
DESCRIBE EMP1;
DESCRIBE EMP_trainee;
```

**Output:**
```
Structure of EMP1:
ID          INT
Name        VARCHAR(15)
Basic       INT
Designation VARCHAR(20)
Age         INT

Structure of EMP_trainee:
Emp_id      INT
Name        VARCHAR(15)
Basic       INT
Designation VARCHAR(20)
Age         INT
```

**Statement:**
These SQL commands display the structure of the EMP1 and EMP_trainee tables, showing their columns and data types.

### Step 9: Add columns Skills and DOJ to the EMP1 table and add data

**Standard SQL:**
```sql
ALTER TABLE EMP1 ADD Skills VARCHAR(10);
ALTER TABLE EMP1 ADD DOJ DATE;
UPDATE EMP1 SET Skills = 'SQL';
UPDATE EMP1 SET DOJ = '2022-08-02';
```

**Output:**
```
Table EMP1 altered.
6 rows updated in EMP1.
6 rows updated in EMP1.
```

**Statement:**
These SQL commands add new columns Skills and DOJ to the EMP1 table and populate them with default values.

### Step 10: Display both the tables EMP1 and EMP_trainee

**Standard SQL:**
```sql
SELECT * FROM EMP1;
SELECT * FROM EMP_trainee;
```

**Output:**

**EMP1:**
```
ID  Name    Basic   Designation Age Skills DOJ
1   Rohit   6700    Manager     24  SQL    2022-08-02
2   Sunil   6200    Engineer    27  SQL    2022-08-02
3   Payal   6300    Engineer    25  SQL    2022-08-02
4   Kunal   6700    Trainee     28  SQL    2022-08-02
5   Sunita  6230    Trainee     26  SQL    2022-08-02
6   Bimal   7000    Trainee     25  SQL    2022-08-02
```

**EMP_trainee:**
```
Emp_id  Name    Basic   Designation          Age
4       Kunal   6700    Programmer_Trainee   28
5       Sunita  6230    Programmer_Trainee   26
6       Bimal   7000    Programmer_Trainee   25
```

**Statement:**
These SQL commands display the content of the EMP1 and EMP_trainee tables, showing all the rows and columns.

### Step 11: Delete the details of all the trainees from the EMP1 table

**Standard SQL:**
```sql
DELETE FROM EMP1 WHERE Designation = 'Trainee';
```

**Output:**
```
3 rows deleted from EMP1.
```

**Statement:**
This SQL command deletes all rows from the EMP1 table where the designation is 'Trainee'.

### Step 12: Drop the Age column from the EMP_trainee table

**Standard SQL:**
```sql
ALTER TABLE EMP_trainee DROP COLUMN Age;
```

**Output:**
```
Table EMP_trainee altered.
```

**Statement:**
This SQL command alters the EMP_trainee table by dropping the Age column.

### Step 13: Drop two columns in one query from EMP_trainee table

**Standard SQL:**
```sql
ALTER TABLE EMP_trainee DROP COLUMN Basic, DROP COLUMN Designation;
```

**Output:**
```
Table EMP_trainee altered.
```

**Statement:**
This SQL command alters the EMP_trainee table by dropping both the Basic and Designation columns in a single query.

### Step 14: Rename the table EMP1 to EMP_Mgr_Engr

**Standard SQL:**
```sql
ALTER TABLE EMP1 RENAME TO EMP_Mgr_Engr;
```

**Output:**
```
Table EMP1 renamed to EMP_Mgr_Engr.
```

**Statement:**
This SQL command renames the EMP1 table to EMP_Mgr_Engr.

### Step 15: Drop the table EMP_trainee

**Standard SQL:**
```sql
DROP TABLE EMP_trainee;
```

**Output:**
```
Table EMP_trainee dropped.
```

**Statement:**
This SQL command drops the EMP_trainee table from the database.

### Step 16: Truncate EMP_Mgr_Engr table

**Standard SQL:**
```sql
TRUNCATE TABLE EMP_Mgr_Engr;
```

**Output:**
```
Table EMP_Mgr_Engr truncated.
```

**Statement:**
This SQL command truncates the EMP_Mgr_Engr table, removing all rows but keeping the table structure.ble named EMP1 with columns for ID, Name, Basic, Designation, and Age, specifying appropriate data types for each column.

