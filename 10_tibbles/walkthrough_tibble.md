Walkthrough for chapter 10- Tibbles
================

  - [Creating tibbles](#creating-tibbles)
  - [Tibbles vs data.frame](#tibbles-vs-data.frame)
  - [Exercises](#exercises)

``` r
library(tidyverse)
```

    ## -- Attaching packages ------------------------------------------------------------------------------------------------------------------- tidyverse 1.2.1 --

    ## v ggplot2 3.2.1     v purrr   0.3.3
    ## v tibble  2.1.3     v dplyr   0.8.3
    ## v tidyr   1.0.0     v stringr 1.4.0
    ## v readr   1.3.1     v forcats 0.4.0

    ## -- Conflicts ---------------------------------------------------------------------------------------------------------------------- tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library(here)
```

    ## here() starts at D:/Documents/Learning/r-for-data-science

``` r
library(knitr)

theme_set(theme_light())

opts_chunk$set(
  cache = TRUE,
  message = FALSE, 
  warning = FALSE, 
  fig.width = 10, 
  fig.height = 7
  )
```

-----

# Creating tibbles

Tibbles are essentially data frames with a few nicer functionalities

as\_tibble() is the function that coerces a data frame to a tibble

``` r
as_tibble(iris)
```

    ## # A tibble: 150 x 5
    ##    Sepal.Length Sepal.Width Petal.Length Petal.Width Species
    ##           <dbl>       <dbl>        <dbl>       <dbl> <fct>  
    ##  1          5.1         3.5          1.4         0.2 setosa 
    ##  2          4.9         3            1.4         0.2 setosa 
    ##  3          4.7         3.2          1.3         0.2 setosa 
    ##  4          4.6         3.1          1.5         0.2 setosa 
    ##  5          5           3.6          1.4         0.2 setosa 
    ##  6          5.4         3.9          1.7         0.4 setosa 
    ##  7          4.6         3.4          1.4         0.3 setosa 
    ##  8          5           3.4          1.5         0.2 setosa 
    ##  9          4.4         2.9          1.4         0.2 setosa 
    ## 10          4.9         3.1          1.5         0.1 setosa 
    ## # ... with 140 more rows

tibble() can be used to create a new data object type tibble

``` r
tibble(
  x = 1:5,
  y = 1,
  z = x^2 + y
)
```

    ## # A tibble: 5 x 3
    ##       x     y     z
    ##   <int> <dbl> <dbl>
    ## 1     1     1     2
    ## 2     2     1     5
    ## 3     3     1    10
    ## 4     4     1    17
    ## 5     5     1    26

tibble() does not change the input type (e.g. string –\> factor),
doesn’t change the variable names, and doesn’t create row names.

Columns can also be non-syntatic

``` r
tibble(
  `:)` = 1:100,
  `:(` = 2
)
```

    ## # A tibble: 100 x 2
    ##     `:)`  `:(`
    ##    <int> <dbl>
    ##  1     1     2
    ##  2     2     2
    ##  3     3     2
    ##  4     4     2
    ##  5     5     2
    ##  6     6     2
    ##  7     7     2
    ##  8     8     2
    ##  9     9     2
    ## 10    10     2
    ## # ... with 90 more rows

tribble() is another way to create a tibble and allows for traditional
data entry to create a dataset

``` r
tribble(
  ~x, ~y, ~z,
  
  "a", 2, 3.6,
  "b", 1, 8.5
)
```

    ## # A tibble: 2 x 3
    ##   x         y     z
    ##   <chr> <dbl> <dbl>
    ## 1 a         2   3.6
    ## 2 b         1   8.5

-----

# Tibbles vs data.frame

There are two main differences between tibbles and data frames:

  - **Printing**

Default prints to 10 rows

``` r
as_tibble(iris) %>% print()
```

    ## # A tibble: 150 x 5
    ##    Sepal.Length Sepal.Width Petal.Length Petal.Width Species
    ##           <dbl>       <dbl>        <dbl>       <dbl> <fct>  
    ##  1          5.1         3.5          1.4         0.2 setosa 
    ##  2          4.9         3            1.4         0.2 setosa 
    ##  3          4.7         3.2          1.3         0.2 setosa 
    ##  4          4.6         3.1          1.5         0.2 setosa 
    ##  5          5           3.6          1.4         0.2 setosa 
    ##  6          5.4         3.9          1.7         0.4 setosa 
    ##  7          4.6         3.4          1.4         0.3 setosa 
    ##  8          5           3.4          1.5         0.2 setosa 
    ##  9          4.4         2.9          1.4         0.2 setosa 
    ## 10          4.9         3.1          1.5         0.1 setosa 
    ## # ... with 140 more rows

``` r
iris %>% print()
```

    ##     Sepal.Length Sepal.Width Petal.Length Petal.Width    Species
    ## 1            5.1         3.5          1.4         0.2     setosa
    ## 2            4.9         3.0          1.4         0.2     setosa
    ## 3            4.7         3.2          1.3         0.2     setosa
    ## 4            4.6         3.1          1.5         0.2     setosa
    ## 5            5.0         3.6          1.4         0.2     setosa
    ## 6            5.4         3.9          1.7         0.4     setosa
    ## 7            4.6         3.4          1.4         0.3     setosa
    ## 8            5.0         3.4          1.5         0.2     setosa
    ## 9            4.4         2.9          1.4         0.2     setosa
    ## 10           4.9         3.1          1.5         0.1     setosa
    ## 11           5.4         3.7          1.5         0.2     setosa
    ## 12           4.8         3.4          1.6         0.2     setosa
    ## 13           4.8         3.0          1.4         0.1     setosa
    ## 14           4.3         3.0          1.1         0.1     setosa
    ## 15           5.8         4.0          1.2         0.2     setosa
    ## 16           5.7         4.4          1.5         0.4     setosa
    ## 17           5.4         3.9          1.3         0.4     setosa
    ## 18           5.1         3.5          1.4         0.3     setosa
    ## 19           5.7         3.8          1.7         0.3     setosa
    ## 20           5.1         3.8          1.5         0.3     setosa
    ## 21           5.4         3.4          1.7         0.2     setosa
    ## 22           5.1         3.7          1.5         0.4     setosa
    ## 23           4.6         3.6          1.0         0.2     setosa
    ## 24           5.1         3.3          1.7         0.5     setosa
    ## 25           4.8         3.4          1.9         0.2     setosa
    ## 26           5.0         3.0          1.6         0.2     setosa
    ## 27           5.0         3.4          1.6         0.4     setosa
    ## 28           5.2         3.5          1.5         0.2     setosa
    ## 29           5.2         3.4          1.4         0.2     setosa
    ## 30           4.7         3.2          1.6         0.2     setosa
    ## 31           4.8         3.1          1.6         0.2     setosa
    ## 32           5.4         3.4          1.5         0.4     setosa
    ## 33           5.2         4.1          1.5         0.1     setosa
    ## 34           5.5         4.2          1.4         0.2     setosa
    ## 35           4.9         3.1          1.5         0.2     setosa
    ## 36           5.0         3.2          1.2         0.2     setosa
    ## 37           5.5         3.5          1.3         0.2     setosa
    ## 38           4.9         3.6          1.4         0.1     setosa
    ## 39           4.4         3.0          1.3         0.2     setosa
    ## 40           5.1         3.4          1.5         0.2     setosa
    ## 41           5.0         3.5          1.3         0.3     setosa
    ## 42           4.5         2.3          1.3         0.3     setosa
    ## 43           4.4         3.2          1.3         0.2     setosa
    ## 44           5.0         3.5          1.6         0.6     setosa
    ## 45           5.1         3.8          1.9         0.4     setosa
    ## 46           4.8         3.0          1.4         0.3     setosa
    ## 47           5.1         3.8          1.6         0.2     setosa
    ## 48           4.6         3.2          1.4         0.2     setosa
    ## 49           5.3         3.7          1.5         0.2     setosa
    ## 50           5.0         3.3          1.4         0.2     setosa
    ## 51           7.0         3.2          4.7         1.4 versicolor
    ## 52           6.4         3.2          4.5         1.5 versicolor
    ## 53           6.9         3.1          4.9         1.5 versicolor
    ## 54           5.5         2.3          4.0         1.3 versicolor
    ## 55           6.5         2.8          4.6         1.5 versicolor
    ## 56           5.7         2.8          4.5         1.3 versicolor
    ## 57           6.3         3.3          4.7         1.6 versicolor
    ## 58           4.9         2.4          3.3         1.0 versicolor
    ## 59           6.6         2.9          4.6         1.3 versicolor
    ## 60           5.2         2.7          3.9         1.4 versicolor
    ## 61           5.0         2.0          3.5         1.0 versicolor
    ## 62           5.9         3.0          4.2         1.5 versicolor
    ## 63           6.0         2.2          4.0         1.0 versicolor
    ## 64           6.1         2.9          4.7         1.4 versicolor
    ## 65           5.6         2.9          3.6         1.3 versicolor
    ## 66           6.7         3.1          4.4         1.4 versicolor
    ## 67           5.6         3.0          4.5         1.5 versicolor
    ## 68           5.8         2.7          4.1         1.0 versicolor
    ## 69           6.2         2.2          4.5         1.5 versicolor
    ## 70           5.6         2.5          3.9         1.1 versicolor
    ## 71           5.9         3.2          4.8         1.8 versicolor
    ## 72           6.1         2.8          4.0         1.3 versicolor
    ## 73           6.3         2.5          4.9         1.5 versicolor
    ## 74           6.1         2.8          4.7         1.2 versicolor
    ## 75           6.4         2.9          4.3         1.3 versicolor
    ## 76           6.6         3.0          4.4         1.4 versicolor
    ## 77           6.8         2.8          4.8         1.4 versicolor
    ## 78           6.7         3.0          5.0         1.7 versicolor
    ## 79           6.0         2.9          4.5         1.5 versicolor
    ## 80           5.7         2.6          3.5         1.0 versicolor
    ## 81           5.5         2.4          3.8         1.1 versicolor
    ## 82           5.5         2.4          3.7         1.0 versicolor
    ## 83           5.8         2.7          3.9         1.2 versicolor
    ## 84           6.0         2.7          5.1         1.6 versicolor
    ## 85           5.4         3.0          4.5         1.5 versicolor
    ## 86           6.0         3.4          4.5         1.6 versicolor
    ## 87           6.7         3.1          4.7         1.5 versicolor
    ## 88           6.3         2.3          4.4         1.3 versicolor
    ## 89           5.6         3.0          4.1         1.3 versicolor
    ## 90           5.5         2.5          4.0         1.3 versicolor
    ## 91           5.5         2.6          4.4         1.2 versicolor
    ## 92           6.1         3.0          4.6         1.4 versicolor
    ## 93           5.8         2.6          4.0         1.2 versicolor
    ## 94           5.0         2.3          3.3         1.0 versicolor
    ## 95           5.6         2.7          4.2         1.3 versicolor
    ## 96           5.7         3.0          4.2         1.2 versicolor
    ## 97           5.7         2.9          4.2         1.3 versicolor
    ## 98           6.2         2.9          4.3         1.3 versicolor
    ## 99           5.1         2.5          3.0         1.1 versicolor
    ## 100          5.7         2.8          4.1         1.3 versicolor
    ## 101          6.3         3.3          6.0         2.5  virginica
    ## 102          5.8         2.7          5.1         1.9  virginica
    ## 103          7.1         3.0          5.9         2.1  virginica
    ## 104          6.3         2.9          5.6         1.8  virginica
    ## 105          6.5         3.0          5.8         2.2  virginica
    ## 106          7.6         3.0          6.6         2.1  virginica
    ## 107          4.9         2.5          4.5         1.7  virginica
    ## 108          7.3         2.9          6.3         1.8  virginica
    ## 109          6.7         2.5          5.8         1.8  virginica
    ## 110          7.2         3.6          6.1         2.5  virginica
    ## 111          6.5         3.2          5.1         2.0  virginica
    ## 112          6.4         2.7          5.3         1.9  virginica
    ## 113          6.8         3.0          5.5         2.1  virginica
    ## 114          5.7         2.5          5.0         2.0  virginica
    ## 115          5.8         2.8          5.1         2.4  virginica
    ## 116          6.4         3.2          5.3         2.3  virginica
    ## 117          6.5         3.0          5.5         1.8  virginica
    ## 118          7.7         3.8          6.7         2.2  virginica
    ## 119          7.7         2.6          6.9         2.3  virginica
    ## 120          6.0         2.2          5.0         1.5  virginica
    ## 121          6.9         3.2          5.7         2.3  virginica
    ## 122          5.6         2.8          4.9         2.0  virginica
    ## 123          7.7         2.8          6.7         2.0  virginica
    ## 124          6.3         2.7          4.9         1.8  virginica
    ## 125          6.7         3.3          5.7         2.1  virginica
    ## 126          7.2         3.2          6.0         1.8  virginica
    ## 127          6.2         2.8          4.8         1.8  virginica
    ## 128          6.1         3.0          4.9         1.8  virginica
    ## 129          6.4         2.8          5.6         2.1  virginica
    ## 130          7.2         3.0          5.8         1.6  virginica
    ## 131          7.4         2.8          6.1         1.9  virginica
    ## 132          7.9         3.8          6.4         2.0  virginica
    ## 133          6.4         2.8          5.6         2.2  virginica
    ## 134          6.3         2.8          5.1         1.5  virginica
    ## 135          6.1         2.6          5.6         1.4  virginica
    ## 136          7.7         3.0          6.1         2.3  virginica
    ## 137          6.3         3.4          5.6         2.4  virginica
    ## 138          6.4         3.1          5.5         1.8  virginica
    ## 139          6.0         3.0          4.8         1.8  virginica
    ## 140          6.9         3.1          5.4         2.1  virginica
    ## 141          6.7         3.1          5.6         2.4  virginica
    ## 142          6.9         3.1          5.1         2.3  virginica
    ## 143          5.8         2.7          5.1         1.9  virginica
    ## 144          6.8         3.2          5.9         2.3  virginica
    ## 145          6.7         3.3          5.7         2.5  virginica
    ## 146          6.7         3.0          5.2         2.3  virginica
    ## 147          6.3         2.5          5.0         1.9  virginica
    ## 148          6.5         3.0          5.2         2.0  virginica
    ## 149          6.2         3.4          5.4         2.3  virginica
    ## 150          5.9         3.0          5.1         1.8  virginica

The width = inf option allows to print all columns

``` r
print(as_tibble(mpg), n = 15, width = Inf)
```

    ## # A tibble: 234 x 11
    ##    manufacturer model      displ  year   cyl trans      drv     cty   hwy fl   
    ##    <chr>        <chr>      <dbl> <int> <int> <chr>      <chr> <int> <int> <chr>
    ##  1 audi         a4           1.8  1999     4 auto(l5)   f        18    29 p    
    ##  2 audi         a4           1.8  1999     4 manual(m5) f        21    29 p    
    ##  3 audi         a4           2    2008     4 manual(m6) f        20    31 p    
    ##  4 audi         a4           2    2008     4 auto(av)   f        21    30 p    
    ##  5 audi         a4           2.8  1999     6 auto(l5)   f        16    26 p    
    ##  6 audi         a4           2.8  1999     6 manual(m5) f        18    26 p    
    ##  7 audi         a4           3.1  2008     6 auto(av)   f        18    27 p    
    ##  8 audi         a4 quattro   1.8  1999     4 manual(m5) 4        18    26 p    
    ##  9 audi         a4 quattro   1.8  1999     4 auto(l5)   4        16    25 p    
    ## 10 audi         a4 quattro   2    2008     4 manual(m6) 4        20    28 p    
    ## 11 audi         a4 quattro   2    2008     4 auto(s6)   4        19    27 p    
    ## 12 audi         a4 quattro   2.8  1999     6 auto(l5)   4        15    25 p    
    ## 13 audi         a4 quattro   2.8  1999     6 manual(m5) 4        17    25 p    
    ## 14 audi         a4 quattro   3.1  2008     6 auto(s6)   4        17    25 p    
    ## 15 audi         a4 quattro   3.1  2008     6 manual(m6) 4        15    25 p    
    ##    class  
    ##    <chr>  
    ##  1 compact
    ##  2 compact
    ##  3 compact
    ##  4 compact
    ##  5 compact
    ##  6 compact
    ##  7 compact
    ##  8 compact
    ##  9 compact
    ## 10 compact
    ## 11 compact
    ## 12 compact
    ## 13 compact
    ## 14 compact
    ## 15 compact
    ## # ... with 219 more rows

View() is also great for easily viewing a dataset in the RStudio data
viewer

``` r
iris %>% View()
```

  - **Subsetting**

Extract a column by name using \[\[\]\] or $

``` r
df <- tibble(
  y = 1:10,
  x = letters[1:10],
  z = rnorm(n = 10)
)

df$x
```

    ##  [1] "a" "b" "c" "d" "e" "f" "g" "h" "i" "j"

``` r
df[["x"]]
```

    ##  [1] "a" "b" "c" "d" "e" "f" "g" "h" "i" "j"

And in a pipe, . is the data set placeholder

``` r
df %>% 
  filter(z < 0) %>% 
  .$z 
```

    ## [1] -0.69256191 -0.44190782 -0.41090414 -0.01223515

-----

# Exercises

**1. How can you tell if an object is a tibble? (Hint: try printing
mtcars, which is a regular data frame).**

``` r
print(mtcars)
```

    ##                      mpg cyl  disp  hp drat    wt  qsec vs am gear carb
    ## Mazda RX4           21.0   6 160.0 110 3.90 2.620 16.46  0  1    4    4
    ## Mazda RX4 Wag       21.0   6 160.0 110 3.90 2.875 17.02  0  1    4    4
    ## Datsun 710          22.8   4 108.0  93 3.85 2.320 18.61  1  1    4    1
    ## Hornet 4 Drive      21.4   6 258.0 110 3.08 3.215 19.44  1  0    3    1
    ## Hornet Sportabout   18.7   8 360.0 175 3.15 3.440 17.02  0  0    3    2
    ## Valiant             18.1   6 225.0 105 2.76 3.460 20.22  1  0    3    1
    ## Duster 360          14.3   8 360.0 245 3.21 3.570 15.84  0  0    3    4
    ## Merc 240D           24.4   4 146.7  62 3.69 3.190 20.00  1  0    4    2
    ## Merc 230            22.8   4 140.8  95 3.92 3.150 22.90  1  0    4    2
    ## Merc 280            19.2   6 167.6 123 3.92 3.440 18.30  1  0    4    4
    ## Merc 280C           17.8   6 167.6 123 3.92 3.440 18.90  1  0    4    4
    ## Merc 450SE          16.4   8 275.8 180 3.07 4.070 17.40  0  0    3    3
    ## Merc 450SL          17.3   8 275.8 180 3.07 3.730 17.60  0  0    3    3
    ## Merc 450SLC         15.2   8 275.8 180 3.07 3.780 18.00  0  0    3    3
    ## Cadillac Fleetwood  10.4   8 472.0 205 2.93 5.250 17.98  0  0    3    4
    ## Lincoln Continental 10.4   8 460.0 215 3.00 5.424 17.82  0  0    3    4
    ## Chrysler Imperial   14.7   8 440.0 230 3.23 5.345 17.42  0  0    3    4
    ## Fiat 128            32.4   4  78.7  66 4.08 2.200 19.47  1  1    4    1
    ## Honda Civic         30.4   4  75.7  52 4.93 1.615 18.52  1  1    4    2
    ## Toyota Corolla      33.9   4  71.1  65 4.22 1.835 19.90  1  1    4    1
    ## Toyota Corona       21.5   4 120.1  97 3.70 2.465 20.01  1  0    3    1
    ## Dodge Challenger    15.5   8 318.0 150 2.76 3.520 16.87  0  0    3    2
    ## AMC Javelin         15.2   8 304.0 150 3.15 3.435 17.30  0  0    3    2
    ## Camaro Z28          13.3   8 350.0 245 3.73 3.840 15.41  0  0    3    4
    ## Pontiac Firebird    19.2   8 400.0 175 3.08 3.845 17.05  0  0    3    2
    ## Fiat X1-9           27.3   4  79.0  66 4.08 1.935 18.90  1  1    4    1
    ## Porsche 914-2       26.0   4 120.3  91 4.43 2.140 16.70  0  1    5    2
    ## Lotus Europa        30.4   4  95.1 113 3.77 1.513 16.90  1  1    5    2
    ## Ford Pantera L      15.8   8 351.0 264 4.22 3.170 14.50  0  1    5    4
    ## Ferrari Dino        19.7   6 145.0 175 3.62 2.770 15.50  0  1    5    6
    ## Maserati Bora       15.0   8 301.0 335 3.54 3.570 14.60  0  1    5    8
    ## Volvo 142E          21.4   4 121.0 109 4.11 2.780 18.60  1  1    4    2

``` r
print(as_tibble(mtcars))
```

    ## # A tibble: 32 x 11
    ##      mpg   cyl  disp    hp  drat    wt  qsec    vs    am  gear  carb
    ##    <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
    ##  1  21       6  160    110  3.9   2.62  16.5     0     1     4     4
    ##  2  21       6  160    110  3.9   2.88  17.0     0     1     4     4
    ##  3  22.8     4  108     93  3.85  2.32  18.6     1     1     4     1
    ##  4  21.4     6  258    110  3.08  3.22  19.4     1     0     3     1
    ##  5  18.7     8  360    175  3.15  3.44  17.0     0     0     3     2
    ##  6  18.1     6  225    105  2.76  3.46  20.2     1     0     3     1
    ##  7  14.3     8  360    245  3.21  3.57  15.8     0     0     3     4
    ##  8  24.4     4  147.    62  3.69  3.19  20       1     0     4     2
    ##  9  22.8     4  141.    95  3.92  3.15  22.9     1     0     4     2
    ## 10  19.2     6  168.   123  3.92  3.44  18.3     1     0     4     4
    ## # ... with 22 more rows

Tibble version prints a clean 10 rows only and…it says it’s a tibble
lol.

**2. Compare and contrast the following operations on a data.frame and
equivalent tibble. What is different? Why might the default data frame
behaviours cause you frustration?**

``` r
df <- data.frame(abc = 1, xyz = "a")

str(df)
```

    ## 'data.frame':    1 obs. of  2 variables:
    ##  $ abc: num 1
    ##  $ xyz: Factor w/ 1 level "a": 1

``` r
df$x
```

    ## [1] a
    ## Levels: a

``` r
str(df[, "xyz"])
```

    ##  Factor w/ 1 level "a": 1

``` r
str(df[, c("abc", "xyz")])
```

    ## 'data.frame':    1 obs. of  2 variables:
    ##  $ abc: num 1
    ##  $ xyz: Factor w/ 1 level "a": 1

``` r
tib <- tibble(
  abc = 1,
  xyz = "a"
)

str(tib)
```

    ## Classes 'tbl_df', 'tbl' and 'data.frame':    1 obs. of  2 variables:
    ##  $ abc: num 1
    ##  $ xyz: chr "a"

``` r
tib$x
```

    ## NULL

``` r
tib[, "xyz"]
```

    ## # A tibble: 1 x 1
    ##   xyz  
    ##   <chr>
    ## 1 a

``` r
tib[, c("abc", "xyz")]
```

    ## # A tibble: 1 x 2
    ##     abc xyz  
    ##   <dbl> <chr>
    ## 1     1 a

Advantages of the tibble:

  - Does not coerce column xyz to be factor instead of chr (and
    therefore can’t access x through $, a column selector)
  - The bracket subset returns type factor for a single column subset,
    type data frame for the multi-column. The tibble subset always
    returns a tibble.

**3. If you have the name of a variable stored in an object, e.g. var
\<- “mpg”, how can you extract the reference variable from a tibble?**

``` r
var <- "model"

mpg %>% 
  select(var)
```

    ## # A tibble: 234 x 1
    ##    model     
    ##    <chr>     
    ##  1 a4        
    ##  2 a4        
    ##  3 a4        
    ##  4 a4        
    ##  5 a4        
    ##  6 a4        
    ##  7 a4        
    ##  8 a4 quattro
    ##  9 a4 quattro
    ## 10 a4 quattro
    ## # ... with 224 more rows

**4. Practice referring to non-syntactic names in the following data
frame by:**

``` r
annoying <- tibble(
  `1` = 1:10,
  `2` = `1` * 2 + rnorm(length(`1`))
  )
```

  - Extracting the variable called 1.

<!-- end list -->

``` r
annoying %>% select(`1`)
```

    ## # A tibble: 10 x 1
    ##      `1`
    ##    <int>
    ##  1     1
    ##  2     2
    ##  3     3
    ##  4     4
    ##  5     5
    ##  6     6
    ##  7     7
    ##  8     8
    ##  9     9
    ## 10    10

  - Plotting a scatterplot of 1 vs 2.

<!-- end list -->

``` r
annoying %>% 
  ggplot(aes(`1`, `2`)) +
  geom_point()
```

![](tibble_walkthrough_files/figure-gfm/unnamed-chunk-15-1.png)<!-- -->

  - Creating a new column called 3 which is 2 divided by 1.

<!-- end list -->

``` r
annoying <- annoying %>% 
  mutate(`3` = `2` / `1`)
```

  - Renaming the columns to one, two and three.

<!-- end list -->

``` r
colnames(annoying)
```

    ## [1] "1" "2" "3"

``` r
annoying %>% 
  rename(
    one = `1`,
    two = `2`,
    three = `3`
  )
```

    ## # A tibble: 10 x 3
    ##      one    two three
    ##    <int>  <dbl> <dbl>
    ##  1     1  0.203 0.203
    ##  2     2  4.15  2.08 
    ##  3     3  5.23  1.74 
    ##  4     4  9.05  2.26 
    ##  5     5 12.0   2.40 
    ##  6     6 12.6   2.10 
    ##  7     7 12.6   1.81 
    ##  8     8 14.9   1.86 
    ##  9     9 17.6   1.95 
    ## 10    10 20.6   2.06

**5. What does tibble::enframe() do? When might you use it?**

``` r
?enframe
```

enframe() & deframe() do converstions:

  - **Vectors to data frames**

<!-- end list -->

``` r
1:5 %>% enframe()
```

    ## # A tibble: 5 x 2
    ##    name value
    ##   <int> <int>
    ## 1     1     1
    ## 2     2     2
    ## 3     3     3
    ## 4     4     4
    ## 5     5     5

  - **Data frames to vectors**

<!-- end list -->

``` r
tibble(a = 1:5, b = letters[1:5]) %>% deframe()
```

    ##   1   2   3   4   5 
    ## "a" "b" "c" "d" "e"

6.  What option controls how many additional column names are printed at
    the footer of a tibble?

<!-- end list -->

``` r
as_tibble(mpg) %>% print()
```

    ## # A tibble: 234 x 11
    ##    manufacturer model    displ  year   cyl trans   drv     cty   hwy fl    class
    ##    <chr>        <chr>    <dbl> <int> <int> <chr>   <chr> <int> <int> <chr> <chr>
    ##  1 audi         a4         1.8  1999     4 auto(l~ f        18    29 p     comp~
    ##  2 audi         a4         1.8  1999     4 manual~ f        21    29 p     comp~
    ##  3 audi         a4         2    2008     4 manual~ f        20    31 p     comp~
    ##  4 audi         a4         2    2008     4 auto(a~ f        21    30 p     comp~
    ##  5 audi         a4         2.8  1999     6 auto(l~ f        16    26 p     comp~
    ##  6 audi         a4         2.8  1999     6 manual~ f        18    26 p     comp~
    ##  7 audi         a4         3.1  2008     6 auto(a~ f        18    27 p     comp~
    ##  8 audi         a4 quat~   1.8  1999     4 manual~ 4        18    26 p     comp~
    ##  9 audi         a4 quat~   1.8  1999     4 auto(l~ 4        16    25 p     comp~
    ## 10 audi         a4 quat~   2    2008     4 manual~ 4        20    28 p     comp~
    ## # ... with 224 more rows
