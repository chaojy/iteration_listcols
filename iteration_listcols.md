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
    ## -2.46483 -0.78795 -0.06930 -0.05433  0.65039  2.24889

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

    ##  [1] 3.1280431 3.1971867 2.8971197 4.2232330 2.5831051 3.6660708 1.8674566
    ##  [8] 1.8223790 2.3480144 2.3666703 3.5750554 0.5729492 2.5706629 1.3068899
    ## [15] 3.5246407 1.6070644 1.5028620 2.7233786 2.6923085 1.6237573

``` r
list_norm
```

    ## $a
    ##  [1] 3.1280431 3.1971867 2.8971197 4.2232330 2.5831051 3.6660708 1.8674566
    ##  [8] 1.8223790 2.3480144 2.3666703 3.5750554 0.5729492 2.5706629 1.3068899
    ## [15] 3.5246407 1.6070644 1.5028620 2.7233786 2.6923085 1.6237573
    ## 
    ## $b
    ##  [1]   3.7358770   4.0365914   8.5078511  -1.7240826   1.9683336   9.6402146
    ##  [7]  -4.6559495  -1.4238157   2.9599076   5.2882203   1.1139659  14.9682345
    ## [13] -10.0321764  -1.2062273   3.2263538  -0.7965848   1.0775749   1.6546803
    ## [19]   3.4195735  -1.3433407   1.9081996   3.0497967  -3.8950346  -5.8143380
    ## [25]  -5.3480183   5.7901201 -12.1351172  -2.9845919  -1.3058023  -5.3357556
    ## 
    ## $c
    ##  [1]  9.917159 10.162593  9.793953 10.062576  9.905221 10.121064  9.812133
    ##  [8]  9.961796 10.267222 10.185987  9.884382  9.885265 10.061553  9.875520
    ## [15]  9.753427  9.858038  9.981936 10.150854 10.199016  9.914173  9.737107
    ## [22] 10.168717  9.951216 10.059043  9.532068 10.134785 10.081685  9.971200
    ## [29] 10.381037  9.838269 10.078105  9.821936  9.970728 10.254696  9.877225
    ## [36]  9.882985 10.045489  9.724553  9.925747  9.652967
    ## 
    ## $d
    ##  [1] -3.468218 -1.029863 -3.885844 -2.094342 -2.387821 -3.878306 -3.699426
    ##  [8] -2.669653 -1.219442 -2.107718 -3.447252 -3.934666 -4.733689 -4.259569
    ## [15] -2.251979 -3.753774 -3.584602 -1.736640 -3.600637 -2.193971

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

    ##  [1] 3.1280431 3.1971867 2.8971197 4.2232330 2.5831051 3.6660708 1.8674566
    ##  [8] 1.8223790 2.3480144 2.3666703 3.5750554 0.5729492 2.5706629 1.3068899
    ## [15] 3.5246407 1.6070644 1.5028620 2.7233786 2.6923085 1.6237573

``` r
list_norm[[2]]
```

    ##  [1]   3.7358770   4.0365914   8.5078511  -1.7240826   1.9683336   9.6402146
    ##  [7]  -4.6559495  -1.4238157   2.9599076   5.2882203   1.1139659  14.9682345
    ## [13] -10.0321764  -1.2062273   3.2263538  -0.7965848   1.0775749   1.6546803
    ## [19]   3.4195735  -1.3433407   1.9081996   3.0497967  -3.8950346  -5.8143380
    ## [25]  -5.3480183   5.7901201 -12.1351172  -2.9845919  -1.3058023  -5.3357556

``` r
list_norm[[3]]
```

    ##  [1]  9.917159 10.162593  9.793953 10.062576  9.905221 10.121064  9.812133
    ##  [8]  9.961796 10.267222 10.185987  9.884382  9.885265 10.061553  9.875520
    ## [15]  9.753427  9.858038  9.981936 10.150854 10.199016  9.914173  9.737107
    ## [22] 10.168717  9.951216 10.059043  9.532068 10.134785 10.081685  9.971200
    ## [29] 10.381037  9.838269 10.078105  9.821936  9.970728 10.254696  9.877225
    ## [36]  9.882985 10.045489  9.724553  9.925747  9.652967

``` r
list_norm[[4]]
```

    ##  [1] -3.468218 -1.029863 -3.885844 -2.094342 -2.387821 -3.878306 -3.699426
    ##  [8] -2.669653 -1.219442 -2.107718 -3.447252 -3.934666 -4.733689 -4.259569
    ## [15] -2.251979 -3.753774 -3.584602 -1.736640 -3.600637 -2.193971

``` r
mean_and_sd(list_norm[[1]])
```

    ## # A tibble: 1 x 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  2.49 0.925

``` r
mean_and_sd(list_norm[[2]])
```

    ## # A tibble: 1 x 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1 0.478  5.64

``` r
mean_and_sd(list_norm[[3]])
```

    ## # A tibble: 1 x 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  9.97 0.180

