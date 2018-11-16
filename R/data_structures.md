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
