## Relational Operators
- equality of types is checked by ```== ```
- inequality of types is checked by ```!=```
- ```> and <``` used to check greater than and less than
  - for strings, will use alphabetical order to check condition
- ```>= and <=``` used to check greater than or equal to, less than or equal to
- can compare vectors using relational operators
  - compares across every element in vector and returns TRUE or FALSE
  
Things to keep in mind:
- R is case sensitive so ```"useR" == "user"``` is ```FALSE```
- ```TRUE``` equates to 1 and ```FALSE``` equates to 0

## Logical Operators
- `&` for "and"
- `|` for "or"
- `!` for "not"

Note: there is a difference between `&` and `&&` as well as `|` and `||` when using the operators on vectors
- `&&` evaluates only the first value in each vector

example:
```r
> c(TRUE, TRUE, FALSE) & c(TRUE, FALSE, FALSE)
[1] TRUE FALSE FALSE

> c(TRUE, TRUE, FALSE) && c(TRUE, FALSE, FALSE)
[1] TRUE

> c(TRUE, TRUE, FALSE) | c(TRUE, FALSE, FALSE)
[1] TRUE TRUE FALSE

> c(TRUE, TRUE, FALSE) || c(TRUE, FALSE, FALSE)
[1] TRUE
```
