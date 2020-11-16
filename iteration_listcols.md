Iteration and listcols
================

## Lists

You can ut anything in a list.

``` r
## concept: lists can store anything.
vec_numeric = 5:8
vec_logical = c(TRUE, TRUE, FALSE, TRUE, FALSE, FALSE)
mat = matrix(1:8, nrow = 2, ncol = 4)
summary = summary(rnorm(100))

##these are all different kinds of lists, different contents and forms
##can't put these in a dataframe but can put in a list

l = list(
  vec_numeric = 5:8,
  vec_logical = c(TRUE, TRUE, FALSE, TRUE, FALSE, FALSE),
  mat = matrix(1:8, nrow = 2, ncol = 4),
  summary = summary(rnorm(100))
)
```

``` r
l
```

    ## $vec_numeric
    ## [1] 5 6 7 8
    ## 
    ## $vec_logical
    ## [1]  TRUE  TRUE FALSE  TRUE FALSE FALSE
    ## 
    ## $mat
    ##      [,1] [,2] [,3] [,4]
    ## [1,]    1    3    5    7
    ## [2,]    2    4    6    8
    ## 
    ## $summary
    ##     Min.  1st Qu.   Median     Mean  3rd Qu.     Max. 
    ## -2.84485 -0.57545  0.09078  0.05604  0.71431  1.61361

``` r
l$vec_numeric
```

    ## [1] 5 6 7 8

``` r
l[[1]]
```

    ## [1] 5 6 7 8

``` r
l[["vec_numeric"]]
```

    ## [1] 5 6 7 8

``` r
l[["vec_numeric"]][1:3]
```

    ## [1] 5 6 7

``` r
mean(l[["vec_numeric"]])
```

    ## [1] 6.5

``` r
## you can do whatevr you normally do to individual elements of a list
```

## `for` loop

Create a new list.

``` r
list_norm = 
  list(
    a = rnorm(20, mean = 3, sd = 1),
    b = rnorm(30, mean = 0, sd = 5),
    c = rnorm(40, mean = 10, sd = .2),
    d = rnorm(20, mean = -3, sd = 1)
  )
```

``` r
list_norm[[1]]
```

    ##  [1] 2.796620 2.977746 3.484485 1.136477 4.096029 2.823071 3.414810 2.718136
    ##  [9] 1.266112 2.830664 3.890631 3.211943 4.601512 2.759416 2.912785 1.434035
    ## [17] 2.110722 1.860735 4.615112 5.102697

``` r
list_norm
```

    ## $a
    ##  [1] 2.796620 2.977746 3.484485 1.136477 4.096029 2.823071 3.414810 2.718136
    ##  [9] 1.266112 2.830664 3.890631 3.211943 4.601512 2.759416 2.912785 1.434035
    ## [17] 2.110722 1.860735 4.615112 5.102697
    ## 
    ## $b
    ##  [1]  -1.4730928  -2.5417414   2.7597602  -0.3889397   0.8809550  -9.9036555
    ##  [7]  -6.1825376  -0.9500518  -8.6376627 -11.4250307   2.3111638  -5.1765572
    ## [13]   3.2504293  -6.6938111   1.0433786   1.9093802  -4.9034491   5.3819857
    ## [19]  -0.4062341   1.3354376   8.7581568   5.6522441  -2.6430193   2.5038216
    ## [25]   7.5395501   2.4417501   1.4184334   8.6587674  12.3639480   1.3821139
    ## 
    ## $c
    ##  [1] 10.139049 10.134839  9.724513  9.917981  9.729033 10.105414  9.649420
    ##  [8]  9.911726 10.081756 10.110784  9.760845 10.139448 10.198033  9.962808
    ## [15]  9.963062 10.004891 10.161258 10.130510  9.861240 10.456053  9.707824
    ## [22]  9.776622 10.114094 10.357570 10.443181 10.145507 10.082519 10.209359
    ## [29] 10.488576 10.019513 10.071050 10.257601  9.925117 10.183095 10.397140
    ## [36]  9.842575  9.731167 10.202099 10.302673 10.276754
    ## 
    ## $d
    ##  [1] -3.3687091 -3.4163289 -2.1184678 -4.3115016 -3.9517647 -2.4246917
    ##  [7] -2.9372014 -3.1550830 -2.5143856 -3.7643284 -3.2696936 -4.2300795
    ## [13] -3.5031807 -2.1864569 -2.1738146 -0.7404777 -4.0114497 -2.0271766
    ## [19] -3.5686064 -3.4360065

