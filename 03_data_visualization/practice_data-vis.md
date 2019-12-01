Self-learning for Chapter 3- Data Visualization
================

  - [Basic scatterplot](#basic-scatterplot)
  - [Plot an aesthetic corresponding to another
    variable.](#plot-an-aesthetic-corresponding-to-another-variable.)
  - [Plot a manual aesthetic](#plot-a-manual-aesthetic)
  - [Facet by a third variable](#facet-by-a-third-variable)
  - [Use two different geom()’s](#use-two-different-geoms)
  - [Use a geom() that uses stat.
    transformations](#use-a-geom-that-uses-stat.-transformations)
  - [Use a positional adjustment in
    geom\_boxplot()](#use-a-positional-adjustment-in-geom_boxplot)
  - [Use coord\_flip() and
    coord\_polar()](#use-coord_flip-and-coord_polar)

``` r
library(tidyverse)
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

``` r
air_incidents <- read_csv("https://raw.githubusercontent.com/fivethirtyeight/data/master/airline-safety/airline-safety.csv") 
```

# Basic scatterplot

``` r
air_incidents %>% 
  ggplot(aes(fatal_accidents_85_99, fatalities_85_99)) +
  geom_point()
```

![](data_visualization_self_learn_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

# Plot an aesthetic corresponding to another variable.

``` r
air_incidents %>% 
  ggplot(aes(fatal_accidents_85_99, fatalities_85_99, size = avail_seat_km_per_week)) +
  geom_point()
```

![](data_visualization_self_learn_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

# Plot a manual aesthetic

``` r
air_incidents %>% 
  ggplot(aes(fatal_accidents_85_99, fatalities_85_99, size = avail_seat_km_per_week)) +
  geom_point(color = "purple")
```

![](data_visualization_self_learn_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

# Facet by a third variable

``` r
air_incidents %>% 
  filter(airline %in% c("Southwest Airlines",
                        "Alaska Airlines*",
                        "American*")) %>% 
  ggplot(aes(avail_seat_km_per_week, fatalities_85_99)) +
  geom_point() +
  facet_wrap(~ airline)
```

![](data_visualization_self_learn_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

# Use two different geom()’s

``` r
air_incidents %>% 
  ggplot(aes(incidents_85_99, incidents_00_14)) +
  geom_point() +
  geom_smooth(se = FALSE)
```

![](data_visualization_self_learn_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->

# Use a geom() that uses stat. transformations

``` r
air_incidents %>% 
  arrange(desc(avail_seat_km_per_week)) %>% 
  slice(1:5) %>% 
  ggplot(aes(airline, avail_seat_km_per_week)) +
  geom_col()
```

![](data_visualization_self_learn_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->

This dataset already had precomputed values, but could’ve used
geom\_bar() if it was in a more raw data-like form.

# Use a positional adjustment in geom\_boxplot()

``` r
air_incidents %>% 
  filter(airline %in% c("American*", "Southwest Airlines", "Air Canada")) %>% 
  ggplot(aes(airline, avail_seat_km_per_week)) +
  geom_boxplot(position = "dodge")
```

![](data_visualization_self_learn_files/figure-gfm/unnamed-chunk-9-1.png)<!-- -->

This would work if data was raw and each row was a flight with that
flight’s available seats

# Use coord\_flip() and coord\_polar()

``` r
air_incidents %>% 
  filter(airline %in% c("American*", "Southwest Airlines", "Air Canada")) %>% 
  ggplot(aes(airline, avail_seat_km_per_week)) +
  geom_boxplot(position = "dodge") +
  coord_flip()
```

![](data_visualization_self_learn_files/figure-gfm/unnamed-chunk-10-1.png)<!-- -->
