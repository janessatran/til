## Constraints and Triggers
- **constraints**: aka integrity, constrain allowable database states
- **triggers**: monitor dabase change,s check conditions and initate actions

## Integrity Constraints
- restrictions on allowable data, beyond those imposed by structure and types (when defining schema) 
- used to catch data-entry errors, create critera for correctness when updating database, to enforce consistency, tell system about data 

Examples:
- 4.0 >= GPA >= 0.0
- decision: ("Y", "N", "NULL")
- if major == "CS", then decision == "NULL"

### Classification of constraints
- **Non-null**: values can't take on ```NULL```
- **Key**: uniquely identifies each record in a database table
- **Referential integrity**: foreign key constraint; states that the table relationships must always be consistent; in other words, any foreign key field must agree with the primary key that is referenced by the foreign key
- **Attribute-based**: specified along with attribute, constraining value of attribute
- **Tuple-based**: constrains how values in tuples relate to each other
- **General assertions**: a predicate expressing a condition we wish the database to always satisfy 

### Declaring and enforcing constraints
#### Declaration
- with original schema; checked after bulk loading
- or later; checked on current state of database at time of declaration 
#### Enforcement
- check after every "dangerous" modification or transaction (grouping of modifications) 
- deferred constraint checking 

### Constraint examples
#### Attribute-based:
```sql
-- not null constraint placed on GPA
create table Student(sID int, sName text, GPA real not null, sizeHS int);

-- primary key constraint on sID, only one can be primary
-- but multiple attributes can have the "unique" constraint applied
create table Student(sID primary key int, sName text, GPA real, sizeHS int);

-- can have keys than span attributes (as a tuple) 
create table College(cName text, state text, enrollment int, primary key (cName, state));
```

#### Tuple-based constraint: 
Uses the `check()` function
```sql
create table Apply(sID int, cName text, major text, decision text,
                    check(decision = 'N' or cname <> 'Stanford' or major <> 'CS'));
                    
create table Student(sID int, sName text, GPA real check(GPA is not null), sizeHS int);
```

#### Referential-integrity constraint:
```sql

create table Apply(sID int, cName text, major text, decision text, 
                    check(sID in (select sID from Student)));
```
#### Notes
- integrity of references; no "dangling pointers" 
- referential integrity from R(A) to S(B) -> each value in column A of table R must appear in column B of table S
- A is called the "foregin key" 
- B is usually required to be the primary key for table S

Modifying tables with referential integrity constraints:
- Delete from S
  - Resterict (default): throws an error and doesn't allow modification
  - SET NULL: if tuple deleted in reference table, take referencing tuples and replace values with NULL
  - Cascade: if tupled deleted, delete any other tuple with referencing value
- Update S.B
  - Resterict (default): throws an error and doesn't allow modification
  - SET NULL: if tuple updated in reference table, take referencing tuples and replace values with NULL
  - Cascade: if tupled updated, update any other tuple with referencing value
  
#### General Assertions
Can refer to any number of tables in the database, not table specific. 
```sql
create assertion Key
check ((select count(distinct A) from T) = (select count(*) from T)));
```

Note:
- diff between `unique` and `primary key`: The UNIQUE constraint uniquely identifies each record in a database table. The UNIQUE and PRIMARY KEY constraints both provide a guarantee for uniqueness for a column or set of columns. ... Primary key can't be null but unique constraint is nullable

## Triggers
"Event-Condition-Action Rules"
- when some event occurs, check condition; if true, do action 
- use them to move logic from applications into the database itself
- use them to enforce constraints (because constraints are more limited than triggers -> triggers more expressive)
- use them to have constraint "repair" logic -> trigger can detect if constraint is violated and then fix it

Examples: 
- if enrollment > 35,000 -> reject all applications 
- if insert application with GPA > 3.95 -> accept application 
- update size HS to be > 7,000 -> change

SQL Standard syntax
```sql
Create Trigger name
Before | After | Instead of events
[referencing-variables]
[for each row]
when (condition)
action

-- Events:
insert on T
delete on T
update on T

-- Referencing variables: 
old row as var
new row as var
old table as var
new table as var
```

Example:
- implement referential integrity 
- R.A references S.B, cascaded delete

Row level:
```sql
Create Trigger Cascade
After Delete On S
Referencing Old Row as O
For Each Row
[ no condition ]
Delete From R Where A = O.B
```

Statement level:
```sql
Create Trigger Cascade
After Delete On S
Referencing Old Table as OT
[ For Each Row ]
[ no condition ]
Delete From R Where A in (Select B From OT)
```

Tricky Issues:
- row level vs statement level
  - new/old row and new/old table
  - before, instead of
- multiple triggers activated at same time (which goes first?)
- trigger actions activating other triggers (chaining)
  - also self-triggering, cycles, nested invocations
- conditions in when vs as part of action 
