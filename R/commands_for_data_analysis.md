## Useful commands for data analysis in R

### Reading data 
To read a **text** file, can use R's standard Utils package:
```r
df <- read.table(".txt", header = TRUE)
```

To read a **csv** file:
```r
df <- read.csv("", header = =TRUE, quote=""", stringAsFactors = TRUE, strip.white = TRUE)
```

To read an **excel** file, can use the [readxl](https://readxl.tidyverse.org/) package:
```r
df <- read_excel("spreadsheet.xlsx", sheet = "data")
```

To read an **SPSS** file, can use the [haven](https://www.rdocumentation.org/packages/haven/versions/1.1.2) package: 
```r
df <- read_sav("datafile.sav")
```

### Plotting data with ggplot
```r
ggplot(data = <DATA>) + 
  <GEOM_FUNCTION>(mapping = aes(<MAPPINGS>))
```
Notes: 
- DATA is your dataframe
- GEOM_FUNCTIONs listed [here](https://ggplot2.tidyverse.org/reference/)
- MAPPINGS include ```aes()``` with x and y, more info [here](https://ggplot2.tidyverse.org/reference/aes.html)

Example: Using mpg data, plot points (x,y) with x as `displ` or engine size, y as `hwy` or fuel efficiency
```r
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy))
```
