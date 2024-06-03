Ex.No:2 DATABASE QUERYING – SIMPLE QUERIES, NESTED QUERIES,
SUB QUERIES AND JOINS
AIM:
To implement and execute a query for manipulating & storing data items in MySQL database
using Structured Query Language commands
SYNTAX:
NESTED and SUB QURIES:
SELECT column_name(s) FROM table_name WHERE condition OPERATOR (SELECT
column_name(s) FROM table_name);
JOINS:
INNER JOIN:
SELECT column_name(s) FROM table_name1 INNER JOIN table_name2 ON
table_name1.column_name=table_name2.column_name
LEFT JOIN
SELECT column_name(s)FROM table_name1LEFT JOIN table_name2ON
table_name1.column_name=table_name2.column_name
RIGHT JOIN
SELECT column_name(s) FROM table_name1 RIGHT JOIN table_name2 ON
table_name1.column_name=table_name2.column_name
FULL JOIN
SELECT column_name(s)FROM table_name1FULL JOIN table_name2ON
table_name1.column_name=table_name2.column_name

SIMPLE QUERIES
1. Display the loan relation with attributes amount multiplied by 100.
mysql> select amount*100 from loan_m;
2. Findall numbers for loan made at perryridge branch with loan amount greater than 1400.
mysql> select loan_no from loan_m where branch_name='perryridge'
and amount>1400;
3. Findall loan numbers for loan’s with loan amount between 900 and 1500.
mysql> select loan_no from loan_m where amount between 900 and
1500;
4. Findthe names of customer of customer whose street names includes the character r in
the third position.
mysql> select customer_name from customer_m where customer_street
like'__r%';
5. Findthe names of customer_m whose street name starts withsubstring ‘ma’.
mysql> select customer_name from customer_m where customer_street
like'ma%';
6. Displaythe entire loan relation in descending order ofamount.
mysql> select * from loan_m order by amount desc;
7. Findtotal number of customer.
mysql> select count(customer_id) from customer_m;
8. Findall the loan number that appears in the loan relationwith NULL values for amount.
mysql> select loan_no from loan_m where amount is null;
9.mysql> select * from customer_m where customer_id=’c_02’;

NESTED and SUB QUERIES:
1. Find all the name of all branches that have assets greater than atleast one bank located in
Stanford. (Nested queries)
mysql>Select branch_name from branch_ma where assets >ANY (select
assets
from branch_ma where branch_city='stanford');
2. Display the entire customer name in alphabetical order that have loan in Perryridge.(Nested
queries).
mysql>Select customer_name from customer_ma where customer_id=ANY
(
select customer_id from borrow_ma where borrow_ma.loan_no=ANY(
select loan_no from loan_ma where branch_name='Perryridge'))
order by customer_ma.customer_name asc;
3. Find all customer having both account and loan at same branch.(Nested queries)
mysql>Select depositor_ma.customer_id from depositor_ma where
customer_id IN (select borrow_ma.customer_id from borrow_ma);
4. Find all customers who have loan at bank but who don’t have account at same
branch.(Nested queries).
mysql>Select borrow_ma.customer_id from borrow_ma where
customer_id NOT IN (
select depositor_ma.customer_id from depositor_ma);
5. Find the name of all branches that have assets greater than those atleast one branch located
in Harrison.(Nested queries).
mysql>Select branch_name from branch_ma where assets>any(select
assets from branch_ma
where branch_city='Harrison');

JOINS:
1. For all customer who have loan from the bank find their ID’s , loan number and loan
amount.(Join)
mysql>Select borrow_ma.customer_id, loan_ma.loan_no,
loan_ma.amount from borrow_ma,
loan_ma where loan_ma.loan_no=borrow_ma.loan_no;
2. For all customers who have loan at perryridge branch find their ID’s,loan ID,loan
amount.(Join)
mysql>Select borrow_ma.customer_id, loan_ma.loan_no,
loan_ma.amount from loan_ma,borrow_ma where
borrow_ma.loan_no=loan_ma.loan_no and
loan_ma.branch_name='Perryridge';
3. Find the number of depositor at each branch.(Join)
mysql>Select
account_ma.branch_name,count(depositor_ma.customer_id) from
account_ma,depositor_ma where
depositor_ma.account_no=account_ma.account_no group by
account_ma.branch_name;

