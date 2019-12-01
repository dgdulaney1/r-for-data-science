Walkthrough for Chapter 3- Data Visualization
================

  - [3.2- First steps](#first-steps)
      - [Exercises](#exercises)
  - [3.3- Aesthetic mappings](#aesthetic-mappings)
      - [Exercises](#exercises-1)
  - [3.5- Facets](#facets)
  - [3.6- Geometric objects](#geometric-objects)
      - [Exercises](#exercises-2)
  - [3.7- Statistical transformations](#statistical-transformations)
  - [3.8- Position adjustments](#position-adjustments)
  - [3.9- Coordinate systems](#coordinate-systems)
  - [3.10- Layered grammar of graphics](#layered-grammar-of-graphics)

``` r
library(tidyverse)
```

    ## -- Attaching packages ------------------------------------------------------------------ tidyverse 1.2.1 --

    ## v ggplot2 3.2.1     v purrr   0.3.3
    ## v tibble  2.1.3     v dplyr   0.8.3
    ## v tidyr   1.0.0     v stringr 1.4.0
    ## v readr   1.3.1     v forcats 0.4.0

    ## -- Conflicts --------------------------------------------------------------------- tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

# 3.2- First steps

Basic scatter plot

``` r
mpg %>% 
  ggplot() +
  geom_point(aes(displ, hwy))
```

![](data_visualization_walkthrough_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->

## Exercises

1.  Run ggplot(data = mpg). What do you see?

<!-- end list -->

``` r
mpg %>% 
  ggplot()
```

![](data_visualization_walkthrough_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->
Empty plot template

2.  How many rows are in mpg? How many columns?

<!-- end list -->

``` r
nrow(mpg)
```

    ## [1] 234

``` r
ncol(mpg)
```

    ## [1] 11

``` r
dim(mpg)
```

    ## [1] 234  11

3.  What does the drv variable describe? Read the help for ?mpg to find
    out.

<!-- end list -->

``` r
?mpg
```

    ## starting httpd help server ... done

4.  Make a scatterplot of hwy vs cyl.

<!-- end list -->

``` r
mpg %>% 
  ggplot(aes(hwy, cyl)) +
  geom_point()
```

![](data_visualization_walkthrough_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

5.  What happens if you make a scatterplot of class vs drv? Why is the
    plot not useful?

<!-- end list -->

``` r
mpg %>% 
  ggplot(aes(class, drv)) +
  geom_point()
```

![](data_visualization_walkthrough_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->

Uhhhh no.

-----

# 3.3- Aesthetic mappings

To assign an aesthetic to the points, include the aesthetic type inside
aes()

``` r
mpg %>% 
  ggplot() +
  geom_point(aes(displ, hwy, color = class))
```

![](data_visualization_walkthrough_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->

``` r
mpg %>% 
  ggplot(aes(displ, hwy, size = class)) +
  geom_point()
```

    ## Warning: Using size for a discrete variable is not advised.

![](data_visualization_walkthrough_files/figure-gfm/unnamed-chunk-9-1.png)<!-- -->

``` r
mpg %>% 
  ggplot(aes(displ, hwy, alpha = class)) +
  geom_point()
```

    ## Warning: Using alpha for a discrete variable is not advised.

![](data_visualization_walkthrough_files/figure-gfm/unnamed-chunk-10-1.png)<!-- -->

``` r
mpg %>% 
  ggplot(aes(displ, hwy, shape = class)) +
  geom_point()
```

    ## Warning: The shape palette can deal with a maximum of 6 discrete values because
    ## more than 6 becomes difficult to discriminate; you have 7. Consider
    ## specifying shapes manually if you must have them.

    ## Warning: Removed 62 rows containing missing values (geom_point).

![](data_visualization_walkthrough_files/figure-gfm/unnamed-chunk-11-1.png)<!-- -->

To assign a manual aesthetic that doesn’t convey info about a variable,
place the aesthetic outside aes()

``` r
mpg %>% 
  ggplot(aes(displ, hwy)) +
  geom_point(color = "blue")
```

![](data_visualization_walkthrough_files/figure-gfm/unnamed-chunk-12-1.png)<!-- -->

## Exercises

1.  What’s gone wrong with this code? Why are the points not blue?

<!-- end list -->

``` r
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy, color = "blue"))
```

![](data_visualization_walkthrough_files/figure-gfm/unnamed-chunk-13-1.png)<!-- -->

The manually assigned aesthetic is inside aes() and so it’s looking for
variable information about “blue”

3.  Map a continuous variable to color, size, and shape. How do these
    aesthetics behave differently for categorical vs. continuous
    variables?

<!-- end list -->

``` r
mpg %>%
  ggplot(aes(displ, hwy, color = cty)) +
  geom_point()
```

![](data_visualization_walkthrough_files/figure-gfm/unnamed-chunk-14-1.png)<!-- -->

Color and shape are on a scale, shape can’t be done.

4.  What happens if you map the same variable to multiple aesthetics?

<!-- end list -->

``` r
mpg %>% 
  ggplot(aes(hwy, hwy)) +
  geom_point()
```

![](data_visualization_walkthrough_files/figure-gfm/unnamed-chunk-15-1.png)<!-- -->

It works\! But is useless.

5.  What does the stroke aesthetic do? What shapes does it work with?
    (Hint: use ?geom\_point)

6.  What happens if you map an aesthetic to something other than a
    variable name, like aes(colour = displ \< 5)? Note, you’ll also need
    to specify x and y.

<!-- end list -->

``` r
mpg %>% 
  ggplot(aes(displ, hwy, color = displ < 5)) +
  geom_point()
```

![](data_visualization_walkthrough_files/figure-gfm/unnamed-chunk-17-1.png)<!-- -->

Creates a binary TRUE/FALSE variable based on the condition provided.

-----

# 3.5- Facets

Facet by another variable with facet\_wrap()

``` r
mpg %>% 
  ggplot(aes(displ, hwy)) +
  geom_point() +
  facet_wrap(~ class, nrow = 2)
```

![](data_visualization_walkthrough_files/figure-gfm/unnamed-chunk-18-1.png)<!-- -->

Facet by 2 variables with facet\_grid()

``` r
mpg %>% 
  ggplot(aes(displ, hwy)) +
  geom_point() +
  facet_grid(drv ~ cyl)
```

![](data_visualization_walkthrough_files/figure-gfm/unnamed-chunk-19-1.png)<!-- -->

-----

# 3.6- Geometric objects

Geoms are used to place objects of different types onto a plot.

``` r
mpg %>% 
  ggplot() +
  geom_point(aes(displ, hwy))
```

![](data_visualization_walkthrough_files/figure-gfm/unnamed-chunk-20-1.png)<!-- -->

``` r
mpg %>% 
  ggplot() +
  geom_smooth(aes(displ, hwy))
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](data_visualization_walkthrough_files/figure-gfm/unnamed-chunk-21-1.png)<!-- -->

Change the object by adding an object characteristic (e.g. color, size,
shape) inside aes()

``` r
mpg %>% 
  ggplot() +
  geom_smooth(aes(displ, hwy, linetype = drv))
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](data_visualization_walkthrough_files/figure-gfm/unnamed-chunk-22-1.png)<!-- -->

``` r
mpg %>% 
  ggplot(aes(displ, hwy, color = drv)) +
  geom_point() +
  geom_smooth(aes(linetype = drv))
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](data_visualization_walkthrough_files/figure-gfm/unnamed-chunk-23-1.png)<!-- -->

Note that using aesthetics in ggplot() will apply those to every
geom\_\*() function in the chain.

This insinuates that using different arguments in different geoms allows
lots of flexibility

``` r
ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) +
  geom_point(aes(color = class)) +
  geom_smooth(data = filter(mpg, class == "subcompact"), se = FALSE)
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](data_visualization_walkthrough_files/figure-gfm/unnamed-chunk-24-1.png)<!-- -->

## Exercises

1.  What geom would you use to draw a line chart? A boxplot? A
    histogram? An area chart?

<!-- end list -->

``` r
geom_line()
```

    ## geom_line: na.rm = FALSE
    ## stat_identity: na.rm = FALSE
    ## position_identity

``` r
geom_boxplot()
```

    ## geom_boxplot: outlier.colour = NULL, outlier.fill = NULL, outlier.shape = 19, outlier.size = 1.5, outlier.stroke = 0.5, outlier.alpha = NULL, notch = FALSE, notchwidth = 0.5, varwidth = FALSE, na.rm = FALSE
    ## stat_boxplot: na.rm = FALSE
    ## position_dodge2

``` r
geom_histogram()
```

    ## geom_bar: na.rm = FALSE
    ## stat_bin: binwidth = NULL, bins = NULL, na.rm = FALSE, pad = FALSE
    ## position_stack

``` r
geom_area()
```

    ## geom_area: na.rm = FALSE
    ## stat_identity: na.rm = FALSE
    ## position_stack

2.  Run this code in your head and predict what the output will look
    like. Then, run the code in R and check your predictions.

<!-- end list -->

``` r
ggplot(data = mpg, mapping = aes(x = displ, y = hwy, color = drv)) + 
      geom_point() + 
      geom_smooth(se = FALSE)
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](data_visualization_walkthrough_files/figure-gfm/unnamed-chunk-26-1.png)<!-- -->

3.  What does show.legend = FALSE do?

Dunno, just use

``` r
theme(legend.position = "none")
```

    ## List of 1
    ##  $ legend.position: chr "none"
    ##  - attr(*, "class")= chr [1:2] "theme" "gg"
    ##  - attr(*, "complete")= logi FALSE
    ##  - attr(*, "validate")= logi TRUE

4.  What does the se argument to geom\_smooth() do?

Removes error bars

5.  Will these two graphs look different? Why/why not?

ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) + geom\_point() +
geom\_smooth()

ggplot() + geom\_point(data = mpg, mapping = aes(x = displ, y = hwy)) +
geom\_smooth(data = mpg, mapping = aes(x = displ, y = hwy))

Nope, inside ggplot() means inside all geom()’s

6.Recreate the R code necessary to generate the following graphs.

``` r
mpg %>% 
  ggplot(aes(displ, hwy)) +
  geom_point() +
  geom_smooth(se = FALSE)
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](data_visualization_walkthrough_files/figure-gfm/unnamed-chunk-28-1.png)<!-- -->

``` r
mpg %>% 
  ggplot(aes(displ, hwy)) +
  geom_point() +
  geom_smooth(aes(group = drv), se = FALSE)
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](data_visualization_walkthrough_files/figure-gfm/unnamed-chunk-29-1.png)<!-- -->

``` r
mpg %>% 
  ggplot(aes(displ, hwy, color = drv)) +
  geom_point() +
  geom_smooth(se = FALSE)
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](data_visualization_walkthrough_files/figure-gfm/unnamed-chunk-30-1.png)<!-- -->

``` r
mpg %>% 
  ggplot(aes(displ, hwy)) +
  geom_point(aes(color = drv)) +
  geom_smooth(se = FALSE)
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](data_visualization_walkthrough_files/figure-gfm/unnamed-chunk-31-1.png)<!-- -->

``` r
mpg %>% 
  ggplot(aes(displ, hwy)) +
  geom_point(aes(color = drv)) + 
  geom_smooth(aes(linetype = drv), se = FALSE)
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](data_visualization_walkthrough_files/figure-gfm/unnamed-chunk-32-1.png)<!-- -->

-----

# 3.7- Statistical transformations

-----

# 3.8- Position adjustments

-----

# 3.9- Coordinate systems

-----

# 3.10- Layered grammar of graphics
