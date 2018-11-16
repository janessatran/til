## Data Structures in R
### Factors
- **factors**: data objects which are used to categorize the data and store it as levels
- can store both strings and integers
- useful for columns which have a limited number of unique values (e.g. "Male", "Female" or 1, 2, 3)
- the function ```factor()``` with a vector input is used to create a factor 

Example:
```r
# Create vector as input
data <- c("Male", "Female", "Female", "Male")
print(data)
print(is.factor(data))

# Apply factor function
factor_data <- factor(data)
print(factor_data)
print(is.factor(factor_data))
```

results in:
```r
[1] "Male", "Female", "Female", "Male"
[1] FALSE
[1] Male Female Female Male
Levels: Male Female
[1] TRUE
```

#### Other notes about factors:
- R treats text columns in dataframes as categorical data and factors it automatically
- the order of levels can be changed by applying the factor function again with the new order of the levels

Example:
```r
# Create vector as input, Create factors
data <- c("Male", "Female", "Female", "Male")
factor_data <- factor(data)
print(factor_data)

# Apply factor function with required order of level
new_order_data <- factor(factor_data, levels = c("Female", "Male"))
print(new_order_data)
```

results in:
```r
[1] Male Female Female Male
Levels: Male Female
[1] Male Female Female Male
Levels: Female Male
```
#### Generating Factor Levels
- we can generate factor levels using the function ```gl(n, k, labels)``` which takes two integers as input, indicating how many levels and how many times each level
  - **n**: integer giving number of levels
  - **k**: integer giving number of replications
  - **labels**: vector of labels for resulting factor levels
  
Example:
```r
x <- gl(3, 2, labels = c("Red", "Orange", "Yellow"))
print(x)
```

results in :
```r
[1] Red Red Orange Orange Yellow Yellow
Levels: Red Orange Yellow
```
