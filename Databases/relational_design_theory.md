## Relational Design Theory

#### Design "anomalies" 
Anomalies are inconvenient or error-prone situations arising when we process tables in a databse.                                                                                                
- **insert anomal                                                                                                 
- **update anomaly**: exists when one or more instances of duplicated data is updated, but not all.
- **delete anomaly**: exists when certain attributes are lost because of the deletion of other attributes.

#### Functional Dependencies
- generalization of the notion of keys
  - can be used to reason about queries (for optimization) and data storage (compression)
- functional dependency is a relationship that exists when one attribute uniquely determines another attribute.
  - If R is a relation with attributes X and Y, a functional dependency between the attributes is represented as X->Y, which specifies Y is functionally dependent on X                                                                                     