RESULT:



Ex.No:3 VIEWS, INDEXES AND SYNONYM
AIM:
To implement and execute view,sequence,indexes,savepoint in MYSQL using SQL commands.
VIEWS:
Create view <viewname> as any select query; (Ex: select * from <tablename> where
<condition>)
SEQUENCE:
Create table <tablename> (column1 datatype1primary key auto_increment,column2 datatype
2……columnN datatypeN)
SYNONYM:
Create synonym<synonym name> for <table name>;
VIEWS:
1) Create a view using aggregate functions to calculate the age of the Person
mysql> create table person_m(name varchar(20) primary key,dob
date,person_city varchar(20));
mysql> desc person_m;
mysql> insert into person_m values('abdulkalam','1931-08-
18','rameshwaram');
mysql> select * from person_m;
mysql> create view personage_m as select
name,datediff(sysdate(),dob)/365.25 as age from person_m;
mysql> select * from personage_m;
mysql> insert into person_m values('jorden','1970-07-08','usa');
mysql> select * from personage_m;

SEQUENCE:
2) Create a sequence and design the department table in the given attribute.
mysql> create table department_m(department_id int primary key
auto_increment,department_name varchar(20));
mysql> desc department_m;
mysql> insert into department_m(department_name)values('it');
mysql> insert into department_m(department_name)values('cse');
mysql>
insert into department_m(department_name)values('mechanical');
mysql> insert into department_m(department_name)values('aero');
mysql> select * from department_m;

SYNONYM(UsingOracle)
4) Show the effect of synonym
CREATING A SYNONYM FOR A TABLE
CREATE TABLE product_m (product_nameVARCHAR2(25) PRIMARY KEY,
product_price NUMBER(4,2), quantity_on_hand NUMBER(5,0), last_stock_date DATE);
Table created.
AFTER INSERTING THE RECORDS TO PRODUCT TABLE
SQL> SELECT * FROM product_m;
SQL> SELECT * FROM prod_m;
SELECT * FROM prod_m
*
ERROR at line 1:
ORA-00942: table or view does not exist
SQL> CREATE SYNONYM prod_m FOR product_m;
SQL> SELECT * FROM prod_m;
SQL> drop SYNONYM prod_m;
SQL> drop table product_m;
RESULT:




Ex.No.4 STUDY OF PL/SQL-SIMPLE PROGRAMS
AIM:
To implement and execute PL/SQL in Mysql using Procedural Language concepts.
PL/SQL: which is a block-structured language; this means that the PL/SQL programs are divided and
written in logical blocks of code. Each block consists of three sub-parts.
1 Declarations
This section starts with the keyword DECLARE. It is an optional section and defines all variables, cursors,
subprograms, and other elements to be used in the program.
2 Executable Commands
This section is enclosed between the keywords BEGIN and END and it is a mandatory section. It consists
of the executable PL/SQL statements of the program. It should have at least one executable line of code,
which may be just a NULL command to indicate that nothing should be executed.
3 Exception Handling
This section starts with the keyword EXCEPTION. This optional section contains exception(s) that handle
errors in the program.
Every PL/SQL statement ends with a semicolon (;). PL/SQL blocks can be nested within other PL/SQL
blocks using BEGIN and END. Following is the basic structure of a PL/SQL block −

DECLARE
<declarations section>
BEGIN
<executable command(s)>
EXCEPTION
<exception handling>
END;

Simple Programs:
(i) Pl/SQL Program to add 2 numbers
DECLARE
a integer := 10;
b integer := 20;
c integer;
f real;
BEGIN
c := a + b;
dbms_output.put_line('Value of c: ' || c);
f := 70.0/3.0;
dbms_output.put_line('Value of f: ' || f);
END;
/
When the above code is executed, it produces the following result −


