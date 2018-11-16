## Data Structures in R
## Factors
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

### Other notes about factors:
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
### Generating Factor Levels
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
## Data Frames
- **data frame**: table or 2d array-like structure in which each column contains values of one variable and each row contains one set of values from each column

### Characteristics:
- column names sould be non-empty
- row names should be unique
- data stored in df can be of numeric, factor, or character type
- each column should contain same number of dta items

### Creating a dataframe:
```r
test.data <- data.frame(
  test_id = c(1:3),
  test_name = c("Zop", "Mop", "Bop"),
  test_count = c(4, 12, 5),
  test_date = as.Date(c('2014-01-23', '2014-03-11', '2014-05-15'))
  stringAsFactors = FALSE
)
print(test.data)
```
results in:
```r
  test_id    test_name     test_count     test_date
1     1       Zop              4         2014-01-12
2     2       Mop              12        2014-03-11
3     3       Bop              5         2014-05-15
```

### Other df notes:
- to get the structure of the data frame, use ```str()```

```str(test.data)``` results in:
```r
'data.frame': 3 obs. of 4 variables:
 $ test_id    : int  1 2 3
 $ test_name  : chr  "Zop" "Mop" "Bop" ...
 $ test_count    : num  4 12 5
 $ start_date: Date, format: "2014-01-12" "2014-03-11" "2014-05-15" ...
```
- to get statistical summary and nature of data use function ```summary()```
- to extract specific column from df, use column name by calling ```df$column_name```
```r 
# extract name and count
result <- data.frame(test.data$test_name, test.data$test_count)
print(result)
```
results in:
```r
   test.data.test_name   test.data.test_count
1               Zop            4
2               Mop            12
3               Bop            5
```
- to extract specific number of rows and columns, call ```df[row_start_1:row_end, columns]```
  - index for R starts at 1
  - to extract all rows, leave first value blank
  - to extract all columns, leave second value blank
- to add a new column to the data frame, call the dataframe with the new column name and values like ```df$new_col <- c("new_val")```
- to add a new row, we create a second dataframe and merge it with the first dataframe using the ```rbind()``` function such as ```result <- rbind(old_df, new_df)```
