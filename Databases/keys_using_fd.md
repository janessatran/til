## Using Functional Dependencies to Find Keys 
- Create a chart of items that appear on the left-hand, middle, or right-hand side of the functional dependency. 
- If an attribute only occurs on the left-hand side, it must be part of the key
- If an attribute only occurs on the right-hand side, it is not a part of any key
- Find the closure of the left-hand side items
  - If the closure includes all attributes, it is the primary key
  - If not, add in the middle attributes one at a time and find the closure. Check if it includes all attributes. 
  
### Example
Given ```R(A,B,C,D)``` and FDs ```AB -> C, C -> B, C -> D```, find the keys.

| Left | Middle | Right |
|:------:|:--------:|:-------:|
|  A   |  B, C  |   D   |  

Check ```A+ = {A}``` from reflexivity, doesnt include all attributes, not primary key.
Check ```AB+ = {ABCD}```, includes all attributes- primary key! 

If all the attributes end up in the middle, we have to find the closure of diff. permutations of those keys and check which includes all attributes in relation. 