Pause and get my old function.

``` r
mean_and_sd = function(x) {
  
  if (!is.numeric(x)) {
    stop("Input must be numeric")
  }
  
  if (length(x) < 3) {
    stop("Input must have at least three numbers")
  }

  mean_x = mean(x)
  sd_x = sd(x)
 
  tibble(
    mean = mean_x,
    sd = sd_x
  )
  
}
```

I can apply that function to each list element.

``` r
list_norm[[1]]
```

    ##  [1] 2.796620 2.977746 3.484485 1.136477 4.096029 2.823071 3.414810 2.718136
    ##  [9] 1.266112 2.830664 3.890631 3.211943 4.601512 2.759416 2.912785 1.434035
    ## [17] 2.110722 1.860735 4.615112 5.102697

``` r
list_norm[[2]]
```

    ##  [1]  -1.4730928  -2.5417414   2.7597602  -0.3889397   0.8809550  -9.9036555
    ##  [7]  -6.1825376  -0.9500518  -8.6376627 -11.4250307   2.3111638  -5.1765572
    ## [13]   3.2504293  -6.6938111   1.0433786   1.9093802  -4.9034491   5.3819857
    ## [19]  -0.4062341   1.3354376   8.7581568   5.6522441  -2.6430193   2.5038216
    ## [25]   7.5395501   2.4417501   1.4184334   8.6587674  12.3639480   1.3821139

``` r
list_norm[[3]]
```

    ##  [1] 10.139049 10.134839  9.724513  9.917981  9.729033 10.105414  9.649420
    ##  [8]  9.911726 10.081756 10.110784  9.760845 10.139448 10.198033  9.962808
    ## [15]  9.963062 10.004891 10.161258 10.130510  9.861240 10.456053  9.707824
    ## [22]  9.776622 10.114094 10.357570 10.443181 10.145507 10.082519 10.209359
    ## [29] 10.488576 10.019513 10.071050 10.257601  9.925117 10.183095 10.397140
    ## [36]  9.842575  9.731167 10.202099 10.302673 10.276754

``` r
list_norm[[4]]
```

    ##  [1] -3.3687091 -3.4163289 -2.1184678 -4.3115016 -3.9517647 -2.4246917
    ##  [7] -2.9372014 -3.1550830 -2.5143856 -3.7643284 -3.2696936 -4.2300795
    ## [13] -3.5031807 -2.1864569 -2.1738146 -0.7404777 -4.0114497 -2.0271766
    ## [19] -3.5686064 -3.4360065

``` r
mean_and_sd(list_norm[[1]])
```

    ## # A tibble: 1 x 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  3.00  1.11

``` r
mean_and_sd(list_norm[[2]])
```

    ## # A tibble: 1 x 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1 0.276  5.64

``` r
mean_and_sd(list_norm[[3]])
```

    ## # A tibble: 1 x 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  10.1 0.222

``` r
mean_and_sd(list_norm[[4]])
```

    ## # A tibble: 1 x 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1 -3.06 0.906

``` r
## so applying a function to each of my list items - that's fine.  With 4 lists, that's ok, but if 40 lists, more tedious. so, let's use a for loop.
```

Let’s use a for loop:

``` r
output = vector("list", length = 4)

for (i in 1:4) {
  
  output[[i]] = mean_and_sd(list_norm[[i]])

}
```

## Let’s try map\!

Instead of saying input list and output list and then do the procedure,
the idea behind map is …

``` r
output = map(list_norm, mean_and_sd)
## doing same thing and even saving the list now
```

what if you want a different function..?

``` r
output = map(list_norm, median)
output = map(list_norm, IQR)
## you can map any function you want across this input list
## this is a function within a function, whatever you want
```
