Practice for Chapter 5- Data Wrangling
================

  - [filter()](#filter)
  - [arrange()](#arrange)
  - [select()](#select)
  - [mutate()](#mutate)
  - [summarise()](#summarise)
  - [grouped mutate()](#grouped-mutate)

``` r
library(tidyverse)
library(here)
```

``` r
theme_set(theme_light())

knitr::opts_chunk$set(
  cache = FALSE,
  message = FALSE, 
  warning = FALSE, 
  fig.width = 10, 
  fig.height = 7
  )
```

Read in Fifa 19 players datset from
[Kaggle](https://www.kaggle.com/karangadiya/fifa19#data.csv).

``` r
fifa_19_players <- read_csv(here("05-data-wrangling", "fifa-19-players.csv"))
```

# filter()

``` r
fifa_19_players %>% 
  filter((Overall >= 90 | Potential >= 90) & (between(Age, 20, 25)))
```

    ## # A tibble: 24 x 89
    ##       X1     ID Name    Age Photo Nationality Flag  Overall Potential Club 
    ##    <dbl>  <dbl> <chr> <dbl> <chr> <chr>       <chr>   <dbl>     <dbl> <chr>
    ##  1     9 200389 J. O~    25 http~ Slovenia    http~      90        93 Atlé~
    ##  2    15 211110 P. D~    24 http~ Argentina   http~      89        94 Juve~
    ##  3    16 202126 H. K~    24 http~ England     http~      89        91 Tott~
    ##  4    42 205600 S. U~    24 http~ France      http~      87        92 FC B~
    ##  5    43 201399 M. I~    25 http~ Argentina   http~      87        90 Inter
    ##  6    45 195864 P. P~    25 http~ France      http~      87        91 Manc~
    ##  7    55 222492 L. S~    22 http~ Germany     http~      86        92 Manc~
    ##  8    56 218667 Bern~    23 http~ Portugal    http~      86        91 Manc~
    ##  9    57 210257 Eder~    24 http~ Brazil      http~      86        90 Manc~
    ## 10    62 201535 R. V~    25 http~ France      http~      86        91 Real~
    ## # ... with 14 more rows, and 79 more variables: `Club Logo` <chr>, Value <chr>,
    ## #   Wage <chr>, Special <dbl>, `Preferred Foot` <chr>, `International
    ## #   Reputation` <dbl>, `Weak Foot` <dbl>, `Skill Moves` <dbl>, `Work
    ## #   Rate` <chr>, `Body Type` <chr>, `Real Face` <chr>, Position <chr>, `Jersey
    ## #   Number` <dbl>, Joined <chr>, `Loaned From` <chr>, `Contract Valid
    ## #   Until` <chr>, Height <chr>, Weight <chr>, LS <chr>, ST <chr>, RS <chr>,
    ## #   LW <chr>, LF <chr>, CF <chr>, RF <chr>, RW <chr>, LAM <chr>, CAM <chr>,
    ## #   RAM <chr>, LM <chr>, LCM <chr>, CM <chr>, RCM <chr>, RM <chr>, LWB <chr>,
    ## #   LDM <chr>, CDM <chr>, RDM <chr>, RWB <chr>, LB <chr>, LCB <chr>, CB <chr>,
    ## #   RCB <chr>, RB <chr>, Crossing <dbl>, Finishing <dbl>,
    ## #   HeadingAccuracy <dbl>, ShortPassing <dbl>, Volleys <dbl>, Dribbling <dbl>,
    ## #   Curve <dbl>, FKAccuracy <dbl>, LongPassing <dbl>, BallControl <dbl>,
    ## #   Acceleration <dbl>, SprintSpeed <dbl>, Agility <dbl>, Reactions <dbl>,
    ## #   Balance <dbl>, ShotPower <dbl>, Jumping <dbl>, Stamina <dbl>,
    ## #   Strength <dbl>, LongShots <dbl>, Aggression <dbl>, Interceptions <dbl>,
    ## #   Positioning <dbl>, Vision <dbl>, Penalties <dbl>, Composure <dbl>,
    ## #   Marking <dbl>, StandingTackle <dbl>, SlidingTackle <dbl>, GKDiving <dbl>,
    ## #   GKHandling <dbl>, GKKicking <dbl>, GKPositioning <dbl>, GKReflexes <dbl>,
    ## #   `Release Clause` <chr>

# arrange()

# select()

# mutate()

# summarise()

# grouped mutate()
