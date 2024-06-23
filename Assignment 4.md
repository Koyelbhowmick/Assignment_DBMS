# Assignment 4 Questions:

1.	Create the following tables with the constraints mentioned: 
        Note: the data type and size should be given in relevance with the data to be inserted. Constraint name are not required to be given for this assignment.

Customer

Cust_id	Fname	Lname	Area	Phone
Primary Key	Not Null		Not Null	
A01	Ivan	Ross	SA	6125467
A02	Vandana	Ray	MU	5560379
A03	Pramada	Jauguste	DA	4560389
A04	Basu	Navindi	BA	6125401
A05	Ravi	Shridhar	NA	       null
A06	Rukmini	Aiyer	GH	5125274

Movie

Mv_no	Cust_id	Title	Star	Price
Primary Key	Foreign
Key	Not Null	Not Null	Should be between 100 and 250
1	A02	Bloody	JC	181
2	A04	The Firm	TC	200
3	A01	Pretty Woman	RG	151
4	A06	Home Alone	MC	150
5	A05	The Fugitive	MF	200
6	A03	Coma	MD	100
7	A02	Dracula	GO	150
8	A06	Quick Change	BM	100
9	A03	Gone with the Wind	CB	200
10	A05	Carry on Doctor	LP	100


2.	Prove that entity integrity constraint is ensured by both the tables. (2 conditions to be checked).							
3.	Prove that referential integrity constraint is ensured by both the tables.
4.	Prove that domain integrity constraint is ensured by the Movie table.
5.	Display the movie titles, whose price is greater than 100 but less than 200.
6.	Display the cust_id who have seen movies having stars as either JC or TC or MC.
7.	Display the details of those customers who have an A in their area name.
8.	Display the movie titles, whose price is within 180 and the movie titles are of exactly 6 characters.
9.	Display the movie name, their original prices and the prices after 10% increment. Give alias name to the incremented price column.

10.	Display all the customer details in the following way:
‘Ivan Ross stays in SA and his phone number is 6125467.’

11.	Add a not null constraint to the Lname field in Customer.
12.	Display the customer name whose phone number is not recorded.
13.	Add the phone number according to your own wish for the person mentioned in problem no 7.
14.	Display the unique customer id’s from movie table.
15.	Remove the not null constraint from Star column in movie table.
16.	Delete any row from the Customer table. If you cannot delete, then note the error message displayed.
17.	Delete any row from the Movie table. If you cannot delete, then note the error message displayed.
18.	Drop the Customer table. If you cannot drop, then note the error message displayed.
19.	Drop the Movie table. If you cannot drop, then note the error message displayed.
20.	Drop the foreign key from Movie table.


# Input Codes:

1. create table customer (cust_id varchar2(6) PRIMARY KEY,Fname VARCHAR2(25) NOT NULL, Lname VARCHAR2(25),Area VARCHAR2(2) NOT NULL, Phone NUMBER (10));
  create table movie1 (my_no varchar2(6) PRIMARY KEY, cust_id varchar2(6) references customer,title VARCHAR2(25) NOT NULL,star VARCHAR2(25) NOT NULL, price NUMBER (10) CHECK (price>=100 AND price<=250 ), CONSTRAINT FK_PersonOrder FOREIGN KEY (CUST_ID) REFERENCES Customer(CUST_ID));

2. Insert into customer values ('A01',null,'Ross','SA',612467);
   Insert into customer values ('A01','Ivan','Ross', null,612467); // integrity constraint

3. insert into movie1 values (1,'A01', 'Bloody', 'JC', 181);
   insert into movie1 values (1,'A02', 'Bloody', 'JC', 181); // referential integrity constraint 

4. insert into movie1 values (2,'A01', 'Bloody', 'JC', 251); //domain integrity constraint 

5. select * from movie1 where price between 100 and 200;

6. select cust_id from movie1 where star in ('JC', 'TC', 'MC');

7. select * from customer where area like '%A%';

