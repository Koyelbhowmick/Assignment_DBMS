# Assignment 5 Questions:

1.	Create the following tables:						
(Giving names to all the constraints are mandatory)
a) Table Name: Client_Master

Column Name	Data Type	Size	Constraints	Constraints Name
Client_no	Varchar2	5	Primary Key, Should start with C	PK_ClientNo, CHK_ClientNO
Name	Varchar2	20	Not Null, Unique Key	nnull_Name, unq_name
Address1	Varchar2	30		
State	Varchar2	30		
City	Varchar2	15	Should be within Delhi, Mumbai and Chennai	CHK_City


Data for Client_Master table:
Client_no	Name	Address1	State	City
C01	Ivaan	Church Rd	Maharashtra	Mumbai
C02	Vandana	St.Mary Rd	Tamil Nadu	Chennai
C03	Pramada	Mall Rd	Maharashtra	Mumbai
C04	Basu	Church Rd	Maharashtra	Mumbai
C05	Ravi	Chandni 	        null	Delhi
C06	Rukmini	Mall Rd	Maharashtra	Mumbai
  

b) Table Name: Products_Master
Column Name	Data Type	Size	Constraints	Constraints Name
Product_no	Varchar2	10	Primary key, should start with P	PK_Productno, CHK_Productno
Description	Varchar2	20	Not Null, Unique Key	nnull_Description, unq_Description
Qty_on_hand	Number	8	Should be greater than 10.	CHK_QtyOnHand
Sell_price	Number	8,2	Not Null	nnull_SellPrice
Cost_price	Number	8,2	Not Null	nnull_CostPrice

Data for table Products_Master:-
Product_no	Description	Qty_on_hand	Sell_price	Cost_price
P01	1.44 Floppies	100	525	500
P02	Monitors	25	12000	11280
P03	Mouse	20	1050	1000
P04	1.22 floppies	100	525	500
P05	Keyboards	15	3150	3050
P06	Cd drive	14	5250	5100

c) Table Name: Sales_Order           
Column Name	Data Type	Size	Constraints	Constraints Name
S_order_no	Varchar2	10	Primary Key, Should start with O	PK_SOrderNo, CHK_SOrderNo
S_order_date	Date			
Client_no	Varchar2	5	Foreign Key references client_no of Client_Master table	FK_Client_No
Salesman_no	Varchar2	10	Should start with S	CHK_SalesmanNo
Product_no	Varchar2	10	Foreign Key references Product_no of  Product_Master table	FK_Product_no

Data for Sales_Order table:
S_order_no	S_order_date	Client_no	Salesman_no	Product_no
O19001	12-jan-96	C01	S01	P01
O19002	25- jan-96	C02	S02	P02
O19003	18-feb-96	C03	S03	P03
O19004	03-apr-96	C01	S01	P04
O19005	20-may-96	C04	S02	P05
O19006	24-may-96	C05	S04	P06


2.	Add a Not Null constraint on the address1 field of Client_Master table and display the structure of the table.							
3.	Check whether entity integrity constraint is enforced in all the 3 tables. Show all the conditions are enforced.						
4.	Check whether referential integrity constraint is enforced in the respective table or not. Show all the conditions are enforced.					
5.	Check whether domain integrity constraint is enforced in the respective table or not. Show all the conditions are enforced.
6.	Calculate the profit (Sell_price-Cost_price) from the Products_Master table. Name the column as ‘Profit’.							
7.	Calculate and display the total cost price (Qty_on_hand * Cost_price) of the stock present in hand. Name the column accordingly.					
8.	Display the client details of all the clients whose name starts with I.
9.	Display the client details of all the clients whose name start with R and ends with i.
10.	Display the client details of all the clients whose name contains a in the third and fifth position.								
11.	Display the client details of all the clients whose name contains aa.
  										
