HW01-Titanic exploration
================
Frederike Basedow
14 September, 2018

Load packages and data
----------------------

In this homework I will explore the `Titanic` data set. This data set is included in RStudio and contains data on the survival of passengers on the Titanic.

First I will load some packages that I would like to use:

``` r
library(tidyverse)
library(knitr)
```

Now, let's have a look at the data set!

``` r
# Have a look at the structure of the data
str(Titanic)
```

    ##  table [1:4, 1:2, 1:2, 1:2] 0 0 35 0 0 0 17 0 118 154 ...
    ##  - attr(*, "dimnames")=List of 4
    ##   ..$ Class   : chr [1:4] "1st" "2nd" "3rd" "Crew"
    ##   ..$ Sex     : chr [1:2] "Male" "Female"
    ##   ..$ Age     : chr [1:2] "Child" "Adult"
    ##   ..$ Survived: chr [1:2] "No" "Yes"

``` r
kable(head(Titanic))
```

|    x|
|----:|
|    0|
|    0|
|   35|
|    0|
|    0|
|    0|

Titanic is a table, trying to get an overview with the function `head()` doesn't give as any valuable information. Let's change it to a data frame for better handling.

``` r
# Change Titanic to data frame
Titanic_df <- data.frame(Titanic)

# Have a look at new structure
str(Titanic_df)
```

    ## 'data.frame':    32 obs. of  5 variables:
    ##  $ Class   : Factor w/ 4 levels "1st","2nd","3rd",..: 1 2 3 4 1 2 3 4 1 2 ...
    ##  $ Sex     : Factor w/ 2 levels "Male","Female": 1 1 1 1 2 2 2 2 1 1 ...
    ##  $ Age     : Factor w/ 2 levels "Child","Adult": 1 1 1 1 1 1 1 1 2 2 ...
    ##  $ Survived: Factor w/ 2 levels "No","Yes": 1 1 1 1 1 1 1 1 1 1 ...
    ##  $ Freq    : num  0 0 35 0 0 0 17 0 118 154 ...

``` r
# Look at first few rows of new data frame
kable(head(Titanic_df))
```

| Class | Sex    | Age   | Survived |  Freq|
|:------|:-------|:------|:---------|-----:|
| 1st   | Male   | Child | No       |     0|
| 2nd   | Male   | Child | No       |     0|
| 3rd   | Male   | Child | No       |    35|
| Crew  | Male   | Child | No       |     0|
| 1st   | Female | Child | No       |     0|
| 2nd   | Female | Child | No       |     0|

Now it is easier to get an idea of the data set's contents. Let's have a closer look at the details.

``` r
# How many rows does the data set have? This tells us how many different categories of passengers there are.
n_pass_cat <- nrow(Titanic_df)

# How many coumns does the data set have? This tells us how many different variables there are.
n_var <- ncol(Titanic_df)
```

The Titanic data set has 32 different passenger categories and 5 different variables.

It would be interesting to know how many passengers were on the Titanic and how many of them survived.

``` r
# Calculate the number of passengers. We can do this by adding up all numbers in the category "Freq".
n_pass <- sum(Titanic_df$Freq)

# Calculate how many passengers survived.
n_surv <- sum(filter(Titanic_df, Survived == "Yes")$Freq)

# Calculate the percentage of survived passengers
perc_surv <- round(n_surv/n_pass*100)
```

There were 2201 passengers on the Titanic and 32% of them survived.