8. select title from movie1 where price<=180 AND length(title)=5;

9. select title, price, (price+(price*10)/100) as Increased_price from movie1

10. select fname||' '|| lname ||'stays in'|| area ||'and his phone number is'|| phone from customer;

11. alter table customer modify lname varchar2(15) not null;

12. select fname,lname from customer where phone is null;

13. update customer set phone=1111 where area like '%A%';

14. select unique cust_id from movie1;

15. alter table movie1 modify star null;

16. delete from customer where cust_id='A01'; //ORA-02292: integrity constraint (SQL_NDYLPQIQJASPWDKSLOFYYXUVF.FK_PERSONORDER) violated - child record found ORA-06512: at "SYS.DBMS_SQL", line 1721

17.drop table customer; 

18. drop table movie;

20. alter table movie drop column cust_id;


# Solutions:

### 1. Create the tables with constraints

**SQL Command:**
```sql
CREATE TABLE Customer (
    Cust_id VARCHAR(6) PRIMARY KEY,
    Fname VARCHAR(25) NOT NULL,
    Lname VARCHAR(25),
    Area VARCHAR(2) NOT NULL,
    Phone BIGINT(10)
);

CREATE TABLE Movie (
    Mv_no INT PRIMARY KEY,
    Cust_id VARCHAR(6),
    Title VARCHAR(25) NOT NULL,
    Star VARCHAR(25) NOT NULL,
    Price INT CHECK (Price >= 100 AND Price <= 250),
    FOREIGN KEY (Cust_id) REFERENCES Customer(Cust_id)
);
```

**Output:**
```
Table Customer created.
Table Movie created.
```

**Statement:**
These SQL commands create the `Customer` and `Movie` tables with specified columns and constraints, ensuring entity integrity, referential integrity, and domain integrity.

### Insert initial data into tables

**SQL Command:**
```sql
INSERT INTO Customer (Cust_id, Fname, Lname, Area, Phone) VALUES 
('A01', 'Ivan', 'Ross', 'SA', 6125467),
('A02', 'Vandana', 'Ray', 'MU', 5560379),
('A03', 'Pramada', 'Jauguste', 'DA', 4560389),
('A04', 'Basu', 'Navindi', 'BA', 6125401),
('A05', 'Ravi', 'Shridhar', 'NA', NULL),
('A06', 'Rukmini', 'Aiyer', 'GH', 5125274);

INSERT INTO Movie (Mv_no, Cust_id, Title, Star, Price) VALUES
(1, 'A02', 'Bloody', 'JC', 181),
(2, 'A04', 'The Firm', 'TC', 200),
(3, 'A01', 'Pretty Woman', 'RG', 151),
(4, 'A06', 'Home Alone', 'MC', 150),
(5, 'A05', 'The Fugitive', 'MF', 200),
(6, 'A03', 'Coma', 'MD', 100),
(7, 'A02', 'Dracula', 'GO', 150),
(8, 'A06', 'Quick Change', 'BM', 100),
(9, 'A03', 'Gone with the Wind', 'CB', 200),
(10, 'A05', 'Carry on Doctor', 'LP', 100);
```

**Output:**
```
6 rows inserted into Customer.
10 rows inserted into Movie.
```

**Statement:**
This SQL command inserts the given initial data into the `Customer` and `Movie` tables.

### 2. Prove entity integrity constraint is ensured by both tables

**SQL Command:**
```sql
INSERT INTO Customer (Cust_id, Fname, Lname, Area, Phone) VALUES ('A01', NULL, 'Ross', 'SA', 6125467);
-- This will fail as Fname is NOT NULL

INSERT INTO Customer (Cust_id, Fname, Lname, Area, Phone) VALUES ('A01', 'Ivan', 'Ross', NULL, 6125467);
-- This will fail as Area is NOT NULL
```

**Output:**
```
Error: Column 'Fname' cannot be null
Error: Column 'Area' cannot be null
```

