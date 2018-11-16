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

```sql
Create Trigger name
Before | After | Instead of events
[referencing-variables]
[for each row]
when (condition)
action
```
