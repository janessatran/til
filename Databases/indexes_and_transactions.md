
## Indexes and Transactions
## Indexes
- **indexes/indices**: primary mechanism to get improved performance on database
  - utility in the difference between full table scans and immediate location of tuples (orders of magnitude performance difference)
  - underlying data structures: 
    - **balanced trees (B trees, B+ trees)**: can be used to compare ```attribute = value``` or ```<, >, <=, >=``` etc
      - more flexible, but logarithmic in runtime
    - **hash tables**: can only be used for equailty conditions ```attribute = value```
      - less flexible, but constant runtime
- many DBMS build indices automatiaclly on primary keys or unique keys

#### Downsides of Indexes
1. Extra space (persistent data structures that reside with data)
2. Index creation (when adding to database)
3. Index maintainence (when modifying database) 

#### Picking which indexes to create
Benefit of an index depends on:
- size of table (possibly layout)
- data distributions
- query vs update load 

Physical design advisors:
- input: database (statistics, that describes size and data distribution) and workload
- output: recommended indexes
- query optimizer: takes query, statistics on database, and set of indexes that currently exist and explore best estimated execution plan with estimated cost

#### SQL Standard for creating indexes:
- all indexes are given names
- can create on single attribute or multiple attributes together
- can enforce uniqueness constraint 
- can drop indexes

```sql
CREATE INDEX IndexName ON T(A)
CREATE INDEX IndexName ON T(A1, A2, ..., An)
CREATE UNIQUE INDEX IndexName on T(A)
DROP INDEX IndexName
```

## Transactions
Motivated by two independent requirements:
- concurrent database access
- resilience to system failures

![alt text](https://github.com/janessatran/til/blob/master/Databases/img/database%20structure.PNG "db")

#### Levels of inconsistency with concurrent access: 
Databases use the get -> modify -> put sequence of actions
- **attribute-level**: 2 clients updating attribute with different values, can result in multiple diff. values if there is interleaving 
- **tuple-level**: 2 clients issuing statements that modify diff attribute for same record, if performed interleaved, both changes will or one of the two changes may occur 
- **table-level**: 2 clients submitting statements, one using a table query as a condition at the same time the second client modifies that table
- **multi-statement**: 2 clients, first client moving records from one table to another and deleting first table, second client counting number of rows in tables; second client may be counting duplicates

Concurrency Goal: execute sequence of SQL statements so they appear to be running in isolation 
- solution: execute statements in isolation
- still want to enable concurrency when safe to do so (multiprocessor, multithreaded, asynchronous I/O)
System-Failure Goal: gaurantee all-or-nothing execution, regardless of failures


#### Transactions are a solution for both concurrency and failures. 
- **transaction**: a sequence of one or more SQL operations treated as a unit
  - transactions appear to run in isoloation
  - if the system fails, each transaction's changes are reflected either entirely or not at all
  
#### SQL Standard:
- begins automatically on first SQL statement
- on "commit" transaction ends and new one begins
- current transaction ends on session termination
- "autocommit" turns each statement into transaction

### ACID Properties:
A set of properties you should apply when modifying a database. 
- **atomicity**: all or nothing; you can guarantee that all of a transaction happens or none of it does; when a crash, power failure, error, etc occurs, this allows it so you won't be in a state in which only some of the related changes have happened.
- **consistency**: you guarantee that your data will be consistent, none of the constraints you have on related data will ever be violated.
- **isolation**: one transaction cannot read data from another transaction that is not yet completed. If two transactions are executing concurrently, each one will see the world as if they were executing sequentially, and if one needs to read data that is written by another, it will have to wait unti lthe other is finished.
  - **serializability**: opeartions may be interleaved, but execution must be equivalent to some sequential (serial) order of all transactions 
- **durability**: once a transaction is complete, it is guaranteed that all of the changes have been recorded to a durable medium (such as a hard disk) and the fact that the trasaction has been compelted is likewise recorded; if system crashses after transaction commits, all effects of transaction remain in database. Protocols based on the property of "logging" used to ensure this. 


- **transaction rollback (abort)**: undoes the partial effects of transaction; can be system or client initiated
```
Begin Transaction;
< get input from user >
SQL commands based on input
< confirm results with user > # not good practice bc may lock database for other users if no confirmation made (or not done in timely manner)
If ans = 'ok' Then Commit; Else Rollback;
```