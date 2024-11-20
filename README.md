# Aggregate-functions-group-by-having-clause

## AIM:
 To study and implement aggregate functions, group by and having clause with suitable examples.
 
 ## THEORY:
 An aggregate function is a function that performs a calculation on a set of values, and returns a single
 value.
 Aggregate functions are often used with the GROUP BY clause of the SELECT statement. The
 GROUP BY clause splits the result-set into groups of values and the aggregate function can be used to
 return a single value for each group.
 ```
 The most commonly used SQL aggregate functions are:
 ● MIN()-returns the smallest value within the selected column
 Syntax:
 SELECT MIN(column_name)
 FROM table_name
 WHERE condition;
 Example: SELECT MIN (Sal) FROM emp;
 ● MAX()-returns the largest value within the selected column
 Syntax:
 SELECT MAX(column_name)
 FROM table_name
 WHERE condition;
 Example: SELECT MAX (Sal) FROM emp;
 ● COUNT()-returns the number of rows in a set
 Syntax:
 SELECT COUNT(column_name)
 FROM table_name
 WHERE condition;
 Example: SELECT COUNT (Sal) FROM emp;
 ● SUM()-returns the total sum of a numerical column
 Syntax:
 SELECT SUM(column_name)
 FROM table_name
 WHERE condition;
 Example: SELECT SUM (Sal) From emp;
 ● AVG()-returns the average value of a numerical column
 Syntax:
 SELECT AVG(column_name)
 FROM table_name
 WHERE condition;
 Example: Select AVG (10, 15, 30) FROM DUAL;
 GROUPBY:
 This query is used to group all the records in a relation together for each and every value of a specific
 key(s) and then display them for a selected set of fields in the relation.
 Syntax:
 SELECT column_name(s)
 FROM table_name
 WHERE condition
 GROUP BY column_name(s)
 ORDER BY column_name(s);
 Example: SQL> SELECT EMPNO,SUM (SALARY)FROMEMPGROUPBYEMPNO;
 GROUPBY-HAVING:
 The HAVING clause was added to SQL because the WHERE keyword could not be used with
 aggregate functions. The HAVING clause must follow the GROUP BY clause in a query and must also
 precede the ORDER BY clause if used.
 Syntax:
 SELECT column_name(s)
 FROM table_name
 WHERE condition
 GROUP BY column_name(s)
 HAVING condition
 ORDER BY column_name(s);
```
```
Question 1:
 What is the total number of appointments scheduled by each doctor?

Answer:
 SELECT DoctorID,count(AppointmentDateTime) AS TotalAppointments
 FROMAppointments GROUP BY DoctorID;
```
## Output:
![Screenshot 2024-11-20 141210](https://github.com/user-attachments/assets/75d4ac9f-dbf4-4986-93bb-7992130dcd10)

```
Question 2:
 Howmanyprescriptions were written by each doctor?

Answer:
 SELECT DoctorID,count(Medication) AS TotalPrescriptions
 FROMPrescriptions GROUP BY PatientID;
```
## Output:
![Screenshot 2024-11-20 141230](https://github.com/user-attachments/assets/cd8061bb-f4ce-4670-bf36-3d4c790182e9)

```
Question 3:
 Howmanypatients are there in each age group category (e.g., under 20, 20-30, 30-40, etc.)?

Answer:
 SELECT
 CASE
  WHENage<20THEN'Under 20'
  WHENageBETWEEN20AND30THEN'20-30'
  WHENageBETWEEN31AND40THEN'31-40'
  WHENageBETWEEN41AND50THEN'41-50'
 ELSE 'Above 50'
 ENDASAgeGroup,
 COUNT(*) AS TotalPatients
 FROM(
 SELECT (2024-DateofBirth) AS age
 FROMpatients
 ) AS AgeData
 GROUPBYAgeGroup
 ORDERBY
 CASE
 WHENAgeGroup ='Under 20' THEN 1
 WHENAgeGroup ='20-30' THEN 2
 WHENAgeGroup ='31-40' THEN 3
 WHENAgeGroup ='41-50' THEN 4
 ELSE 5
 END;
```
## Output:
![Screenshot 2024-11-20 141237](https://github.com/user-attachments/assets/76e84fda-ca8f-42b5-9376-85c0e9deff7f)

```
Question 4:
 Write a SQL query to find the shortest email address in the customer table?

Answer:
 SELECT name,email,min(length(email)) AS min_email_length
 FROMcustomer;
```
## Output:
![Screenshot 2024-11-20 141242](https://github.com/user-attachments/assets/32b0b105-9b98-421d-a7b0-93536c73fb77)

```
Question 5:
 Write a SQL query to find the minimum purchase amount.

Answer:
 SELECT MIN(purch_amt) AS MINIMUM
 FROM orders;
```
## Output:
![Screenshot 2024-11-20 141250](https://github.com/user-attachments/assets/9ec0f773-e9ec-40e2-8a45-db9843428187)

```
Question 6:
 Write a SQL query to Calculate the average email length (in characters) for people who lives in Mumbai 
 city
Answer:
 SELECT AVG(LENGTH(email)) AS avg_email_length_below_30
 FROMcustomer
 WHEREc ity='Mumbai';
```
## Output:
![Screenshot 2024-11-20 141255](https://github.com/user-attachments/assets/81e83a4e-ffce-4761-bafa-03d3b6377f21)

```
Question 7:
 Write a SQL query to find the average length of names for people living in Chennai?

Answer:
 SELECT AVG(LENGTH(name)) AS avg_name_length
 FROMcustomer
 WHERE city='Chennai';
```
## Output:
![Screenshot 2024-11-20 141259](https://github.com/user-attachments/assets/7193d58d-5014-45a8-b21c-64711133d2bf)

```
Question 8:
 Write the SQL query that accomplishes the grouping of data by addresses, calculates the sum of salaries for each address, and excludes addresses where the total salary sum is not greater than 2000.
Answer:
 SELECT address,SUM(salary)
 FROMcustomer1
 GROUPBYaddress
 HAVING SUM(salary)>2000;
```
## Output:
![Screenshot 2024-11-20 141307](https://github.com/user-attachments/assets/f12e3357-1339-4a91-b58d-54286d6541d5)

```
Question 9:
 Write the SQL query that achieves the grouping of data by age, calculates the minimum income for each age
 group, and includes only those age groups where the minimum income is less than 400,000.

Answer:
 SELECT age,MIN(income)
 FROM employee
 GROUPBY age
 HAVING MIN(income)<400000;
```
## Outut
![Screenshot 2024-11-20 141313](https://github.com/user-attachments/assets/501d39c9-351a-4ab2-824e-7c255c0a5edc)

```
Question 10:
 Write the SQL query that accomplishes the grouping of data by joining date (jdate), calculates the total work hours for each date, and excludes dates where the total work hour sum is not greater than 40.

Answer:
 SELECT jdate,SUM(workhour)
 FROMemployee1
 GROUPBYjdate
 HAVING SUM(workhour)>40;
```
## Output:
![Screenshot 2024-11-20 141319](https://github.com/user-attachments/assets/3aaa75d8-6237-4bca-9e93-fe0351e12e0c)