(ii) Pl/SQL Program to calculate area and perimeter of Rectangle.
DECLARE
LENGTH number:=&LENGTH;
Width number:=&width;
Area number;
Parimeter number;
BEGIN Area:=LENGTH*width;
Parimeter:= 2*(LENGTH+width);
dbms_output.put_line('AREA OF RECTANGLE IS:'||Area);
dbms_output.put_line('PARIMETER OF RECTANGLE IS:'||PARIMETER);
END;
/
Output:

(iii) Pl/SQL Program to obtain factorial of a number.
Declare
num number:= #
fact number:= 1;
temp number;
begin
temp := num;
while (num > 0)
loop
fact := fact * num;
num := num - 1;
end loop;
Dbms_Output.Put_line('factorial of ' || temp || ' is ' || fact);
end;
/

(iv) PL/SQL block to obtain Fibonacci series.
declare
a number(3):=1;
b number(3):=1;
c number(3);
n number(3):=&n;
begin
Dbms_output.put_line('the fibinocci series is:');
while a<=n
loop
dbms_output.put_line(a);
c:=a+b;
a:=b;
b:=c;
end loop;
end;
/
RESULT:




Ex.No.5 DATABASE PROGRAMMING: IMPLICIT AND EXPLICIT CURSORS
AIM:
To implement and execute cursor in Mysql using Procedural Language concepts.
Cursor:A cursor is a pointer to this context area. PL/SQL controls the context area through a cursor. A
cursor holds the rows (one or more) returned by a SQL statement. The set of rows the cursor holds is
referred to as the active set.
There are two types of cursors −
• Implicit cursors
• Explicit cursors

SYNTAX:
IMPLICIT CURSOR:
Sql%attribute name
Where attribute name can be FOUND, NOT FOUND, ISOPEN, %ROWCOUNT
EXPLICIT CURSOR:
Creating an explicit cursor
CURSOR <cursor_name> IS select_statement;
Opening the Cursor
OPEN <cursor_name>;
Fetching the Cursor
FETCH <cursor_name>INTO attributes;
Closing the Cursor
CLOSE <cursor_name>;

IMPLICIT CURSOR (in Oracle)
DECLARE
rows number(2);
BEGIN
UPDATE student SET stu_class = stu_class + 2;
IF sql%notfound THEN
dbms_output.put_line('no student selected');
ELSIF sql%found THEN
rows := sql%rowcount;
dbms_output.put_line(rows || ' student selected ');
END IF;
END;
4 student selected

EXPLICIT CURSOR:
mysql> delimiter $$
mysql> create procedure curdemo(id int)
-> begin
-> declare name varchar(255);
-> declare cur1 cursor for select stu_name from student where
stu_id=id;
->open cur1;
-> fetch cur1 into name;
->select name;
->close cur1;
->end $$
mysql> delimiter ;
mysql> call curdemo(2);
RESULT:





Ex.No.6 PROCEDURES AND FUNCTIONS
AIM:
To implement and execute Procedures and functions in Mysql using Procedural Language
concepts.
PROCEDURES: Procedure is a sub program used to perform an action. Replace-recreates the procedure
if it already exists.
3 MODES:
1) IN – Means you must specify a value for the argument at the time execution of the procedure.
2) OUT-passes back a value to its calling program.
3) INOUT – When calling the procedure, yu must specify the value and that procedures passes value
back to the calling procedure.
SYNTAX:
Create procedure <procedure_name> (argument {in, out, in out} data type) is
Variable declaration
Begin
Pl/SQL Subprogram body.
End;
FUNCTION: A function is a sub program that accepts argument and returns a unique value to the caller.
SYNTAX :
Create function <function_name> (parameter) return <data type> is
Variable declaration
Begin
Pl/SQL Subprogram body.
Return statement
End;
1. Procedures:
Create a procedure to update the phone number to customer table
Mysql> create table customer_m (cust_id int primary key,cust_name
varchar(20),cust_phone int);
Mysql> desc customer_m;
Mysql> insert into customer_m (cust_id,cust_name)values(201,'raja');
Mysql> insert into customer_m (cust_id,cust_name)values(202,'ravi');
Mysql> select * from customer_m;
Procedure
---------
DELIMITER //
CREATE PROCEDURE c
(IN ph int,IN cid int)
BEGIN
declare name varchar(20);
select cust_name into name from customer_m where cust_id=cid;
if name is null then
select 'Name is not there';
ELSE
update customer_m set cust_phone=ph where cust_id=cid;
END IF;
END //
DELIMITER ;
Mysql> call c(66,88);
Mysql> call c(98567,201);
Mysql> select * from customer_m;