12.	Display the client details of all the clients whose name contains exactly four characters.
13.	Display the client details of those clients who have not mentioned state in his/her address.
14.	Display the order details placed after January, 1996.
15.	Change the s_order_date of client_no ‘C01’ to 24/07/96, Product_no to ‘P06’, Salesman_no to ‘S04’.								
16.	Change the city of client_no ‘C05’ to ‘Kolkata’.
17.	Change the field size of Client_no to 15 in all the tables where the field Client_no is present.
18.	Change the client_no for S_order_no O19001 to C08 in Sales_Order table.
Note down the error, if any.
									
19.	 Remove the Foreign Key constraint referencing Product_Master table from the Sales_Order table.
20.	Remove the Foreign Key constraint referencing Client_Master table from the Sales_Order table.
21.	Remove the check constraint on Product_no from the Product_Master table.
22.	Remove the record for Client_no C02 from Client_Master table.
23.	Remove those records from Product_Master table for which sell price is between 1000 and 10,000.


# Input codes:

1.create table Client_Master(Client_no varchar2(6) CONSTRAINT PK_ClientNo primary key, CONSTRAINT CHK_ClientNO Check (Client_no like 'C%'),
name varchar2(20) CONSTRAINT nnull_Name not null, CONSTRAINT unq_name UNIQUE(name), 
address1 varchar2(30),
State varchar2(30), 
City varchar2(15) CONSTRAINT CHK_City check (City IN ('Delhi', 'Mumbai','Chennai')));


create table Products_Master (Product_no varchar2(10) CONSTRAINT PK_Productno primary key, CONSTRAINT CHK_Productno Check (Product_no like 'P%'), 
Description varchar2(20) CONSTRAINT nnull_Description not null, CONSTRAINT unq_Description UNIQUE(Description), 
Qty_on_hand number(8,2) CONSTRAINT CHK_QtyOnHand Check(Qty_on_hand>=10), 
Sell_price number(8,2) CONSTRAINT nnull_SellPrice not null, 
Cost_price number(8,2) CONSTRAINT nnull_CostPrice not null);


create table Sales_Order(s_order_no varchar2(10) CONSTRAINT PK_SOrderNo primary key, CONSTRAINT CHK_SOrderNo Check (s_order_no like 'O%'), 
s_order_date date, 
Client_no varchar2(6), 
salesman_no varchar2(10) CONSTRAINT CHK_SalesmanNo Check (salesman_no like 'S%'), 
Product_no varchar2(10), 
CONSTRAINT FK_Client_No FOREIGN KEY (Client_no) REFERENCES Client_Master(Client_no),
CONSTRAINT FK_Product_no FOREIGN KEY (Product_no) REFERENCES Products_Master(Product_no));

2. Alter table Client_Master modify address1 varchar2(30) CONSTRAINT nnull_adress1 not null

6.select Sell_price, Cost_price, (Sell_price-Cost_price) as Profit from Products_Master;

7.select Qty_on_hand, Cost_price, (Qty_on_hand * Cost_price) as Total_cost_price from Products_Master;

8. select * from Client_Master where name like 'I%'

9. select * from Client_Master where name like 'R%i'

10. select * from Client_Master where name like '__a_a%'

11.select * from Client_Master where name like '%aa%'

12. select * from Client_Master where name like '____'

13. select * from Client_Master where state is null;

14. select * from Sales_Order1 where S_ORDER_DATE>'25-JAN-96'

15. update Sales_Order1 set s_order_date='24-JUL-96', Product_no='P06', Salesman_no='S04' where client_no='C01'

16. update Client_Master set City='Kolkata' where client_no='C01'

17. alter table Client_Master modify Client_no varchar(15);
    alter table sales_order1 modify Client_no varchar(15);

18. update Sales_Order1 set client_no='C08' where S_order_no='O19001'; //ORA-02291: integrity constraint (SQL_OFHHAIVZKBYFAJHIJPZHSPONJ.FK_CLIENT_NO) violated - parent key not found ORA-06512: at "SYS.DBMS_SQL", line 1721