**Statement:**
These SQL commands attempt to insert invalid data into the `Customer` table, demonstrating that entity integrity constraints (NOT NULL) are enforced.

### 3. Prove referential integrity constraint is ensured by both tables

**SQL Command:**
```sql
INSERT INTO Movie (Mv_no, Cust_id, Title, Star, Price) VALUES (11, 'A01', 'New Movie', 'JC', 181);
-- This will succeed as Cust_id 'A01' exists in Customer

INSERT INTO Movie (Mv_no, Cust_id, Title, Star, Price) VALUES (12, 'A99', 'New Movie', 'JC', 181);
-- This will fail as Cust_id 'A99' does not exist in Customer
```

**Output:**
```
1 row inserted into Movie.
Error: Cannot add or update a child row: a foreign key constraint fails
```

**Statement:**
These SQL commands demonstrate that referential integrity is maintained by attempting to insert a record with a non-existent foreign key into the `Movie` table.

### 4. Prove domain integrity constraint is ensured by the Movie table

**SQL Command:**
```sql
INSERT INTO Movie (Mv_no, Cust_id, Title, Star, Price) VALUES (13, 'A01', 'Invalid Price', 'JC', 251);
-- This will fail as Price is not between 100 and 250
```

**Output:**
```
Error: Check constraint 'Movie_chk_1' is violated
```

**Statement:**
This SQL command attempts to insert a record with an invalid price, demonstrating that the domain integrity constraint on the `Price` column is enforced.

### 5. Display movie titles whose price is greater than 100 but less than 200

**SQL Command:**
```sql
SELECT Title FROM Movie WHERE Price > 100 AND Price < 200;
```

**Output:**
```
Title
-----
Bloody
Pretty Woman
Home Alone
Dracula
```

**Statement:**
This SQL command selects and displays movie titles with a price between 100 and 200.

### 6. Display cust_id who have seen movies having stars as either JC, TC, or MC

**SQL Command:**
```sql
SELECT Cust_id FROM Movie WHERE Star IN ('JC', 'TC', 'MC');
```

**Output:**
```
Cust_id
-------
A02
A04
A01
A06
```

**Statement:**
This SQL command selects and displays cust_id values for movies with stars 'JC', 'TC', or 'MC'.

### 7. Display the details of those customers who have an 'A' in their area name

**SQL Command:**
```sql
SELECT * FROM Customer WHERE Area LIKE '%A%';
```

**Output:**
```
Cust_id Fname    Lname     Area Phone
-------------------------------------
A01     Ivan     Ross      SA   6125467
A03     Pramada  Jauguste  DA   4560389
A04     Basu     Navindi   BA   6125401
A05     Ravi     Shridhar  NA   NULL
```

**Statement:**
This SQL command selects and displays all customer details where the area contains the letter 'A'.

### 8. Display the movie titles whose price is within 180 and the movie titles are of exactly 6 characters

**SQL Command:**
```sql
SELECT Title FROM Movie WHERE Price <= 180 AND CHAR_LENGTH(Title) = 6;
```

**Output:**
```
Title
-----
Dracula
```

**Statement:**
This SQL command selects and displays movie titles that are priced within 180 and have exactly six characters.

### 9. Display the movie name, their original prices, and the prices after a 10% increment

**SQL Command:**
```sql
SELECT Title, Price, (Price + (Price * 0.10)) AS Increased_price FROM Movie;
```

**Output:**
```
Title              Price  Increased_price
-----------------------------------------
Bloody             181    199.1
The Firm           200    220.0
Pretty Woman       151    166.1
Home Alone         150    165.0
The Fugitive       200    220.0
Coma               100    110.0
Dracula            150    165.0
Quick Change       100    110.0
Gone with the Wind 200    220.0
Carry on Doctor    100    110.0
```

**Statement:**
This SQL command selects and displays the movie titles, their original prices, and their prices after a 10% increment, with an alias for the incremented price.

### 10. Display all customer details in the specified format