``` r
mean_and_sd(list_norm[[4]])
```

    ## # A tibble: 1 x 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1 -3.00  1.06

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
    ##  [1] 3.1280431 3.1971867 2.8971197 4.2232330 2.5831051 3.6660708 1.8674566
    ##  [8] 1.8223790 2.3480144 2.3666703 3.5750554 0.5729492 2.5706629 1.3068899
    ## [15] 3.5246407 1.6070644 1.5028620 2.7233786 2.6923085 1.6237573
    ## 
    ## $b
    ##  [1]   3.7358770   4.0365914   8.5078511  -1.7240826   1.9683336   9.6402146
    ##  [7]  -4.6559495  -1.4238157   2.9599076   5.2882203   1.1139659  14.9682345
    ## [13] -10.0321764  -1.2062273   3.2263538  -0.7965848   1.0775749   1.6546803
    ## [19]   3.4195735  -1.3433407   1.9081996   3.0497967  -3.8950346  -5.8143380
    ## [25]  -5.3480183   5.7901201 -12.1351172  -2.9845919  -1.3058023  -5.3357556
    ## 
    ## $c
    ##  [1]  9.917159 10.162593  9.793953 10.062576  9.905221 10.121064  9.812133
    ##  [8]  9.961796 10.267222 10.185987  9.884382  9.885265 10.061553  9.875520
    ## [15]  9.753427  9.858038  9.981936 10.150854 10.199016  9.914173  9.737107
    ## [22] 10.168717  9.951216 10.059043  9.532068 10.134785 10.081685  9.971200
    ## [29] 10.381037  9.838269 10.078105  9.821936  9.970728 10.254696  9.877225
    ## [36]  9.882985 10.045489  9.724553  9.925747  9.652967
    ## 
    ## $d
    ##  [1] -3.468218 -1.029863 -3.885844 -2.094342 -2.387821 -3.878306 -3.699426
    ##  [8] -2.669653 -1.219442 -2.107718 -3.447252 -3.934666 -4.733689 -4.259569
    ## [15] -2.251979 -3.753774 -3.584602 -1.736640 -3.600637 -2.193971

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
    ##  [1] 3.1280431 3.1971867 2.8971197 4.2232330 2.5831051 3.6660708 1.8674566
    ##  [8] 1.8223790 2.3480144 2.3666703 3.5750554 0.5729492 2.5706629 1.3068899
    ## [15] 3.5246407 1.6070644 1.5028620 2.7233786 2.6923085 1.6237573
    ## 
    ## $b
    ##  [1]   3.7358770   4.0365914   8.5078511  -1.7240826   1.9683336   9.6402146
    ##  [7]  -4.6559495  -1.4238157   2.9599076   5.2882203   1.1139659  14.9682345
    ## [13] -10.0321764  -1.2062273   3.2263538  -0.7965848   1.0775749   1.6546803
    ## [19]   3.4195735  -1.3433407   1.9081996   3.0497967  -3.8950346  -5.8143380
    ## [25]  -5.3480183   5.7901201 -12.1351172  -2.9845919  -1.3058023  -5.3357556
    ## 
    ## $c
    ##  [1]  9.917159 10.162593  9.793953 10.062576  9.905221 10.121064  9.812133
    ##  [8]  9.961796 10.267222 10.185987  9.884382  9.885265 10.061553  9.875520
    ## [15]  9.753427  9.858038  9.981936 10.150854 10.199016  9.914173  9.737107
    ## [22] 10.168717  9.951216 10.059043  9.532068 10.134785 10.081685  9.971200
    ## [29] 10.381037  9.838269 10.078105  9.821936  9.970728 10.254696  9.877225
    ## [36]  9.882985 10.045489  9.724553  9.925747  9.652967
    ## 
    ## $d
    ##  [1] -3.468218 -1.029863 -3.885844 -2.094342 -2.387821 -3.878306 -3.699426
    ##  [8] -2.669653 -1.219442 -2.107718 -3.447252 -3.934666 -4.733689 -4.259569
    ## [15] -2.251979 -3.753774 -3.584602 -1.736640 -3.600637 -2.193971

``` r
## dollar sign is the same thing as pulling out that list - a little easier in this example

listcol_df$samp[[1]]
```

    ##  [1] 3.1280431 3.1971867 2.8971197 4.2232330 2.5831051 3.6660708 1.8674566
    ##  [8] 1.8223790 2.3480144 2.3666703 3.5750554 0.5729492 2.5706629 1.3068899
    ## [15] 3.5246407 1.6070644 1.5028620 2.7233786 2.6923085 1.6237573

``` r
mean_and_sd(listcol_df$samp[[1]])
```

    ## # A tibble: 1 x 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  2.49 0.925

``` r
## so we are applying mean_and_sd function to the df and only the first element in that dataframe

mean_and_sd(listcol_df$samp[[2]])
```

    ## # A tibble: 1 x 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1 0.478  5.64

``` r
mean_and_sd(listcol_df$samp[[3]])
```

    ## # A tibble: 1 x 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  9.97 0.180

``` r
mean_and_sd(listcol_df$samp[[4]])
```

    ## # A tibble: 1 x 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1 -3.00  1.06

Can I just map??

``` r
map(listcol_df$samp, mean_and_sd)
```

    ## $a
    ## # A tibble: 1 x 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  2.49 0.925
    ## 
    ## $b
    ## # A tibble: 1 x 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1 0.478  5.64
    ## 
    ## $c
    ## # A tibble: 1 x 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  9.97 0.180
    ## 
    ## $d
    ## # A tibble: 1 x 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1 -3.00  1.06

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
