
## Indexes and Transactions

### Indexes
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

### Transactions
Motivated by two independent requirements:
- concurrent database access
- resilience to system failures
![alt text](https://github.com/janessatran/til/blob/master/Databases/img/database%20structure.PNG "db")