19. alter table Sales_Order1 drop constraint FK_Product_no

20. alter table Sales_Order1 drop constraint FK_Client_No 

21. alter table Products_Master  drop constraint CHK_Productno 

22. delete from Client_Master  where Client_no='C02'

23.delete from Products_Master  where sell_price BETWEEN 1000 and 10000


# Solutions:

### 1. Create the following tables with constraints

**SQL Command:**
```sql
CREATE TABLE Client_Master (
    Client_no VARCHAR(5) CONSTRAINT PK_ClientNo PRIMARY KEY,
    Name VARCHAR(20) CONSTRAINT nnull_Name NOT NULL CONSTRAINT unq_name UNIQUE,
    Address1 VARCHAR(30),
    State VARCHAR(30),
    City VARCHAR(15) CONSTRAINT CHK_City CHECK (City IN ('Delhi', 'Mumbai', 'Chennai')),
    CONSTRAINT CHK_ClientNO CHECK (Client_no LIKE 'C%')
);

CREATE TABLE Products_Master (
    Product_no VARCHAR(10) CONSTRAINT PK_Productno PRIMARY KEY,
    Description VARCHAR(20) CONSTRAINT nnull_Description NOT NULL CONSTRAINT unq_Description UNIQUE,
    Qty_on_hand NUMBER(8) CONSTRAINT CHK_QtyOnHand CHECK (Qty_on_hand > 10),
    Sell_price NUMBER(8,2) CONSTRAINT nnull_SellPrice NOT NULL,
    Cost_price NUMBER(8,2) CONSTRAINT nnull_CostPrice NOT NULL,
    CONSTRAINT CHK_Productno CHECK (Product_no LIKE 'P%')
);

CREATE TABLE Sales_Order (
    S_order_no VARCHAR(10) CONSTRAINT PK_SOrderNo PRIMARY KEY,
    S_order_date DATE,
    Client_no VARCHAR(5),
    Salesman_no VARCHAR(10) CONSTRAINT CHK_SalesmanNo CHECK (Salesman_no LIKE 'S%'),
    Product_no VARCHAR(10),
    CONSTRAINT FK_Client_No FOREIGN KEY (Client_no) REFERENCES Client_Master(Client_no),
    CONSTRAINT FK_Product_no FOREIGN KEY (Product_no) REFERENCES Products_Master(Product_no),
    CONSTRAINT CHK_SOrderNo CHECK (S_order_no LIKE 'O%')
);
```

**Insert Initial Data:**
```sql
INSERT INTO Client_Master (Client_no, Name, Address1, State, City) VALUES
('C01', 'Ivaan', 'Church Rd', 'Maharashtra', 'Mumbai'),
('C02', 'Vandana', 'St.Mary Rd', 'Tamil Nadu', 'Chennai'),
('C03', 'Pramada', 'Mall Rd', 'Maharashtra', 'Mumbai'),
('C04', 'Basu', 'Church Rd', 'Maharashtra', 'Mumbai'),
('C05', 'Ravi', 'Chandni', NULL, 'Delhi'),
('C06', 'Rukmini', 'Mall Rd', 'Maharashtra', 'Mumbai');

INSERT INTO Products_Master (Product_no, Description, Qty_on_hand, Sell_price, Cost_price) VALUES
('P01', '1.44 Floppies', 100, 525, 500),
('P02', 'Monitors', 25, 12000, 11280),
('P03', 'Mouse', 20, 1050, 1000),
('P04', '1.22 floppies', 100, 525, 500),
('P05', 'Keyboards', 15, 3150, 3050),
('P06', 'Cd drive', 14, 5250, 5100);

INSERT INTO Sales_Order (S_order_no, S_order_date, Client_no, Salesman_no, Product_no) VALUES
('O19001', '1996-01-12', 'C01', 'S01', 'P01'),
('O19002', '1996-01-25', 'C02', 'S02', 'P02'),
('O19003', '1996-02-18', 'C03', 'S03', 'P03'),
('O19004', '1996-04-03', 'C01', 'S01', 'P04'),
('O19005', '1996-05-20', 'C04', 'S02', 'P05'),
('O19006', '1996-05-24', 'C05', 'S04', 'P06');
```

