## Relational Design Theory

### Design "anomalies" 
Anomalies are inconvenient or error-prone situations arising when we process tables in a databse.                                                                                                
- **insert anomaly**: occurs when certain attributes in the database can't be inserted without the existence of other attributes.
- **update anomaly**: exists when one or more instances of duplicated data is updated, but not all.
- **delete anomaly**: exists when certain attributes are lost because of the deletion of other attributes.

### Functional Dependencies
- generalization of the notion of keys
  - can be used to reason about queries (for optimization) and data storage (compression)
- functional dependency is a relationship that exists when one attribute uniquely determines another attribute.
  - If R is a relation with attributes X and Y, a functional dependency between the attributes is represented as X->Y, which specifies Y is functionally dependent on X                    
  - If all attributes are determined by A, then A is the **primary key** of the relation

Example: Below, SIN determines Name, Address, and Birthdate. Given SIN, we can determine any of the other attributes within the table.
```
SIN -> Name, Address, Birthdate
```

In the examples below, A is the determinant (left side) and B is the dependent (right side)
- **trivial FD**: ```A --> B``` (attribute B is functionally dependent on attribute A) where B is a subset of A
- **non-trivial FD**: ```A -> B``` where B is not a subset of A
- **completely nontrivial FD**: ```A -> B``` where A never intersects B 

### Rules for FDs
#### Armstrong's Axioms
- **axiom of reflexivity**: If Y is a subset of X, then X determines Y 

![equation](https://latex.codecogs.com/gif.latex?%5Ctext%20if%20%5C%3B%20Y%20%5Csubseteq%20X%2C%20%5Ctext%20then%20%5C%3B%20X%20%5Crightarrow%20Y)

- **axiom of augementation**: if X determines Y, then XZ determines YZ for any Z
  - says that every non-key attribute must be fully dependent on the primary key 

![equation](https://latex.codecogs.com/gif.latex?%5Ctext%20if%20%5C%3B%20X%20%5Crightarrow%20Y%2C%20%5Ctext%20then%20%5C%3B%20XZ%20%5Ctext%20%5C%3B%20for%20%5C%3A%20any%20%5C%3B%20Z)

- **axiom of transitivity**: if X determines Y, and Y determines Z, then X must also determine Z

![equation](https://latex.codecogs.com/gif.latex?%5Ctext%20if%20%5C%3B%20X%20%5Crightarrow%20Y%20%5C%3B%20%5Ctext%20and%20%5C%3B%20Y%20%5Crightarrow%20Z%2C%20%5C%3B%20%5Ctext%20then%20%5C%3B%20X%20%5Crightarrow%20Z)

#### Additional rules to help
- **Union**: this rule suggests that if two tables ar eseparate, and the primary key is the same, you may want to consider putting them together
- **Decomposition**: reverse of the union rule, if you have a table that appears to contain two entites that are determined by the same Primary Key, consider breaking them up into two tables 

### Boyce-Codd Normal Form
AKA "good" relations..

If a relational schema is in BCNF, then all redudancy based on FD has been removed, although other types of redundancy may still exist. A relational schema R is in Boyce-Codd Normal form if and if only for every one of its dependencies ```X -> Y```, at least one of the following conditions hold:
```
 X -> Y is a trivial functional dependency (Y subset of X)
    X is a superkey for schema R (left hand side of functional dependency is a key) 
```
Ask: Does every functional dependency have a key on the left-hand side? 

#### BCNF decomposition algorithm
Input: relation R + FDs for R
Output: decomposition of R into BCNF relations with "lossless join"
- Compute keys for R
- Repeat until all relations are in BCNF:
  - Pick any R' with ```A -> B``` that violates BCNF (no primary key on left hand side)
  - Decompose R' into ```R1(A, B) and R2(A, rest)```
  - Compute FDs for R1 and R2 (implied functional dependencies using closure)
  - Copmute keys for R1 and R2

### Multivalued Dependencies and Fourth Normal Form
- multi-valued dependencies lead to unnecessary repetition of data and other anomalies
- A table is in fourth normal form (4NF), if and only if for every one of its non-trivial multivalued dependencies ```X -> Y```, X is a superkey, that is, X is either a candidate key or a supserset thereof. 

How to know if there is a multi-valued dependency: 
1. For a dependency ```A -> B```, if for a single value of A, multipel values of B exists, then the table may have multi-valued dependency
2. Also, a table should at least 3 columns for it to have a multi-valued dependency
3. And, for a relation ```R(A,B,C)```, if there is a multi-valued dependency between A and B, then B and C should be indpendent of each other.
If all these conditions are true for any relation (table), it is said to have multi-valued dependency.

#### 4NF decomposition algorithm
Relation R with MVDs is in 4NF if: 
- for each nontrivial ```A ->-> B```, A is a key

Input: relation R + FDs for R + MVDs for R
Output: Decomposition of R into 4NF relations with "lossless join"
- Compute keys for R
- Repeat until all relations are in 4NF:
  - Pick any R' with ```A ->-> B``` that violates 4NF
  - Decompose R' into ```R1(A, B) and R2(A, rest)```
  - Compute FDs and MVDs for R1 and R2 (implied functional dependencies using closure)
  - Copmute keys for R1 and R20
  
Fourth normal form is a stronger property than BCNF
