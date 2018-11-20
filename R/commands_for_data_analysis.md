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