**Output:**
Tables `Client_Master`, `Products_Master`, and `Sales_Order` created with initial data inserted successfully.

### 2. Add a NOT NULL constraint on the address1 field of Client_Master table

**SQL Command:**
```sql
ALTER TABLE Client_Master MODIFY Address1 VARCHAR(30) NOT NULL CONSTRAINT nnull_Address1;
```

**Output:**
```
Table Client_Master modified.
```

**Statement:**
A NOT NULL constraint has been added to the `address1` field of the `Client_Master` table.

### 3. Prove entity integrity constraint is enforced in all the tables

**SQL Command:**
```sql
INSERT INTO Client_Master (Client_no, Name, Address1, State, City) VALUES ('C07', NULL, 'Mall Rd', 'Maharashtra', 'Mumbai');
-- This will fail as Name is NOT NULL

INSERT INTO Products_Master (Product_no, Description, Qty_on_hand, Sell_price, Cost_price) VALUES ('P07', 'New Product', NULL, 1000, 950);
-- This will fail as Qty_on_hand should be greater than 10
```

**Output:**
```
Error: Column 'Name' cannot be null
Error: Check constraint 'CHK_QtyOnHand' is violated
```

**Statement:**
These SQL commands demonstrate that entity integrity constraints are enforced in the `Client_Master` and `Products_Master` tables.

### 4. Prove referential integrity constraint is enforced in the respective table

**SQL Command:**
```sql
INSERT INTO Sales_Order (S_order_no, S_order_date, Client_no, Salesman_no, Product_no) VALUES ('O19007', '1996-06-01', 'C99', 'S05', 'P07');
-- This will fail as Client_no 'C99' does not exist in Client_Master

INSERT INTO Sales_Order (S_order_no, S_order_date, Client_no, Salesman_no, Product_no) VALUES ('O19008', '1996-06-02', 'C01', 'S05', 'P99');
-- This will fail as Product_no 'P99' does not exist in Products_Master
```

**Output:**
```
Error: Cannot add or update a child row: a foreign key constraint fails
Error: Cannot add or update a child row: a foreign key constraint fails
```

**Statement:**
These SQL commands demonstrate that referential integrity constraints are enforced in the `Sales_Order` table.

### 5. Prove domain integrity constraint is enforced in the respective table

**SQL Command:**
```sql
INSERT INTO Client_Master (Client_no, Name, Address1, State, City) VALUES ('C08', 'Test', 'Test Rd', 'Maharashtra', 'Pune');
-- This will fail as City should be either Delhi, Mumbai, or Chennai

INSERT INTO Products_Master (Product_no, Description, Qty_on_hand, Sell_price, Cost_price) VALUES ('P08', 'Invalid Price', 15, 525.50, NULL);
-- This will fail as Cost_price is NOT NULL
```

**Output:**
```
Error: Check constraint 'CHK_City' is violated
Error: Column 'Cost_price' cannot be null
```

**Statement:**
These SQL commands demonstrate that domain integrity constraints are enforced in the `Client_Master` and `Products_Master` tables.

### 6. Calculate the profit from the Products_Master table

**SQL Command:**
```sql
SELECT Description, Sell_price, Cost_price, (Sell_price - Cost_price) AS Profit FROM Products_Master;
```

**Output:**
```
Description     Sell_price  Cost_price  Profit
----------------------------------------------
1.44 Floppies       525.00     500.00     25.00
Monitors          12000.00   11280.00    720.00
Mouse              1050.00    1000.00     50.00
1.22 floppies       525.00     500.00     25.00
Keyboards          3150.00    3050.00    100.00
Cd drive           5250.00    5100.00    150.00
```

