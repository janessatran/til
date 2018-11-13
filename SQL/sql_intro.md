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
