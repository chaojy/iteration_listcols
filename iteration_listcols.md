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
    ## -2.64446 -0.75197  0.00596 -0.03578  0.51465  2.04383

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

    ##  [1] 3.165231 2.430264 2.845420 2.746671 4.632908 1.698360 3.234596 4.716283
    ##  [9] 5.588216 1.905555 5.357418 3.308823 3.064374 2.242463 3.183032 3.065470
    ## [17] 3.823775 2.793408 3.449930 2.822274

``` r
list_norm
```

    ## $a
    ##  [1] 3.165231 2.430264 2.845420 2.746671 4.632908 1.698360 3.234596 4.716283
    ##  [9] 5.588216 1.905555 5.357418 3.308823 3.064374 2.242463 3.183032 3.065470
    ## [17] 3.823775 2.793408 3.449930 2.822274
    ## 
    ## $b
    ##  [1]  -1.0273108  -4.6520136  -4.7100328  -3.1257576  -2.3206759   1.7942328
    ##  [7]  -6.6617379  -1.2954238  -2.0137220  -8.2432422   8.0627530   0.1421405
    ## [13]   3.1783954  -3.4096608   8.6609997  -1.7979736   0.7644718  -9.1008577
    ## [19]   5.0834091  -2.1984694  -5.4412863   3.6036193  -7.4448725 -11.9211365
    ## [25]   5.1603929  -4.7410261   6.2392831  -0.5675471   3.1286714   9.6010483
    ## 
    ## $c
    ##  [1]  9.867020 10.429457 10.273375 10.250991 10.258240 10.162421 10.179986
    ##  [8] 10.012653 10.020572  9.744698 10.356048 10.229940 10.097227 10.165594
    ## [15]  9.590347 10.306782 10.237168 10.377565 10.237674  9.976944  9.700159
    ## [22]  9.933553 10.251139  9.506537  9.563587  9.794636  9.942226  9.724984
    ## [29] 10.149739 10.030909  9.981973  9.786148 10.083372  9.759187  9.770845
    ## [36] 10.300163  9.834468  9.792100 10.254420 10.056874
    ## 
    ## $d
    ##  [1] -1.775992 -3.517999 -1.889596 -3.720322 -4.180576 -2.825448 -2.467010
    ##  [8] -4.000895 -2.462634 -3.602608 -3.390259 -3.385608 -2.658832 -3.615186
    ## [15] -2.853783 -1.848820 -2.238918 -3.114111 -2.036296 -3.868798

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

    ##  [1] 3.165231 2.430264 2.845420 2.746671 4.632908 1.698360 3.234596 4.716283
    ##  [9] 5.588216 1.905555 5.357418 3.308823 3.064374 2.242463 3.183032 3.065470
    ## [17] 3.823775 2.793408 3.449930 2.822274

``` r
list_norm[[2]]
```

    ##  [1]  -1.0273108  -4.6520136  -4.7100328  -3.1257576  -2.3206759   1.7942328
    ##  [7]  -6.6617379  -1.2954238  -2.0137220  -8.2432422   8.0627530   0.1421405
    ## [13]   3.1783954  -3.4096608   8.6609997  -1.7979736   0.7644718  -9.1008577
    ## [19]   5.0834091  -2.1984694  -5.4412863   3.6036193  -7.4448725 -11.9211365
    ## [25]   5.1603929  -4.7410261   6.2392831  -0.5675471   3.1286714   9.6010483

``` r
list_norm[[3]]
```

    ##  [1]  9.867020 10.429457 10.273375 10.250991 10.258240 10.162421 10.179986
    ##  [8] 10.012653 10.020572  9.744698 10.356048 10.229940 10.097227 10.165594
    ## [15]  9.590347 10.306782 10.237168 10.377565 10.237674  9.976944  9.700159
    ## [22]  9.933553 10.251139  9.506537  9.563587  9.794636  9.942226  9.724984
    ## [29] 10.149739 10.030909  9.981973  9.786148 10.083372  9.759187  9.770845
    ## [36] 10.300163  9.834468  9.792100 10.254420 10.056874

``` r
list_norm[[4]]
```

    ##  [1] -1.775992 -3.517999 -1.889596 -3.720322 -4.180576 -2.825448 -2.467010
    ##  [8] -4.000895 -2.462634 -3.602608 -3.390259 -3.385608 -2.658832 -3.615186
    ## [15] -2.853783 -1.848820 -2.238918 -3.114111 -2.036296 -3.868798

