## Supervised Learning in R


#### Random Notes:
`%>%`:
- passes the left hand side of the opeartor to the first argument of the right hand side of the operator
- Often `%>%` is called multiple times to chain functions together (accomplishes same result as nesting)
- for example, `iris %>% head()` is equivalent to  `head(iris)`

- `select()`: keeps only the variables you mention
- `rename()`: keeps all variables 
- `lm()`: linear model function, can be used to create a simple regression model
```r
lm(formula, data, subset, weights, na.action,
   method = "qr", model = TRUE, x = FALSE, y = FALSE, qr = TRUE,
   singular.ok = TRUE, contrasts = NULL, offset, …)
```
- the formula describes the model, for example `lm(MPG ~ ., data=data)` indicates that MPG is explained by all predictors (denoted as `.`) in the R formula input to `lm()`
- An expression in the form `y ~ model` is inerpreted as a model consists of a series of terms separated by `+` operators. 

- `createDataPartition()`: function that can be used to create balanced splits of the data; from the `caret` package
```r
library(caret)
set.seed(3456)
trainIndex <- createDataPartition(iris$Species, p=.8, list = FALSE, times = 1)
irisTrain <- iris[trainIndex, ]
iristest <- iris[-trainIndex,]
```

- `trainControl(method = 'none')`: turns off all resampling and just trains the model on all the data
