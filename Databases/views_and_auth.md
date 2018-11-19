## Views
- three level vision of database -> physical, conceptual, logical
- why use views?
  - hide some data from users
  - make some queries easier / more natural
  - modularity of database access
  
### Defining and using views
- View ```V = ViewQuery(R1, R2, ..., Rn)```

```sql
CREATE VIEW vName AS <Query>
```
example:
```sql
create view CSaccept as 
select sID, cName
from Apply
where major = 'CS' and decision = 'Y';
```

### Querying views
- once V defined, can reference V like any table
- queries invovling V rewritten to use base tables

### Modifying views
- modifications to view V, rewritten to modify base tables

two options to modify base tables:
- rewriting process specified explicitly by view creator
  - can handle all modifcations
  - no gaurantee of correctness (or meaningful)
- restrict views + modifications so that translation to base table modification is meaningful and unambiguous
  - no user intervention
  - restrictions are significant
  
#### Modifying views using triggers
-  using special ```INSTEAD OF``` triggers
  
```sql
CREATE TRIGGER triggerName
INSTEAD OF [modification] ON [view]
FOR EACH ROW
BEGIN
  [modification statement on basetable];
END;
  ```
#### Automatic view modifications
Restrictions in SQL standard for "updatable views"
1. ```SELECT``` (no DISTINCT) on single table T
2. Attributes not in view can be NULL or have default values
3. Subqueries must not refer to T
4. No ```GROUP BY``` or aggregation

- can use ```with check option```; when the system automatically performs a translation, it actually checks to make sure that the translation properly inserted the data into the view
```sql
create view CSaccept as 
select sID, cName
from Apply
where major = 'CS' and decision = 'Y'
with check option;
```

#### Materialized views
- In computing, a materialized view is a database object that contains the results of a query. For example, it may be a local copy of data located remotely, or may be a subset of the rows and/or columns of a table or join result, or may be a summary using an aggregate function.

```sql
Create Materialized View CA-CS As
Select C.cName, S.sName
From College C, Student S, Apply A
Where C.cName = A.cName and S.sID = A.sID
And C.state = 'Ca' and A.major = 'CS'
```
- modifications to base data invalidate view (inserts, deletes, updates)

Efficiency benefits of a materialized view depend on:
- size of data
- complexity of view
- number of queries using view
- number of modifications affecting view
  - "incremental maintenance" vs full recomputation
  
### Updating views
In order to be updatable according to the SQL standard, a view must:

1. Have only one table T in its top-level FROM clause
2. Not use SELECT DISTINCT in its top-level FROM clause
3. Include all attributes from T that do not permit NULLs
4. Not refer to T in subqueries
5. Not use GROUP BY or aggregation
  
## Authorization 
- make sure users see only data they're supposed to see
- guard database against modifications by malicious users
- users have privileges; can only operate on data for which they are authorized
  - READ, WRITE, DELETE privleges
- can authorize privleges on tables and views
  - Note: all views are not updatabale, including views with aggregations

### Obtaining privleges
- relation creator is owner
- owner has all privleges and may grant privileges

```sql
GRANT pivs ON R TO users
[ with grant option]

REVOKE privs ON R FROM users
[ CASCADE | RESTRICT ]
```

- **cascade**: also revoke privleges granted from privileges being revoked (transitively), unless also granted from another source
- **restrict**: disallow if cascade would revoke any other privileges