``` r
mean_and_sd(list_norm[[1]])
```

    ## # A tibble: 1 x 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  3.30  1.05

``` r
mean_and_sd(list_norm[[2]])
```

    ## # A tibble: 1 x 2
    ##     mean    sd
    ##    <dbl> <dbl>
    ## 1 -0.842  5.48

``` r
mean_and_sd(list_norm[[3]])
```

    ## # A tibble: 1 x 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  10.0 0.246

``` r
mean_and_sd(list_norm[[4]])
```

    ## # A tibble: 1 x 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1 -2.97 0.771

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

``` r
output = map(list_norm, median)

output = map_dbl(list_norm, median)
## this creates a different kind of fancier list - it is giving e a vector
```

``` r
output = map_df(list_norm, mean_and_sd)
## what this does is instead of having multiple lists (4 lists), it creates a dataframe and binds them 
output = map_df(list_norm, mean_and_sd, .id = "input")
## here, .id = "input" tells it to keep track of from which list the mean and sd are coming from
```

Up to this point, for loops, map statements, we got lists. Key idea is
keeping track of everything so in your environment, you’ve got a lot of
stuff. What you want to have is something that keeps tracks of inputs
and outputs at the same time.

## List columns\!

``` r
listcol_df =
  tibble(
    name = c("a", "b", "c", "d"),
    samp = list_norm
  )
## this is a dataframe - printed tibble shows you the name and the lists and their elements
```

``` r
listcol_df %>% pull(name)
```

    ## [1] "a" "b" "c" "d"

``` r
listcol_df %>% pull(samp)
```

    ## $a
    ##  [1] 3.165231 2.430264 2.845420 2.746671 4.632908 1.698360 3.234596 4.716283
    ##  [9] 5.588216 1.905555 5.357418 3.308823 3.064374 2.242463 3.183032 3.065470
    ## [17] 3.823775 2.793408 3.449930 2.822274
    ## 
    ## $b
    ##  [1]  -1.0273108  -4.6520136  -4.7100328  -3.1257576  -2.3206759   1.7942328
    ##  [7]  -6.6617379  -1.2954238  -2.0137220  -8.2432422   8.0627530   0.1421405
    ## [13]   3.1783954  -3.4096608   8.6609997  -1.7979736   0.7644718  -9.1008577
    ## [19]   5.0834091  -2.1984694  -5.4412863   3.6036193  -7.4448725 -11.9211365
    ## [25]   5.1603929  -4.7410261   6.2392831  -0.5675471   3.1286714   9.6010483
    ## 
    ## $c
    ##  [1]  9.867020 10.429457 10.273375 10.250991 10.258240 10.162421 10.179986
    ##  [8] 10.012653 10.020572  9.744698 10.356048 10.229940 10.097227 10.165594
    ## [15]  9.590347 10.306782 10.237168 10.377565 10.237674  9.976944  9.700159
    ## [22]  9.933553 10.251139  9.506537  9.563587  9.794636  9.942226  9.724984
    ## [29] 10.149739 10.030909  9.981973  9.786148 10.083372  9.759187  9.770845
    ## [36] 10.300163  9.834468  9.792100 10.254420 10.056874
    ## 
    ## $d
    ##  [1] -1.775992 -3.517999 -1.889596 -3.720322 -4.180576 -2.825448 -2.467010
    ##  [8] -4.000895 -2.462634 -3.602608 -3.390259 -3.385608 -2.658832 -3.615186
    ## [15] -2.853783 -1.848820 -2.238918 -3.114111 -2.036296 -3.868798

``` r
## so the listcol_df still has all the elements that should be there, it is just a more compact way of looking at things
## it's a dataframe, so you can still do whatever you want to a dataframe

listcol_df %>%
  filter(name == "a")
```

    ## # A tibble: 1 x 2
    ##   name  samp        
    ##   <chr> <named list>
    ## 1 a     <dbl [20]>

Let’s try some operations.

