### Structured Query Language
- **data definition language (DDL)**: create table, drop table, etc
- **data maniulation language (DML)**: select, insert, delete, update 
- **other commands**: indexes, constraints, views, triggers, transactions, authorization, etc 

#### The Basic SELECT Statement
```sql 
Select A1, A2
FROM R1
WHERE condition
```
Note: can apply join condition in where clause (R1.id = R2.id) 

#### Set Operators
- **UNION**: used to join to tables/relations; by default eliminiates duplicates in result
- **UNION ALL**: used to join to tables/relations; multi-set operator, does not delete duplicates and sort
- **INTERSECT**: used to combine two select statements, but returns rows only from first select statement that are indentical to row in the second select statement
- **EXCEPT**: returns all records from first select statement that are not in the second select statement

#### Subqueries in WHERE Clause
```sql
SELECT ID, Name
FROM Table1
WHERE ID in (SELECT ID FROM Table2 WHERE Name like 'Ja%');
```
##### ANY and ALL Operators
- used with a WHERE or HAVING clause
- ANY returns true if one or more of the subquery values meet the condition
- ALL returns true if all the subquery values meet the condition

```sql
SELECT c1
FROM t1
WHERE c1 = ANY (SELECT c2 FROM t2 WHERE condition);
```

#### Subqueries in FROM and SELECT 
- aka "nested" select statement
- can use to refer to subquery as table in a from clause
Example: Finding colleges and their highest GPA applicants
```sql
SELECT distinct College.cName, state, GPA
FROM College, Apply, Student
WHERE College.cName = Apply.cName
  and Apply.sID = Student.sID
  and GPA >= all 
              (select GPA from Student, Apply
               where Student.sID = Apply.sID
                 and Apply.cName = College.cName);
```
is the same as
```sql
SELECT cName, state,
(SELECT distinct GPA
FROM Apply, Student
WHERE College.cName = Apply.cName
  and Apply.sID = Student.sID
  and GPA >= all 
              (select GPA from Student, Apply
               where Student.sID = Apply.sID
                 and Apply.cName = College.cName)) as GPA
FROM College;
```

#### JOINS
- **INNER JOIN** on condition: cross product that satisifies condition 
- **NATURAL JOIN**: equates columns across tables of the same name 
- **INNER JOIN** (using attrs): like natural join, but explicitly list attributes to be equated
- **LEFT | RIGHT | FULL OUTER JOIN**: similar to cross product on condition, but when results don't meet condition they  are still added to the result and padded with null values. 
  - outer joins are not associate, but full outer join is commutatitve
  
#### Aggregate Functions
- **AVG**: calculates the average of a set of values
- **COUNT**: counts rows in a specified table or view
- **MIN**: gets min value in set of values
- **MAX**: gets max value in set of values
- **SUM**: calculates sum of values
- **HAVING**: used to apply aggregate condition on set; applied after group by clause

