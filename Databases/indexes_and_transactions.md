## Indexes and Transactions
- **indexes/indices**: primary mechanism to get improved performance on database
  - utility in the difference between full table scans and immediate location of tuples (orders of magnitude performance difference)
  - underlying data structures: 
    - **balanced trees (B trees, B+ trees)**: can be used to compare ```attribute = value``` or ```<, >, <=, >=``` etc
      - more flexible, but logarithmic in runtime
    - **hash tables**: can only be used for equailty conditions ```attribute = value```
      - less flexible, but constant runtime
      