``` r
listcol_df$samp
```

    ## $a
    ##  [1] 3.165231 2.430264 2.845420 2.746671 4.632908 1.698360 3.234596 4.716283
    ##  [9] 5.588216 1.905555 5.357418 3.308823 3.064374 2.242463 3.183032 3.065470
    ## [17] 3.823775 2.793408 3.449930 2.822274
    ## 
    ## $b
    ##  [1]  -1.0273108  -4.6520136  -4.7100328  -3.1257576  -2.3206759   1.7942328
    ##  [7]  -6.6617379  -1.2954238  -2.0137220  -8.2432422   8.0627530   0.1421405
    ## [13]   3.1783954  -3.4096608   8.6609997  -1.7979736   0.7644718  -9.1008577
    ## [19]   5.0834091  -2.1984694  -5.4412863   3.6036193  -7.4448725 -11.9211365
    ## [25]   5.1603929  -4.7410261   6.2392831  -0.5675471   3.1286714   9.6010483
    ## 
    ## $c
    ##  [1]  9.867020 10.429457 10.273375 10.250991 10.258240 10.162421 10.179986
    ##  [8] 10.012653 10.020572  9.744698 10.356048 10.229940 10.097227 10.165594
    ## [15]  9.590347 10.306782 10.237168 10.377565 10.237674  9.976944  9.700159
    ## [22]  9.933553 10.251139  9.506537  9.563587  9.794636  9.942226  9.724984
    ## [29] 10.149739 10.030909  9.981973  9.786148 10.083372  9.759187  9.770845
    ## [36] 10.300163  9.834468  9.792100 10.254420 10.056874
    ## 
    ## $d
    ##  [1] -1.775992 -3.517999 -1.889596 -3.720322 -4.180576 -2.825448 -2.467010
    ##  [8] -4.000895 -2.462634 -3.602608 -3.390259 -3.385608 -2.658832 -3.615186
    ## [15] -2.853783 -1.848820 -2.238918 -3.114111 -2.036296 -3.868798

``` r
## dollar sign is the same thing as pulling out that list - a little easier in this example

listcol_df$samp[[1]]
```

    ##  [1] 3.165231 2.430264 2.845420 2.746671 4.632908 1.698360 3.234596 4.716283
    ##  [9] 5.588216 1.905555 5.357418 3.308823 3.064374 2.242463 3.183032 3.065470
    ## [17] 3.823775 2.793408 3.449930 2.822274

``` r
mean_and_sd(listcol_df$samp[[1]])
```

    ## # A tibble: 1 x 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  3.30  1.05

``` r
## so we are applying mean_and_sd function to the df and only the first element in that dataframe

mean_and_sd(listcol_df$samp[[2]])
```

    ## # A tibble: 1 x 2
    ##     mean    sd
    ##    <dbl> <dbl>
    ## 1 -0.842  5.48

``` r
mean_and_sd(listcol_df$samp[[3]])
```

    ## # A tibble: 1 x 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  10.0 0.246

``` r
mean_and_sd(listcol_df$samp[[4]])
```

    ## # A tibble: 1 x 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1 -2.97 0.771

Can I just map??

``` r
map(listcol_df$samp, mean_and_sd)
```

    ## $a
    ## # A tibble: 1 x 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  3.30  1.05
    ## 
    ## $b
    ## # A tibble: 1 x 2
    ##     mean    sd
    ##    <dbl> <dbl>
    ## 1 -0.842  5.48
    ## 
    ## $c
    ## # A tibble: 1 x 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  10.0 0.246
    ## 
    ## $d
    ## # A tibble: 1 x 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1 -2.97 0.771

So… can I add a list column?? YES Mutate issue\!

``` r
listcol_df %>% 
  mutate(summary = map(samp, mean_and_sd))
```

    ## # A tibble: 4 x 3
    ##   name  samp         summary         
    ##   <chr> <named list> <named list>    
    ## 1 a     <dbl [20]>   <tibble [1 × 2]>
    ## 2 b     <dbl [30]>   <tibble [1 × 2]>
    ## 3 c     <dbl [40]>   <tibble [1 × 2]>
    ## 4 d     <dbl [20]>   <tibble [1 × 2]>

``` r
listcol_df =
  listcol_df %>% 
  mutate(summary = map(samp, mean_and_sd))

listcol_df =
  listcol_df %>% 
  mutate(summary = map_df(samp, mean_and_sd))

listcol_df =
  listcol_df %>% 
  mutate(
    summary = map(samp, mean_and_sd),
    medians = map(samp, median)
  )

listcol_df =
  listcol_df %>% 
  mutate(
    summary = map(samp, mean_and_sd),
    medians = map_dbl(samp, median)
  )

## so the process here, in a few lines of code, is to say i hae a df, created a mean_and_sd summary, and median for these elements... you don't have a bunch of vectors flaoting around and everythign is in a dataframe.
```

