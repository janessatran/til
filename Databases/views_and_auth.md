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