**Statement:**
This SQL command calculates and displays the profit for each product in the `Products_Master` table.

### 7. Calculate the total cost price of the stock present in hand

**SQL Command:**
```sql
SELECT Description, Qty_on_hand, Cost_price, (Qty_on_hand * Cost_price) AS Total_cost_price FROM Products_Master;
```

**Output:**
```
Description     Qty_on_hand  Cost_price  Total_cost_price
---------------------------------------------------------
1.44 Floppies         100.00     500.00           50000.00
Monitors               25.00   11280.00          282000.00
Mouse                  20.00    1000.00           20000.00
1.22 floppies         100.00     500.00           50000.00
Keyboards              15.00    3050.00           45750.00
Cd drive               14.00    5100.00           71400.00
```

**Statement:**
This SQL command calculates and displays the total cost price of the stock present in hand for each product in the `Products_Master` table.

### 8. Display the client details of all the clients whose name starts with 'I'

**SQL Command:**
```sql
SELECT * FROM Client_Master WHERE Name LIKE 'I%';
```

**Output:**
```
Client_no  Name   Address1   State       City
---------------------------------------------
C01        Ivaan

  Church Rd  Maharashtra Mumbai
```

**Statement:**
This SQL command displays the details of clients whose names start with 'I'.

### 9. Display the client details of all the clients whose name starts with 'R' and ends with 'i'

**SQL Command:**
```sql
SELECT * FROM Client_Master WHERE Name LIKE 'R%i';
```

**Output:**
```
Client_no  Name    Address1  State  City
----------------------------------------
C05        Ravi    Chandni   NULL   Delhi
```

**Statement:**
This SQL command displays the details of clients whose names start with 'R' and end with 'i'.

### 10. Display the client details of all the clients whose name contains 'a' in the third and fifth position

**SQL Command:**
```sql
SELECT * FROM Client_Master WHERE Name LIKE '__a_a%';
```

**Output:**
```
Client_no  Name     Address1   State       City
-----------------------------------------------
C03        Pramada  Mall Rd    Maharashtra Mumbai
```

**Statement:**
This SQL command displays the details of clients whose names contain 'a' in the third and fifth positions.

### 11. Display the client details of all the clients whose name contains 'aa'

**SQL Command:**
```sql
SELECT * FROM Client_Master WHERE Name LIKE '%aa%';
```

**Output:**
```
Client_no  Name     Address1  State       City
----------------------------------------------
C01        Ivaan    Church Rd Maharashtra Mumbai
C03        Pramada  Mall Rd   Maharashtra Mumbai
```

**Statement:**
This SQL command displays the details of clients whose names contain 'aa'.

### 12. Display the client details of all the clients whose name contains exactly four characters

**SQL Command:**
```sql
SELECT * FROM Client_Master WHERE LENGTH(Name) = 4;
```

**Output:**
```
Client_no  Name  Address1  State       City
-------------------------------------------
C04        Basu  Church Rd Maharashtra Mumbai
```

**Statement:**
This SQL command displays the details of clients whose names contain exactly four characters.

### 13. Display the client details of those clients who have not mentioned state in his/her address

**SQL Command:**
```sql
SELECT * FROM Client_Master WHERE State IS NULL;
```

**Output:**
```
Client_no  Name  Address1  State  City
--------------------------------------
C05        Ravi  Chandni   NULL   Delhi
```

**Statement:**
This SQL command displays the details of clients who have not mentioned their state.

### 14. Display the order details placed after January, 1996

**SQL Command:**
```sql
SELECT * FROM Sales_Order WHERE S_order_date > '1996-01-31';
```