Now let’s look at a more concrete example that is less contrived

## Weather data

``` r
weather_df = 
  rnoaa::meteo_pull_monitors(
    c("USW00094728", "USC00519397", "USS0023B17S"),
    var = c("PRCP", "TMIN", "TMAX"), 
    date_min = "2017-01-01",
    date_max = "2017-12-31") %>%
  mutate(
    name = recode(
      id, 
      USW00094728 = "CentralPark_NY", 
      USC00519397 = "Waikiki_HA",
      USS0023B17S = "Waterhole_WA"),
    tmin = tmin / 10,
    tmax = tmax / 10) %>%
  select(name, id, everything())
```

    ## Registered S3 method overwritten by 'hoardr':
    ##   method           from
    ##   print.cache_info httr

    ## using cached file: /Users/jerrychao/Library/Caches/R/noaa_ghcnd/USW00094728.dly

    ## date created (size, mb): 2020-10-01 11:21:13 (7.519)

    ## file min/max dates: 1869-01-01 / 2020-09-30

    ## using cached file: /Users/jerrychao/Library/Caches/R/noaa_ghcnd/USC00519397.dly

    ## date created (size, mb): 2020-10-01 11:21:23 (1.699)

    ## file min/max dates: 1965-01-01 / 2020-03-31

    ## using cached file: /Users/jerrychao/Library/Caches/R/noaa_ghcnd/USS0023B17S.dly

    ## date created (size, mb): 2020-10-01 11:21:28 (0.877)

    ## file min/max dates: 1999-09-01 / 2020-09-30

Get our list columns ..

``` r
weather_nest =
  weather_df %>% 
  nest(data = date:tmin)
```

``` r
weather_nest %>% pull(name)
```

    ## [1] "CentralPark_NY" "Waikiki_HA"     "Waterhole_WA"

``` r
weather_nest %>% pull(data)
```

    ## [[1]]
    ## # A tibble: 365 x 4
    ##    date        prcp  tmax  tmin
    ##    <date>     <dbl> <dbl> <dbl>
    ##  1 2017-01-01     0   8.9   4.4
    ##  2 2017-01-02    53   5     2.8
    ##  3 2017-01-03   147   6.1   3.9
    ##  4 2017-01-04     0  11.1   1.1
    ##  5 2017-01-05     0   1.1  -2.7
    ##  6 2017-01-06    13   0.6  -3.8
    ##  7 2017-01-07    81  -3.2  -6.6
    ##  8 2017-01-08     0  -3.8  -8.8
    ##  9 2017-01-09     0  -4.9  -9.9
    ## 10 2017-01-10     0   7.8  -6  
    ## # … with 355 more rows
    ## 
    ## [[2]]
    ## # A tibble: 365 x 4
    ##    date        prcp  tmax  tmin
    ##    <date>     <dbl> <dbl> <dbl>
    ##  1 2017-01-01     0  26.7  16.7
    ##  2 2017-01-02     0  27.2  16.7
    ##  3 2017-01-03     0  27.8  17.2
    ##  4 2017-01-04     0  27.2  16.7
    ##  5 2017-01-05     0  27.8  16.7
    ##  6 2017-01-06     0  27.2  16.7
    ##  7 2017-01-07     0  27.2  16.7
    ##  8 2017-01-08     0  25.6  15  
    ##  9 2017-01-09     0  27.2  15.6
    ## 10 2017-01-10     0  28.3  17.2
    ## # … with 355 more rows
    ## 
    ## [[3]]
    ## # A tibble: 365 x 4
    ##    date        prcp  tmax  tmin
    ##    <date>     <dbl> <dbl> <dbl>
    ##  1 2017-01-01   432  -6.8 -10.7
    ##  2 2017-01-02    25 -10.5 -12.4
    ##  3 2017-01-03     0  -8.9 -15.9
    ##  4 2017-01-04     0  -9.9 -15.5
    ##  5 2017-01-05     0  -5.9 -14.2
    ##  6 2017-01-06     0  -4.4 -11.3
    ##  7 2017-01-07    51   0.6 -11.5
    ##  8 2017-01-08    76   2.3  -1.2
    ##  9 2017-01-09    51  -1.2  -7  
    ## 10 2017-01-10     0  -5   -14.2
    ## # … with 355 more rows

