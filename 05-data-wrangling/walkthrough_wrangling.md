Walkthrough for Chapter 5- Data Wrangling
================

  - [Intro](#intro)
  - [filter()](#filter)
      - [Exercises](#exercises)
  - [arrange()](#arrange)
      - [Exercises](#exercises-1)
  - [select()](#select)
      - [Exercises](#exercises-2)
  - [mutate()](#mutate)
  - [summarise()](#summarise)
  - [grouped mutate (and filters)](#grouped-mutate-and-filters)

``` r
library(tidyverse)
```

    ## -- Attaching packages -------------------------- tidyverse 1.2.1 --

    ## v ggplot2 3.2.1     v purrr   0.3.3
    ## v tibble  2.1.3     v dplyr   0.8.3
    ## v tidyr   1.0.0     v stringr 1.4.0
    ## v readr   1.3.1     v forcats 0.4.0

    ## -- Conflicts ----------------------------- tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library(nycflights13)

theme_set(theme_light())

knitr::opts_chunk$set(
  cache = FALSE,
  message = FALSE, 
  warning = FALSE, 
  fig.width = 10, 
  fig.height = 7
  )
```

# Intro

Using `nycflights13::flights` dataset.

``` r
flights %>% 
  head(5)
```

    ## # A tibble: 5 x 19
    ##    year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
    ##   <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
    ## 1  2013     1     1      517            515         2      830            819
    ## 2  2013     1     1      533            529         4      850            830
    ## 3  2013     1     1      542            540         2      923            850
    ## 4  2013     1     1      544            545        -1     1004           1022
    ## 5  2013     1     1      554            600        -6      812            837
    ## # ... with 11 more variables: arr_delay <dbl>, carrier <chr>, flight <int>,
    ## #   tailnum <chr>, origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>,
    ## #   hour <dbl>, minute <dbl>, time_hour <dttm>

# filter()

Use an `&` filter by just adding multiple conditions.

``` r
flights %>% 
  filter(month == 1, day == 1)
```

    ## # A tibble: 842 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
    ##  1  2013     1     1      517            515         2      830            819
    ##  2  2013     1     1      533            529         4      850            830
    ##  3  2013     1     1      542            540         2      923            850
    ##  4  2013     1     1      544            545        -1     1004           1022
    ##  5  2013     1     1      554            600        -6      812            837
    ##  6  2013     1     1      554            558        -4      740            728
    ##  7  2013     1     1      555            600        -5      913            854
    ##  8  2013     1     1      557            600        -3      709            723
    ##  9  2013     1     1      557            600        -3      838            846
    ## 10  2013     1     1      558            600        -2      753            745
    ## # ... with 832 more rows, and 11 more variables: arr_delay <dbl>,
    ## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
    ## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

Have to assign to actually save the new data frame

``` r
dec_25 <- flights %>% filter(month == 12, day == 25)
```

The comparisons to use are `>`, `>=`, `<`, `<=`, `!=`, and `==`

Logical operators like `&` and `|`, and `%in%` are also used.

``` r
flights %>% 
  filter(month %in% c(11, 12))
```

    ## # A tibble: 55,403 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
    ##  1  2013    11     1        5           2359         6      352            345
    ##  2  2013    11     1       35           2250       105      123           2356
    ##  3  2013    11     1      455            500        -5      641            651
    ##  4  2013    11     1      539            545        -6      856            827
    ##  5  2013    11     1      542            545        -3      831            855
    ##  6  2013    11     1      549            600       -11      912            923
    ##  7  2013    11     1      550            600       -10      705            659
    ##  8  2013    11     1      554            600        -6      659            701
    ##  9  2013    11     1      554            600        -6      826            827
    ## 10  2013    11     1      554            600        -6      749            751
    ## # ... with 55,393 more rows, and 11 more variables: arr_delay <dbl>,
    ## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
    ## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

When an `NA` value is involved in a filter, the result will almost
always be `NA` as well

``` r
NA > 5
```

    ## [1] NA

``` r
NA + 10
```

    ## [1] NA

These operations make sense when we consider adding a known and an
unknown; the result will also be unknown\!

## Exercises

1.  Find all flights that

<!-- end list -->

  - Had an arrival delay of two or more hours

<!-- end list -->

``` r
flights %>% 
  filter(arr_delay <= 120)
```

    ## # A tibble: 317,312 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
    ##  1  2013     1     1      517            515         2      830            819
    ##  2  2013     1     1      533            529         4      850            830
    ##  3  2013     1     1      542            540         2      923            850
    ##  4  2013     1     1      544            545        -1     1004           1022
    ##  5  2013     1     1      554            600        -6      812            837
    ##  6  2013     1     1      554            558        -4      740            728
    ##  7  2013     1     1      555            600        -5      913            854
    ##  8  2013     1     1      557            600        -3      709            723
    ##  9  2013     1     1      557            600        -3      838            846
    ## 10  2013     1     1      558            600        -2      753            745
    ## # ... with 317,302 more rows, and 11 more variables: arr_delay <dbl>,
    ## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
    ## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

  - Flew to Houston (IAH or HOU)

<!-- end list -->

``` r
flights %>% 
  filter(dest %in% c("IAH", "HOU"))
```

    ## # A tibble: 9,313 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
    ##  1  2013     1     1      517            515         2      830            819
    ##  2  2013     1     1      533            529         4      850            830
    ##  3  2013     1     1      623            627        -4      933            932
    ##  4  2013     1     1      728            732        -4     1041           1038
    ##  5  2013     1     1      739            739         0     1104           1038
    ##  6  2013     1     1      908            908         0     1228           1219
    ##  7  2013     1     1     1028           1026         2     1350           1339
    ##  8  2013     1     1     1044           1045        -1     1352           1351
    ##  9  2013     1     1     1114            900       134     1447           1222
    ## 10  2013     1     1     1205           1200         5     1503           1505
    ## # ... with 9,303 more rows, and 11 more variables: arr_delay <dbl>,
    ## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
    ## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

  - Departed between midnight and 6am (inclusive)

<!-- end list -->

``` r
flights %>% 
  filter(dep_time >= 0 & dep_time <= 600)
```

    ## # A tibble: 9,344 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
    ##  1  2013     1     1      517            515         2      830            819
    ##  2  2013     1     1      533            529         4      850            830
    ##  3  2013     1     1      542            540         2      923            850
    ##  4  2013     1     1      544            545        -1     1004           1022
    ##  5  2013     1     1      554            600        -6      812            837
    ##  6  2013     1     1      554            558        -4      740            728
    ##  7  2013     1     1      555            600        -5      913            854
    ##  8  2013     1     1      557            600        -3      709            723
    ##  9  2013     1     1      557            600        -3      838            846
    ## 10  2013     1     1      558            600        -2      753            745
    ## # ... with 9,334 more rows, and 11 more variables: arr_delay <dbl>,
    ## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
    ## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

2.  Another useful dplyr filtering helper is between(). What does it do?
    Can you use it to simplify the code needed to answer the previous
    challenges?

<!-- end list -->

``` r
flights %>% 
  filter(between(dep_time, 0, 600))
```

    ## # A tibble: 9,344 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
    ##  1  2013     1     1      517            515         2      830            819
    ##  2  2013     1     1      533            529         4      850            830
    ##  3  2013     1     1      542            540         2      923            850
    ##  4  2013     1     1      544            545        -1     1004           1022
    ##  5  2013     1     1      554            600        -6      812            837
    ##  6  2013     1     1      554            558        -4      740            728
    ##  7  2013     1     1      555            600        -5      913            854
    ##  8  2013     1     1      557            600        -3      709            723
    ##  9  2013     1     1      557            600        -3      838            846
    ## 10  2013     1     1      558            600        -2      753            745
    ## # ... with 9,334 more rows, and 11 more variables: arr_delay <dbl>,
    ## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
    ## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

3.  How many flights have a missing dep\_time? What other variables are
    missing? What might these rows represent?

<!-- end list -->

``` r
flights %>% 
  filter(is.na(dep_time))
```

    ## # A tibble: 8,255 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
    ##  1  2013     1     1       NA           1630        NA       NA           1815
    ##  2  2013     1     1       NA           1935        NA       NA           2240
    ##  3  2013     1     1       NA           1500        NA       NA           1825
    ##  4  2013     1     1       NA            600        NA       NA            901
    ##  5  2013     1     2       NA           1540        NA       NA           1747
    ##  6  2013     1     2       NA           1620        NA       NA           1746
    ##  7  2013     1     2       NA           1355        NA       NA           1459
    ##  8  2013     1     2       NA           1420        NA       NA           1644
    ##  9  2013     1     2       NA           1321        NA       NA           1536
    ## 10  2013     1     2       NA           1545        NA       NA           1910
    ## # ... with 8,245 more rows, and 11 more variables: arr_delay <dbl>,
    ## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
    ## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

4.  Why is NA ^ 0 not missing? Why is NA | TRUE not missing? Why is
    FALSE & NA not missing? Can you figure out the general rule? (NA \*
    0 is a tricky counterexample\!)

<!-- end list -->

``` r
NA ^ 0 # anything to the 0th power equals 1
```

    ## [1] 1

``` r
NA | TRUE # anything or TRUE has to be TRUE
```

    ## [1] TRUE

``` r
FALSE & NA # anything and false has to be FALSE
```

    ## [1] FALSE

# arrange()

`arrange()` allows us to order rows based on values.

``` r
flights %>% 
  arrange(year)
```

    ## # A tibble: 336,776 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
    ##  1  2013     1     1      517            515         2      830            819
    ##  2  2013     1     1      533            529         4      850            830
    ##  3  2013     1     1      542            540         2      923            850
    ##  4  2013     1     1      544            545        -1     1004           1022
    ##  5  2013     1     1      554            600        -6      812            837
    ##  6  2013     1     1      554            558        -4      740            728
    ##  7  2013     1     1      555            600        -5      913            854
    ##  8  2013     1     1      557            600        -3      709            723
    ##  9  2013     1     1      557            600        -3      838            846
    ## 10  2013     1     1      558            600        -2      753            745
    ## # ... with 336,766 more rows, and 11 more variables: arr_delay <dbl>,
    ## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
    ## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

``` r
flights %>% 
  arrange(year, month, day)
```

    ## # A tibble: 336,776 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
    ##  1  2013     1     1      517            515         2      830            819
    ##  2  2013     1     1      533            529         4      850            830
    ##  3  2013     1     1      542            540         2      923            850
    ##  4  2013     1     1      544            545        -1     1004           1022
    ##  5  2013     1     1      554            600        -6      812            837
    ##  6  2013     1     1      554            558        -4      740            728
    ##  7  2013     1     1      555            600        -5      913            854
    ##  8  2013     1     1      557            600        -3      709            723
    ##  9  2013     1     1      557            600        -3      838            846
    ## 10  2013     1     1      558            600        -2      753            745
    ## # ... with 336,766 more rows, and 11 more variables: arr_delay <dbl>,
    ## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
    ## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

Use `desc()` to sort in…descending order\!

``` r
flights %>% 
  arrange(desc(month))
```

    ## # A tibble: 336,776 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
    ##  1  2013    12     1       13           2359        14      446            445
    ##  2  2013    12     1       17           2359        18      443            437
    ##  3  2013    12     1      453            500        -7      636            651
    ##  4  2013    12     1      520            515         5      749            808
    ##  5  2013    12     1      536            540        -4      845            850
    ##  6  2013    12     1      540            550       -10     1005           1027
    ##  7  2013    12     1      541            545        -4      734            755
    ##  8  2013    12     1      546            545         1      826            835
    ##  9  2013    12     1      549            600       -11      648            659
    ## 10  2013    12     1      550            600       -10      825            854
    ## # ... with 336,766 more rows, and 11 more variables: arr_delay <dbl>,
    ## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
    ## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

Missing values are always sorted to the end

``` r
tibble(x = c(1:5, NA)) %>% 
  arrange(x)
```

    ## # A tibble: 6 x 1
    ##       x
    ##   <int>
    ## 1     1
    ## 2     2
    ## 3     3
    ## 4     4
    ## 5     5
    ## 6    NA

## Exercises

1.  How could you use arrange() to sort all missing values to the start?
    (Hint: use is.na()).

<!-- end list -->

``` r
tibble(x = c(1:5, NA, 6, NA)) %>% 
  arrange(desc(is.na(x)))
```

    ## # A tibble: 8 x 1
    ##       x
    ##   <dbl>
    ## 1    NA
    ## 2    NA
    ## 3     1
    ## 4     2
    ## 5     3
    ## 6     4
    ## 7     5
    ## 8     6

2.  Sort flights to find the most delayed flights. Find the flights that
    left earliest.

<!-- end list -->

``` r
flights %>% 
  arrange(desc(dep_delay)) %>% 
  select(dep_delay)
```

    ## # A tibble: 336,776 x 1
    ##    dep_delay
    ##        <dbl>
    ##  1      1301
    ##  2      1137
    ##  3      1126
    ##  4      1014
    ##  5      1005
    ##  6       960
    ##  7       911
    ##  8       899
    ##  9       898
    ## 10       896
    ## # ... with 336,766 more rows

# select()

Select columns\!

``` r
flights %>% 
  select(year, month, day)
```

    ## # A tibble: 336,776 x 3
    ##     year month   day
    ##    <int> <int> <int>
    ##  1  2013     1     1
    ##  2  2013     1     1
    ##  3  2013     1     1
    ##  4  2013     1     1
    ##  5  2013     1     1
    ##  6  2013     1     1
    ##  7  2013     1     1
    ##  8  2013     1     1
    ##  9  2013     1     1
    ## 10  2013     1     1
    ## # ... with 336,766 more rows

Use helper functions like:

  - `starts_with()`
  - `ends_with()`
  - `contains()`
  - `matches()`- reg expressions
  - `num_range()`- `num_range("x", 1:3)` would reurn x1, x2, x3

`rename()` is a variant of select and returns all columns

``` r
flights %>% 
  rename(Year = year)
```

    ## # A tibble: 336,776 x 19
    ##     Year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
    ##  1  2013     1     1      517            515         2      830            819
    ##  2  2013     1     1      533            529         4      850            830
    ##  3  2013     1     1      542            540         2      923            850
    ##  4  2013     1     1      544            545        -1     1004           1022
    ##  5  2013     1     1      554            600        -6      812            837
    ##  6  2013     1     1      554            558        -4      740            728
    ##  7  2013     1     1      555            600        -5      913            854
    ##  8  2013     1     1      557            600        -3      709            723
    ##  9  2013     1     1      557            600        -3      838            846
    ## 10  2013     1     1      558            600        -2      753            745
    ## # ... with 336,766 more rows, and 11 more variables: arr_delay <dbl>,
    ## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
    ## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

`everything()` is a nice select helper, especially when you want to move
a few columns to the front

``` r
flights %>% 
  select(origin, everything())
```

    ## # A tibble: 336,776 x 19
    ##    origin  year month   day dep_time sched_dep_time dep_delay arr_time
    ##    <chr>  <int> <int> <int>    <int>          <int>     <dbl>    <int>
    ##  1 EWR     2013     1     1      517            515         2      830
    ##  2 LGA     2013     1     1      533            529         4      850
    ##  3 JFK     2013     1     1      542            540         2      923
    ##  4 JFK     2013     1     1      544            545        -1     1004
    ##  5 LGA     2013     1     1      554            600        -6      812
    ##  6 EWR     2013     1     1      554            558        -4      740
    ##  7 EWR     2013     1     1      555            600        -5      913
    ##  8 LGA     2013     1     1      557            600        -3      709
    ##  9 JFK     2013     1     1      557            600        -3      838
    ## 10 LGA     2013     1     1      558            600        -2      753
    ## # ... with 336,766 more rows, and 11 more variables: sched_arr_time <int>,
    ## #   arr_delay <dbl>, carrier <chr>, flight <int>, tailnum <chr>, dest <chr>,
    ## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

## Exercises

# mutate()

# summarise()

# grouped mutate (and filters)
