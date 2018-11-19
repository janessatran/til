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