``` r
weather_nest$data[[1]]
```

    ## # A tibble: 365 x 4
    ##    date        prcp  tmax  tmin
    ##    <date>     <dbl> <dbl> <dbl>
    ##  1 2017-01-01     0   8.9   4.4
    ##  2 2017-01-02    53   5     2.8
    ##  3 2017-01-03   147   6.1   3.9
    ##  4 2017-01-04     0  11.1   1.1
    ##  5 2017-01-05     0   1.1  -2.7
    ##  6 2017-01-06    13   0.6  -3.8
    ##  7 2017-01-07    81  -3.2  -6.6
    ##  8 2017-01-08     0  -3.8  -8.8
    ##  9 2017-01-09     0  -4.9  -9.9
    ## 10 2017-01-10     0   7.8  -6  
    ## # … with 355 more rows

``` r
# just the tibble for central park
weather_nest$data[[2]]
```

    ## # A tibble: 365 x 4
    ##    date        prcp  tmax  tmin
    ##    <date>     <dbl> <dbl> <dbl>
    ##  1 2017-01-01     0  26.7  16.7
    ##  2 2017-01-02     0  27.2  16.7
    ##  3 2017-01-03     0  27.8  17.2
    ##  4 2017-01-04     0  27.2  16.7
    ##  5 2017-01-05     0  27.8  16.7
    ##  6 2017-01-06     0  27.2  16.7
    ##  7 2017-01-07     0  27.2  16.7
    ##  8 2017-01-08     0  25.6  15  
    ##  9 2017-01-09     0  27.2  15.6
    ## 10 2017-01-10     0  28.3  17.2
    ## # … with 355 more rows

``` r
# just the tibble for waikiki
weather_nest$data[[3]]
```

    ## # A tibble: 365 x 4
    ##    date        prcp  tmax  tmin
    ##    <date>     <dbl> <dbl> <dbl>
    ##  1 2017-01-01   432  -6.8 -10.7
    ##  2 2017-01-02    25 -10.5 -12.4
    ##  3 2017-01-03     0  -8.9 -15.9
    ##  4 2017-01-04     0  -9.9 -15.5
    ##  5 2017-01-05     0  -5.9 -14.2
    ##  6 2017-01-06     0  -4.4 -11.3
    ##  7 2017-01-07    51   0.6 -11.5
    ##  8 2017-01-08    76   2.3  -1.2
    ##  9 2017-01-09    51  -1.2  -7  
    ## 10 2017-01-10     0  -5   -14.2
    ## # … with 355 more rows

``` r
# # just the tibble for water hole
```

Suppose I want to regress `tmax` on `tmin` for each station.

This works …

``` r
lm(tmax ~ tmin, data = weather_nest$data[[1]])
```

    ## 
    ## Call:
    ## lm(formula = tmax ~ tmin, data = weather_nest$data[[1]])
    ## 
    ## Coefficients:
    ## (Intercept)         tmin  
    ##       7.209        1.039

Let’s write s funtion. to do this regression

``` r
weather_lm = function(df) {
  
  lm(tmax ~ tmin, data = df)
  
}

weather_lm(weather_nest$data[[1]])
```

    ## 
    ## Call:
    ## lm(formula = tmax ~ tmin, data = df)
    ## 
    ## Coefficients:
    ## (Intercept)         tmin  
    ##       7.209        1.039

``` r
weather_lm(weather_nest$data[[1]])
```

    ## 
    ## Call:
    ## lm(formula = tmax ~ tmin, data = df)
    ## 
    ## Coefficients:
    ## (Intercept)         tmin  
    ##       7.209        1.039

``` r
weather_lm(weather_nest$data[[1]])
```

    ## 
    ## Call:
    ## lm(formula = tmax ~ tmin, data = df)
    ## 
    ## Coefficients:
    ## (Intercept)         tmin  
    ##       7.209        1.039

``` r
weather_lm(weather_nest$data[[1]])
```

    ## 
    ## Call:
    ## lm(formula = tmax ~ tmin, data = df)
    ## 
    ## Coefficients:
    ## (Intercept)         tmin  
    ##       7.209        1.039

``` r
##can do a for loop

output = vector("list", 3)

for (i in 1:3) {
  
  output[[i]] = weather_lm(weather_nest$data[[i]])

  }
```

What about a map …\!?