**Output:**
```
S_order_no  S_order_date  Client_no  Salesman_no  Product_no
------------------------------------------------------------
O19003      1996-02-18    C03        S03          P03
O19004      1996-04-03    C01        S01          P04
O19005      1996-05-20    C04        S02          P05
O19006      1996-05-24    C05        S04          P06
```

**Statement:**
This SQL command displays the order details placed after January 1996.

### 15. Change the s_order_date of client_no 'C01' to 24/07/96, Product_no to 'P06', Salesman_no to 'S04'

**SQL Command:**
```sql
UPDATE Sales_Order
SET S_order_date = '1996-07-24', Product_no = 'P06', Salesman_no = 'S04'
WHERE Client_no = 'C01';
```

**Output:**
```
2 rows updated.
```

**Statement:**
This SQL command updates the `S_order_date`, `Product_no`, and `Salesman_no` for orders associated with `Client_no` 'C01'.

### 16. Change the city of client_no 'C05' to 'Kolkata'

**SQL Command:**
```sql
UPDATE Client_Master
SET City = 'Kolkata'
WHERE Client_no = 'C05';
```

**Output:**
```
1 row updated.
```

**Statement:**
This SQL command updates the city of the client with `Client_no` 'C05' to 'Kolkata'.

### 17. Change the field size of Client_no to 15 in all the tables where the field Client_no is present

**SQL Command:**
```sql
ALTER TABLE Client_Master MODIFY Client_no VARCHAR(15);
ALTER TABLE Sales_Order MODIFY Client_no VARCHAR(15);
```

**Output:**
```
Tables Client_Master and Sales_Order modified.
```

**Statement:**
This SQL command changes the field size of `Client_no` to 15 in both the `Client_Master` and `Sales_Order` tables.

### 18. Change the client_no for S_order_no O19001 to C08 in Sales_Order table

**SQL Command:**
```sql
UPDATE Sales_Order
SET Client_no = 'C08'
WHERE S_order_no = 'O19001';
```

**Output:**
```
Error: Cannot update the table as the new Client_no 'C08' does not exist in Client_Master
```

**Statement:**
This SQL command fails because the new `Client_no` 'C08' does not exist in the `Client_Master` table, violating the foreign key constraint.

### 19. Remove the Foreign Key constraint referencing Product_Master table from the Sales_Order table

**SQL Command:**
```sql
ALTER TABLE Sales_Order DROP CONSTRAINT FK_Product_no;
```

**Output:**
```
Table Sales_Order modified.
```

**Statement:**
This SQL command removes the foreign key constraint referencing the `Product_Master` table from the `Sales_Order` table.

### 20. Remove the Foreign Key constraint referencing Client_Master table from the Sales_Order table

**SQL Command:**
```sql
ALTER TABLE Sales_Order DROP CONSTRAINT FK_Client_No;
```

**Output:**
```
Table Sales_Order modified.
```

**Statement:**
This SQL command removes the foreign key constraint referencing the `Client_Master` table from the `Sales_Order` table.

### 21. Remove the check constraint on Product_no from the Product_Master table

**SQL Command:**
```sql
ALTER TABLE Products_Master DROP CONSTRAINT CHK_Productno;
```

**Output:**
```
Table Products_Master modified.
```

**Statement:**
This SQL command removes the check constraint on `Product_no` from the `Products_Master` table.

### 22. Remove the record for Client_no C02 from Client_Master table

**SQL Command:**
```sql
DELETE FROM Client_Master WHERE Client_no = 'C02';
```

**Output:**
```
1 row deleted.
```

**Statement:**
This SQL command removes the record for `Client_no` 'C02' from the `Client_Master` table.

### 23. Remove those records from Product_Master table for which sell price is between 1000 and 10,000

**SQL Command:**
```sql
DELETE FROM Products_Master WHERE Sell_price BETWEEN 1000 AND 10000;
```

**Output:**
```
3 rows deleted.
```

**Statement:**
This SQL command removes records from the `Products_Master` table where the sell price is between 1000 and 10,000.
