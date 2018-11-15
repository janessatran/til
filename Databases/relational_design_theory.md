## Relational Design Theory

#### Design "anomalies" 
Anomalies are inconvenient or error-prone situations arising when we process tables in a databse.                                                                                                
- **insert anomaly**: occurs when certain attributes in the database can't be inserted without the existence of other attributes.
- **update anomaly**: exists when one or more instances of duplicated data is updated, but not all.
- **delete anomaly**: exists when certain attributes are lost because of the deletion of other attributes.

#### Functional Dependencies
- generalization of the notion of keys
  - can be used to reason about queries (for optimization) and data storage (compression)
- functional dependency is a relationship that exists when one attribute uniquely determines another attribute.
  - If R is a relation with attributes X and Y, a functional dependency between the attributes is represented as X->Y, which specifies Y is functionally dependent on X                                                                                     

Example: Below, SIN determines Name, Address, and Birthdate. Given SIN, we can determine any of the other attributes within the table.
```
SIN -> Name, Address, Birthdate
```

In the examples below, A is the determinant (left side) and B is the dependent (right side)
- **trivial FD**: ```A --> B``` (attribute B is functionally dependent on attribute A) where B is a subset of A
- **non-trivial FD**: ```A -> B``` where B is not a subset of A
- **completely nontrivial FD**: ```A -> B``` where A never intersects B 

#### Rules for FDs
- **axiom of reflexivity**: If Y is a subset of X, then X determines Y 
![equation](https://latex.codecogs.com/gif.latex?%5Ctext%20if%20%5C%3B%20Y%20%5Csubseteq%20X%2C%20%5Ctext%20then%20%5C%3B%20X%20%5Crightarrow%20Y)