``` r
weather_nest$data
```

    ## [[1]]
    ## # A tibble: 365 x 4
    ##    date        prcp  tmax  tmin
    ##    <date>     <dbl> <dbl> <dbl>
    ##  1 2017-01-01     0   8.9   4.4
    ##  2 2017-01-02    53   5     2.8
    ##  3 2017-01-03   147   6.1   3.9
    ##  4 2017-01-04     0  11.1   1.1
    ##  5 2017-01-05     0   1.1  -2.7
    ##  6 2017-01-06    13   0.6  -3.8
    ##  7 2017-01-07    81  -3.2  -6.6
    ##  8 2017-01-08     0  -3.8  -8.8
    ##  9 2017-01-09     0  -4.9  -9.9
    ## 10 2017-01-10     0   7.8  -6  
    ## # … with 355 more rows
    ## 
    ## [[2]]
    ## # A tibble: 365 x 4
    ##    date        prcp  tmax  tmin
    ##    <date>     <dbl> <dbl> <dbl>
    ##  1 2017-01-01     0  26.7  16.7
    ##  2 2017-01-02     0  27.2  16.7
    ##  3 2017-01-03     0  27.8  17.2
    ##  4 2017-01-04     0  27.2  16.7
    ##  5 2017-01-05     0  27.8  16.7
    ##  6 2017-01-06     0  27.2  16.7
    ##  7 2017-01-07     0  27.2  16.7
    ##  8 2017-01-08     0  25.6  15  
    ##  9 2017-01-09     0  27.2  15.6
    ## 10 2017-01-10     0  28.3  17.2
    ## # … with 355 more rows
    ## 
    ## [[3]]
    ## # A tibble: 365 x 4
    ##    date        prcp  tmax  tmin
    ##    <date>     <dbl> <dbl> <dbl>
    ##  1 2017-01-01   432  -6.8 -10.7
    ##  2 2017-01-02    25 -10.5 -12.4
    ##  3 2017-01-03     0  -8.9 -15.9
    ##  4 2017-01-04     0  -9.9 -15.5
    ##  5 2017-01-05     0  -5.9 -14.2
    ##  6 2017-01-06     0  -4.4 -11.3
    ##  7 2017-01-07    51   0.6 -11.5
    ##  8 2017-01-08    76   2.3  -1.2
    ##  9 2017-01-09    51  -1.2  -7  
    ## 10 2017-01-10     0  -5   -14.2
    ## # … with 355 more rows

``` r
map(weather_nest$data, weather_lm)
```

    ## [[1]]
    ## 
    ## Call:
    ## lm(formula = tmax ~ tmin, data = df)
    ## 
    ## Coefficients:
    ## (Intercept)         tmin  
    ##       7.209        1.039  
    ## 
    ## 
    ## [[2]]
    ## 
    ## Call:
    ## lm(formula = tmax ~ tmin, data = df)
    ## 
    ## Coefficients:
    ## (Intercept)         tmin  
    ##     20.0966       0.4509  
    ## 
    ## 
    ## [[3]]
    ## 
    ## Call:
    ## lm(formula = tmax ~ tmin, data = df)
    ## 
    ## Coefficients:
    ## (Intercept)         tmin  
    ##       7.499        1.221

What about a map in a list column \!\!\!\!\!??

``` r
weather_nest =
  weather_nest %>% 
    mutate(
      models = map(data, weather_lm)
    )

weather_nest$models
```

    ## [[1]]
    ## 
    ## Call:
    ## lm(formula = tmax ~ tmin, data = df)
    ## 
    ## Coefficients:
    ## (Intercept)         tmin  
    ##       7.209        1.039  
    ## 
    ## 
    ## [[2]]
    ## 
    ## Call:
    ## lm(formula = tmax ~ tmin, data = df)
    ## 
    ## Coefficients:
    ## (Intercept)         tmin  
    ##     20.0966       0.4509  
    ## 
    ## 
    ## [[3]]
    ## 
    ## Call:
    ## lm(formula = tmax ~ tmin, data = df)
    ## 
    ## Coefficients:
    ## (Intercept)         tmin  
    ##       7.499        1.221

Summary: talked about lists, assumed we know how lists work, used lists
as list columns, for loops, map statements, and given list columns,
we’ve used map function to create more list columns

This is foundaational tools to run simulation, etc. bootstrapping etc.
Big shift

Group by and Summarize - can only get you so far, but can’t summarize
with regression - this allows you to do it.