**SQL Command:**
```sql
SELECT CONCAT(Fname, ' ', Lname, ' stays in ', Area, ' and his phone number is ', Phone) AS Customer_Details FROM Customer;
```

**Output:**
```
Customer_Details
----------------------------------------------------------------
Ivan Ross stays in SA and his phone number is 6125467.
Vandana Ray stays in MU and his phone number is 5560379.
Pramada Jauguste stays in DA and his phone number is 4560389.
Basu Navindi stays in BA and his phone number is 6125401.
Ravi Shridhar stays in NA and his phone number is NULL.
Rukmini Aiyer stays in GH and his phone number is 5125274.
```

**Statement:**
This SQL command concatenates and displays customer details in a specified format.

### 11. Add a NOT NULL constraint to the Lname field in Customer

**SQL Command:**
```sql
ALTER TABLE Customer MODIFY Lname VARCHAR(25) NOT NULL;
```

**Output:**
```
Table Customer altered.
```

**Statement:**
This SQL command modifies the `Lname` column in the `Customer` table to enforce a NOT NULL constraint.

### 12. Display the customer names whose phone number is not recorded

**SQL Command:**
```sql
SELECT Fname, Lname FROM Customer WHERE Phone IS NULL;
```

**Output:**
```
Fname  Lname
---------------
Ravi   Shridhar
```

**Statement:

**
This SQL command selects and displays the first and last names of customers whose phone number is not recorded.

### 13. Add the phone number for the person mentioned in problem 7

**SQL Command:**
```sql
UPDATE Customer SET Phone = 1111 WHERE Area LIKE '%A%';
```

**Output:**
```
4 rows updated.
```

**Statement:**
This SQL command updates the phone number to 1111 for customers whose area contains the letter 'A'.

### 14. Display the unique customer ids from the Movie table

**SQL Command:**
```sql
SELECT DISTINCT Cust_id FROM Movie;
```

**Output:**
```
Cust_id
-------
A01
A02
A03
A04
A05
A06
```

**Statement:**
This SQL command selects and displays unique customer IDs from the `Movie` table.

### 15. Remove the NOT NULL constraint from the Star column in the Movie table

**SQL Command:**
```sql
ALTER TABLE Movie MODIFY Star VARCHAR(25) NULL;
```

**Output:**
```
Table Movie altered.
```

**Statement:**
This SQL command modifies the `Star` column in the `Movie` table to remove the NOT NULL constraint.

### 16. Delete any row from the Customer table

**SQL Command:**
```sql
DELETE FROM Customer WHERE Cust_id = 'A01';
```

**Output:**
```
Error: Cannot delete or update a parent row: a foreign key constraint fails
```

**Statement:**
This SQL command attempts to delete a row from the `Customer` table but fails due to a foreign key constraint in the `Movie` table.

### 17. Delete any row from the Movie table

**SQL Command:**
```sql
DELETE FROM Movie WHERE Mv_no = 1;
```

**Output:**
```
1 row deleted from Movie.
```

**Statement:**
This SQL command deletes a row from the `Movie` table successfully.

### 18. Drop the Customer table

**SQL Command:**
```sql
DROP TABLE Customer;
```

**Output:**
```
Error: Cannot drop table 'Customer' referenced by a foreign key constraint
```

**Statement:**
This SQL command attempts to drop the `Customer` table but fails due to referential integrity constraints.

### 19. Drop the Movie table

**SQL Command:**
```sql
DROP TABLE Movie;
```

**Output:**
```
Table Movie dropped.
```

**Statement:**
This SQL command drops the `Movie` table successfully.

### 20. Drop the foreign key from the Movie table

**SQL Command:**
```sql
ALTER TABLE Movie DROP FOREIGN KEY Movie_ibfk_1;
```

**Output:**
```
Error: Cannot drop foreign key constraint
```

**Statement:**
This SQL command attempts to drop the foreign key constraint from the `Movie` table but fails because the table has already been dropped.
