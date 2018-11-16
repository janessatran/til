
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
  - **serializability**: operations may be interleaved, but execution must be equivalent to some sequential (serial) order of all transactions 
- **durability**: once a transaction is complete, it is guaranteed that all of the changes have been recorded to a durable medium (such as a hard disk) and the fact that the trasaction has been compelted is likewise recorded; if system crashses after transaction commits, all effects of transaction remain in database. Protocols based on the property of "logging" used to ensure this. 


- **transaction rollback (abort)**: undoes the partial effects of transaction; can be system or client initiated
```
Begin Transaction;
< get input from user >
SQL commands based on input
< confirm results with user > # not good practice bc may lock database for other users
                              # if no confirmation made (or not done in timely manner)
If ans = 'ok' Then Commit; Else Rollback;
```
### Isolation Levels
- there are different isolation levels:
- per transaction and "in the eye of the beholder" 
- levels are "read uncommitted", "read committed", "repeatable read"
  - **read uncommitted**: a transaction may perform dirty reads
  - **read committed**: a transaction may not perform dirty reads; still does not guarantee global serializability 
  - **repeatable read**: a transaction nmay not perform dirty reads; an item read multiple times cannot change value
    - **phantom read**: occurs when, in the course of a transaction, two identical queries are executed and the collection of rows returned by the second query is different from the first
    - can occur with inserts into table, because values are not inserted with locks (unlike reads) 
- **dirty data item**: written by an uncommitted transaction 

### EXAMPLES

#### Read Uncommitted
```
Consider a table R(A) containing {(1),(2)}. T1 is "update R set A = 2*A" and T2 is "select avg(A) from R". 
If T2 executes using "read uncommitted", what are the possible values it returns?

ANSWER: 1.5, 2, 2.5, 3
```

**Explanation**: The update command in T1 can update the values in either order, and the select command in T2 can compute the average at any point before, between, or after the updates.

#### Read Committed
```
R(A) = {(1),(2)}, S(B) = {(1),(2)}
T1 -> update R set A = 2*!; update S set B = 2*B
T2 -> select avg(A) from R; select avg(B) from S

If T2 executes "read committed" is it possible for T2 to return two diff values?

ANSWER: Yes
```

**Explanation**: T2 could return avg(A) computed before T1 and avg(B) computed after T1

#### Repeatable Read
```
R(A) = {(1),(2)}
T1 -> update R set A = 2*!; insert into R values (6)
T2 -> select avg(A) from R; select avg(A) from R
If T2 executes using "repeatable read", what are the possible values returned by its SECOND statement?

ANSWER: 1.5, 4
```
**Explanation**: T2 must (appear to) execute entirely before or after T1. You might think T2 could (appear to) execute between T1's two statements since the second statement is an insert, but that would be allowing dirty reads.

### Isolation Levels Summary
![alt text](https://github.com/janessatran/til/blob/master/Databases/img/isolation_levels.PNG)

- standard default: serializable
- weaker isolation levels
  - increased concurrency + decreaesd overhead = increased performance
  - weaker consistency guarantees
  - some systems have default Repeatable Read