2. Functions
Create a function to check whether particular customer is having phone number or Not
create table customer_m (custid int,phone int);
insert into customer_m values(101,899);
mysql> create function check12(cust_id int)
->returns varchar(20)
-> begin
-> declare ph int;
->select phone into ph from customer_m where custid=cust_id;
->if ph is null then
-> return 'Mobile Number is not there';
-> ELSE
-> return 'Mobile Number is there';
-> END IF;
->end //
mysql> select * from customer_m;
mysql> select check12(101);
mysql> insert into customer_m (custid)values(102);
mysql> select * from customer_m;
mysql> select check12(102);
RESULT:



Ex.No.7 TRIGGERS
AIM:
To implement and execute triggers and functions in Mysql using Procedural Language concepts.
TRIGGERS:
1) Trigger is a special type of procedure that the oracle executes when an insert, modify or
delete operation is performed against a given table.
2) It is a stored sub program associated with a table.
3) It is used to keep an audit trial of a table, to prevent invalid transaction, enforce complex
security authorization, to generate data automatically.


SYNTAX FOR TRIGGER
CREATE TRIGGER <TRIGGER NAME>
{BEFORE/AFTER}
{INSERT/UPDATE/DELETE}
ON <TABLENAME>
REFRENCECING {OLD AS OLD /NEW AS NEW}
[FOR EACH STATEMENT /FOR EACH ROW [WHEN <CONDITION>]]
DECLARE
Variable declaration
Constant declaration
BEGIN
PL/SQL Sub program body.
END;
1) Create a trigger to calculate the total and average of a student in the student table.
mysql> create table student_m (regno int primary key,name
varchar(20),tamil int,english int,maths int,science int,social
int,total int,average int);
Mysql> desc student_m;
Mysql> CREATE TRIGGER avg1 BEFORE INSERT ON student_m FOR EACH ROW
-> BEGIN
-> SET
new.total=new.tamil+new.english+new.maths+new.science+new.social;
-> SET new.average=new.total/5;
-> END;//
DELIMITER ;
mysql> insert into student_m
(regno,name,tamil,english,maths,science,social)values(101,'raja',90,95
,100,100,99);
Mysql> select * from student;

RESULT:




Ex.No.8 EXCEPTION HANDLING
AIM:
To implement and execute PL/SQL Block that handles all types of exceptions in Oracle Database
using Procedural Language concepts.


SYNTAX
DECLARE
Variable declaration
BEGIN
Program Execution
EXCEPTION
Exception handling
END;
ZERO_DIVIDE EXCEPTION
SQL> BEGIN
2 DBMS_OUTPUT.PUT_LINE(1 / 0);
3 END;
4 /
BEGIN
*
ERROR at line 1:
ORA-01476: divisor is equal to zero
ORA-06512: at line 2
------------------------------------------------------
BEGIN
2 DBMS_OUTPUT.PUT_LINE(1 / 0);
3 EXCEPTION
4 WHEN ZERO_DIVIDE THEN
5 DBMS_OUTPUT.PUT_LINE('Division by zero');
6 END;
7 /
Division by zero
PL/SQL procedure successfully completed.

INVALID_NUMBER EXCEPTION
1 BEGIN
2 INSERT INTO employees(DEPARTMENT_ID)VALUES('101x');
3 EXCEPTION
4 WHEN INVALID_NUMBER THEN
5 DBMS_OUTPUT.PUT_LINE('Conversion of string to number failed');
6* end;
SQL> /
Conversion of string to number failed
PL/SQL procedure successfully completed.

OTHERS EXCEPTION
1 BEGIN
2 DBMS_OUTPUT.PUT_LINE(1 / 0);
3 EXCEPTION
4 WHEN OTHERS THEN
5 DBMS_OUTPUT.PUT_LINE('An exception occurred');
6* END;
7 /
An exception occurred
PL/SQL procedure successfully completed.
RESULT:
