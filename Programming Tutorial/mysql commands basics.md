CREATE DATABASE MITAOE_DB;
SHOW DATABASES;
CREATE TABLE STUDENT_INFO (name VARCHAR(20),
Age INT(2),
DOB DATE,
PINCODE INT(6));
You will get error as no DB is select
USE MITAOE_DB;
CREATE TABLE STUDENT_INFO(name VARCHAR(20),
Age INT(2),
DOB DATE,
PINCODE INT(6));
Again we fire table query and after “SHOW TABLES”
Now to display tables in Database
SELECT * FROM MITAOE_DB;
Table ‘MITAOE_DB.Student_info’ does not exist,
DESC STUDENT_INFO
DESCRIBE STUDENT_INFO
SELECT * FROM STUDENT_INFO;
SELECT * FROM MITAOE_DB.STUDENT_INFO;
USE mysql;
Fire query
DESC STUDENT_INFO;
ERROR: Gives error as STUDENT_INFO is not table in mysql database.
Only tables are accessible from currently selected databases.
USE MITAOE_DB;
INSERT INTO STUDENT_INFO VALUES (‘RAM’. 24. 1979-06-24, 411585);
As DOB is now string due to dash, we need to put inverted commas.
Now execute:
Update STUDENT_INFO SET DOB = ‘1979-05-25’ WHERE name = ‘Gopal’;
SELECT * FROM  STUDENT_INFO;
DROP TABLE STUDENT_INFO;
DROP DATABASE MITAOE_DB;
SELECT * FROM DB WHERE RNO = 1 AND RNO = 5;
Now, put wrong  values in format
***  YYYY-MM-DD ⇒ Requires proper format
***  Specifying no limit to integer can result in generation of garbage value.
Select * from STUDENT_INFO where rno > 10;
                                                         	where 10 < rno < 16;
                                                         	where rno > 10 or rno < 16;
