viz_2
================
Nicole Lewis
2026-10-06

``` r
library(tidyverse)
```

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.2.1     ✔ readr     2.2.0
    ## ✔ forcats   1.0.1     ✔ stringr   1.6.0
    ## ✔ ggplot2   4.0.3     ✔ tibble    3.3.1
    ## ✔ lubridate 1.9.5     ✔ tidyr     1.3.2
    ## ✔ purrr     1.2.2     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

``` r
library(patchwork)
library(dplyr)
```

## Load the weather data

``` r
library(p8105.datasets)
data("weather_df")
```

## Remember this plot..?

``` r
weather_df |> 
  ggplot(aes(x = tmin, y = tmax)) + 
  geom_point(aes(color = name), alpha = .5)
```

    ## Warning: Removed 17 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](viz_2_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

## Labels

``` r
weather_df |> 
  ggplot(aes(x = tmin, y = tmax)) + 
  geom_point(aes(color = name), alpha = .5) +
  labs(
    title = "Temperature plot",
    x = "Minimum daily temperature (C)",
    y = "Maximum daily temperature (C)", 
    color = "Location",
    caption = "Data from the rnoaa package; temperatures in 2017."
  )
```

    ## Warning: Removed 17 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](viz_2_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

## Scales

Start with the same plot; x and y scales

X axis scale

``` r
weather_df |> 
  ggplot(aes(x = tmin, y = tmax)) + 
  geom_point(aes(color = name), alpha = .5) +
  labs(
    title = "Temperature plot",
    x = "Minimum daily temperature (C)",
    y = "Maximum daily temperature (C)", 
    color = "Location",
    caption = "Data from the rnoaa package; temperatures in 2017."
  ) + 
  scale_x_continuous(
    breaks = c(-15, 0, 15),
    labels = c("-15 ºC", "0", "15")
  )
```

    ## Warning: Removed 17 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](viz_2_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

Adding y axis scale

``` r
weather_df |> 
  ggplot(aes(x = tmin, y = tmax)) + 
  geom_point(aes(color = name), alpha = .5) +
  labs(
    title = "Temperature plot",
    x = "Minimum daily temperature (C)",
    y = "Maximum daily temperature (C)", 
    color = "Location",
    caption = "Data from the rnoaa package; temperatures in 2017."
  ) + 
  scale_x_continuous(
    breaks = c(-15, 0, 15),
    labels = c("-15 ºC", "0", "15"), 
    limits = c(-20, 30)
  ) +
  scale_y_continuous(
    trans = "sqrt", 
    position = "right"
  )
```

    ## Warning in transformation$transform(x): NaNs produced

    ## Warning in scale_y_continuous(trans = "sqrt", position = "right"): sqrt
    ## transformation introduced infinite values.

    ## Warning: Removed 142 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](viz_2_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

Look at colour scales

``` r
weather_df |> 
  ggplot(aes(x = tmin, y = tmax)) + 
  geom_point(aes(color = name), alpha = .5) +
  labs(
    title = "Temperature plot",
    x = "Minimum daily temperature (C)",
    y = "Maximum daily temperature (C)", 
    caption = "Data from the rnoaa package; temperatures in 2017."
  ) +
  scale_color_hue(
    name = "Location",  
    h = c(100, 300))
```

    ## Warning: Removed 17 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](viz_2_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->

Viridis package:

``` r
ggp_temp_plot = 
weather_df |> 
  ggplot(aes(x = tmin, y = tmax)) + 
  geom_point(aes(color = name), alpha = .5) +
  labs(
    title = "Temperature plot",
    x = "Minimum daily temperature (C)",
    y = "Maximum daily temperature (C)", 
    caption = "Data from the rnoaa package; temperatures in 2017."
  ) +
 viridis:: scale_color_viridis(
   name = "Location",
   discrete = TRUE)
```

## Themes

Themes are used to modify non-data elements of a plot (ie. controls
things like background color and location of the the legend)

Shift the legend

``` r
weather_df |> 
  ggplot(aes(x = tmin, y = tmax)) + 
  geom_point(aes(color = name), alpha = .5) +
  labs(
    title = "Temperature plot",
    x = "Minimum daily temperature (C)",
    y = "Maximum daily temperature (C)", 
    caption = "Data from the rnoaa package; temperatures in 2017."
  ) +
 viridis:: scale_color_viridis(
   name = "Location",
   discrete = TRUE) +
  theme(legend.position = "bottom")
```

    ## Warning: Removed 17 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](viz_2_files/figure-gfm/unnamed-chunk-9-1.png)<!-- -->

Change the overall theme

``` r
weather_df |> 
  ggplot(aes(x = tmin, y = tmax)) + 
  geom_point(aes(color = name), alpha = .5) +
  labs(
    title = "Temperature plot",
    x = "Minimum daily temperature (C)",
    y = "Maximum daily temperature (C)", 
    caption = "Data from the rnoaa package; temperatures in 2017."
  ) +
 viridis:: scale_color_viridis(
   name = "Location",
   discrete = TRUE) +
  theme_minimal() + 
  theme(legend.position = "bottom")
```

    ## Warning: Removed 17 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](viz_2_files/figure-gfm/unnamed-chunk-10-1.png)<!-- -->

``` r
ggp_temp_plot +
  theme(legend.position = "bottom")
```

    ## Warning: Removed 17 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](viz_2_files/figure-gfm/unnamed-chunk-11-1.png)<!-- -->

``` r
ggp_temp_plot +
  theme_bw() +
  theme(legend.position = "bottom")
```

    ## Warning: Removed 17 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](viz_2_files/figure-gfm/unnamed-chunk-12-1.png)<!-- -->

``` r
ggp_temp_plot +
  theme_classic() +
  theme(legend.position = "bottom")
```

    ## Warning: Removed 17 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](viz_2_files/figure-gfm/unnamed-chunk-13-1.png)<!-- -->

Learning assessment: Revisit the plot showing tmax against data for each
location.Use labels, scale options, and theme changes to improve the
readability of this plot.

``` r
weather_df |> 
  ggplot(aes(x = date, y = tmax, color = name)) +
  geom_smooth(se = FALSE) +
  geom_point(aes(size = prcp), alpha = .75) +
  labs(
    title = "Temperature plot", 
    x = "Date", 
    y = "Maximum daily temperature (ºC)", 
    color = "Location", 
    caption = "Data from the rnoaa package"
  ) +
  viridis::scale_color_viridis(discrete = TRUE) +
  theme_minimal() + 
  theme(legend.position = "bottom")
```

    ## `geom_smooth()` using method = 'loess' and formula = 'y ~ x'

    ## Warning: Removed 17 rows containing non-finite outside the scale range
    ## (`stat_smooth()`).

    ## Warning: Removed 19 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](viz_2_files/figure-gfm/unnamed-chunk-14-1.png)<!-- -->

## Setting options

``` r
library(tidyverse)

knitr::opts_chunk$set(
  fig.width = 6, 
  fig.asp = .6,
  out.width = "90%"
)

theme_set(theme_minimal() + theme(legend.position = "bottom"))

options(
  ggplot2.continuous.colour = "viridis",
  ggplot2.continuous.fill = "viridis"
)

scale_colour_discrete = scale_colour_viridis_d
scale_fill_discrete = scale_fill_viridis_d
```

## Data args in `geom`

``` r
central_park_df = 
  weather_df |> 
  filter(name == "CentralPark_NY")

molokai_df = 
  weather_df |> 
  filter(name == "Molokai_HI")

ggplot(data = molokai_df, aes(x = date, y = tmax, color = name)) +
  geom_point() +
  geom_line(data = central_park_df)
```

    ## Warning: Removed 1 row containing missing values or values outside the scale range
    ## (`geom_point()`).

![](viz_2_files/figure-gfm/unnamed-chunk-16-1.png)<!-- -->

## `patchwork`

Remember faceting?

``` r
weather_df |> 
  ggplot(aes(x = tmin, fill = name)) + 
  geom_density(alpha = .5) +
facet_grid(. ~ name)
```

    ## Warning: Removed 17 rows containing non-finite outside the scale range
    ## (`stat_density()`).

![](viz_2_files/figure-gfm/unnamed-chunk-17-1.png)<!-- -->

What happens when you want multipanel plots but can’t facet?

``` r
tmax_tmin_p = 
  weather_df |> 
  ggplot(aes(x = tmin, y = tmax, color = name)) +
  geom_point(alpha = .5) +
  theme(legend.position = "none")

prcp_dens_p = 
  weather_df |> 
  filter(prcp > 0) |> 
  ggplot(aes(x = prcp, fill = name)) +
  geom_density(alpha = .5)
  theme(legend.position = "none")
```

    ## <theme> List of 1
    ##  $ legend.position: chr "none"
    ##  @ complete: logi FALSE
    ##  @ validate: logi TRUE

``` r
tmax_date_p = 
  weather_df |> 
  ggplot(aes(x = date, y = tmax, color = name)) +
  geom_point(alpha = .5) + 
  geom_smooth(se = FALSE) + 
  theme(legend.position = "bottom")

tmax_tmin_p + prcp_dens_p
```

    ## Warning: Removed 17 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](viz_2_files/figure-gfm/unnamed-chunk-18-1.png)<!-- -->

``` r
tmax_tmin_p + prcp_dens_p + tmax_date_p
```

    ## Warning: Removed 17 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

    ## `geom_smooth()` using method = 'loess' and formula = 'y ~ x'

    ## Warning: Removed 17 rows containing non-finite outside the scale range
    ## (`stat_smooth()`).
    ## Removed 17 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](viz_2_files/figure-gfm/unnamed-chunk-18-2.png)<!-- -->

``` r
tmax_tmin_p + (prcp_dens_p + tmax_date_p)
```

    ## Warning: Removed 17 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

    ## `geom_smooth()` using method = 'loess' and formula = 'y ~ x'

    ## Warning: Removed 17 rows containing non-finite outside the scale range
    ## (`stat_smooth()`).
    ## Removed 17 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](viz_2_files/figure-gfm/unnamed-chunk-18-3.png)<!-- -->

``` r
(tmax_tmin_p + prcp_dens_p) / tmax_date_p
```

    ## Warning: Removed 17 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

    ## `geom_smooth()` using method = 'loess' and formula = 'y ~ x'

    ## Warning: Removed 17 rows containing non-finite outside the scale range
    ## (`stat_smooth()`).
    ## Removed 17 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](viz_2_files/figure-gfm/unnamed-chunk-18-4.png)<!-- -->

## Data manipulation

``` r
weather_df |> 
  ggplot(aes(x = name, y = tmax, fill = name)) + 
  geom_violin(alpha = .5)
```

    ## Warning: Removed 17 rows containing non-finite outside the scale range
    ## (`stat_ydensity()`).

![](viz_2_files/figure-gfm/unnamed-chunk-19-1.png)<!-- -->

Control your factors. If you want to change the order (reorder
categorical predictor on X axis)

Option 1; just include Molokai_HI (makes this first), keeps rest in same
order

``` r
weather_df |> 
  mutate(
    name = factor(name),
    name = forcats::fct_relevel(name, c("Molokai_HI"))
  ) |> 
  ggplot(aes(x = name, y = tmax, fill = name)) + 
  geom_violin(alpha = .5)
```

    ## Warning: Removed 17 rows containing non-finite outside the scale range
    ## (`stat_ydensity()`).

![](viz_2_files/figure-gfm/unnamed-chunk-20-1.png)<!-- -->

Option 2; specify exact order you want

``` r
weather_df |> 
  mutate(
    name = factor(name),
    name = forcats::fct_relevel(name, c("Molokai_HI", "CentralPark_NY", "Waterhole_WA"))
  ) |> 
  ggplot(aes(x = name, y = tmax)) + 
  geom_violin(aes(fill = name), color = "blue", alpha = .5) +
  theme(legend.position = "bottom")
```

    ## Warning: Removed 17 rows containing non-finite outside the scale range
    ## (`stat_ydensity()`).

![](viz_2_files/figure-gfm/unnamed-chunk-21-1.png)<!-- -->

Option 3; reorders name according to tmax values in each name (place)
-sorts from lowest to highest tmax (based on each place’s median temp
value)

``` r
weather_df |> 
  mutate(name = forcats::fct_reorder(name, tmax)) |> 
  ggplot(aes(x = name, y = tmax)) +
  geom_violin(aes(fill = name), colour = "blue", alpha = .5) +
  theme(legend.position = "bottom")
```

    ## Warning: There was 1 warning in `mutate()`.
    ## ℹ In argument: `name = forcats::fct_reorder(name, tmax)`.
    ## Caused by warning:
    ## ! `fct_reorder()` removing 17 missing values.
    ## ℹ Use `.na_rm = TRUE` to silence this message.
    ## ℹ Use `.na_rm = FALSE` to preserve NAs.

    ## Warning: Removed 17 rows containing non-finite outside the scale range
    ## (`stat_ydensity()`).

![](viz_2_files/figure-gfm/unnamed-chunk-22-1.png)<!-- -->

What if I wanted densities for tmin and tmax simultaneously?

shows tmax and tmin values for central park NY

``` r
weather_df |> 
  filter(name == "CentralPark_NY") |> 
  pivot_longer(
    tmax:tmin,
    names_to = "observation", 
    values_to = "temp") |> 
  ggplot(aes(x = temp, fill = observation)) +
  geom_density(alpha = .5) 
```

![](viz_2_files/figure-gfm/unnamed-chunk-23-1.png)<!-- -->

Makes density plots with tmin and tmax for each place (one panel per
place)

``` r
weather_df |> 
  pivot_longer(
    tmax:tmin,
    names_to = "observation", 
    values_to = "temp") |> 
  ggplot(aes(x = temp, fill = observation)) +
  geom_density(alpha = .5) +
  facet_grid(. ~ name) 
```

    ## Warning: Removed 34 rows containing non-finite outside the scale range
    ## (`stat_density()`).

![](viz_2_files/figure-gfm/unnamed-chunk-24-1.png)<!-- -->

Makes density plots with tmin and tmax for each place (one panel per
place), with viridis colour scheme

``` r
weather_df |> 
  select(name, tmax, tmin) |> 
  pivot_longer(
    tmax:tmin,
    names_to = "observation", 
    values_to = "temp") |> 
  ggplot(aes(x = temp, fill = observation)) +
  geom_density(alpha = .5) +
  facet_grid(. ~ name) +
  viridis::scale_fill_viridis(discrete = TRUE)
```

    ## Warning: Removed 34 rows containing non-finite outside the scale range
    ## (`stat_density()`).

![](viz_2_files/figure-gfm/unnamed-chunk-25-1.png)<!-- -->

## Revisit the pups

Data from the FAS study.

Import, tidying, and plotting steps \[following 2 chunks do the same\]

From class:

``` r
pups_data = 
  read_csv("./data/FAS_pups.csv", na = c("NA", ".", ""), skip = 3) |> 
  janitor::clean_names() |> 
  mutate(
    sex = 
      case_match(
        sex, 
        1 ~ "male", 
        2 ~ "female"))
```

    ## Rows: 313 Columns: 6
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (1): Litter Number
    ## dbl (5): Sex, PD ears, PD eyes, PD pivot, PD walk
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

    ## Warning: There was 1 warning in `mutate()`.
    ## ℹ In argument: `sex = case_match(sex, 1 ~ "male", 2 ~ "female")`.
    ## Caused by warning:
    ## ! `case_match()` was deprecated in dplyr 1.2.0.
    ## ℹ Please use `recode_values()` instead.

``` r
litters_data = 
  read_csv("./data/FAS_litters.csv", na = c("NA", ".", "")) |> 
  janitor::clean_names() |> 
  separate(group, into = c("dose", "day_of_tx"), sep = 3)
```

    ## Rows: 49 Columns: 8
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (2): Group, Litter Number
    ## dbl (6): GD0 weight, GD18 weight, GD of Birth, Pups born alive, Pups dead @ ...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
fas_data = left_join(pups_data, litters_data, by = "litter_number")

fas_data |> 
  ggplot(aes(x = dose, y = pd_ears)) +
  geom_violin() +
  facet_grid(. ~ day_of_tx)
```

    ## Warning: Removed 18 rows containing non-finite outside the scale range
    ## (`stat_ydensity()`).

![](viz_2_files/figure-gfm/unnamed-chunk-26-1.png)<!-- -->

``` r
fas_data |> 
  select(sex, dose, day_of_tx, starts_with("pd_")) |> 
  pivot_longer(
    pd_ears:pd_walk, 
    names_to = "outcome", 
    values_to = "pn_day"
  ) |> 
  drop_na() |> 
  mutate(outcome = forcats::fct_reorder(outcome, pn_day, median)) |> 
  ggplot(aes(x = dose, y = pn_day)) +
  geom_violin() +
  facet_grid(day_of_tx ~ outcome)
```

![](viz_2_files/figure-gfm/unnamed-chunk-26-2.png)<!-- -->

From video:

``` r
pups_data = 
  read_csv("./data/FAS_pups.csv", na = c("NA", ".", ""), skip = 3) |> 
  janitor::clean_names() |> 
  mutate(sex = recode(sex, `1` = "male", `2` = "female"))
```

    ## Rows: 313 Columns: 6
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (1): Litter Number
    ## dbl (5): Sex, PD ears, PD eyes, PD pivot, PD walk
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
litters_data = 
  read_csv("./data/FAS_litters.csv", na = c("NA", ".", "")) |> 
  janitor::clean_names() |> 
  separate(group, into = c("dose", "day_of_tx"), sep = 3)
```

    ## Rows: 49 Columns: 8
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (2): Group, Litter Number
    ## dbl (6): GD0 weight, GD18 weight, GD of Birth, Pups born alive, Pups dead @ ...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
fas_data = left_join(pups_data, litters_data, by = "litter_number")

fas_data |> 
  ggplot(aes(x = dose, y = pd_ears)) +
  geom_violin() +
  facet_grid(. ~ day_of_tx)
```

    ## Warning: Removed 18 rows containing non-finite outside the scale range
    ## (`stat_ydensity()`).

![](viz_2_files/figure-gfm/unnamed-chunk-27-1.png)<!-- -->

``` r
fas_data |> 
  select(dose, day_of_tx, starts_with("pd_")) |> 
  pivot_longer(
    pd_ears:pd_walk, 
    names_to = "outcome", 
    values_to = "pn_day"
  ) |> 
  drop_na() |> 
  mutate(outcome = forcats::fct_relevel(outcome, "pd_ears", "pd_pivot", "pd_walk", "pd_eyes")) |> 
  ggplot(aes(x = dose, y = pn_day)) +
  geom_violin() +
  facet_grid(day_of_tx ~ outcome)
```

![](viz_2_files/figure-gfm/unnamed-chunk-27-2.png)<!-- -->

Pulse data example

``` r
pulse_data = 
  haven::read_sas("./data/public_pulse_data.sas7bdat") |> 
  janitor::clean_names() |> 
  pivot_longer(
    bdi_score_bl:bdi_score_12m,
    names_to = "visit", 
    names_prefix = "bdi_score_", 
    values_to = "bdi") |> 
  select(id, visit, everything()) |> 
  mutate(
    visit = recode(visit, "bl" = "00m"), 
    visit = factor(visit, levels = str_c(c("00", "01", "06", "12"), "m"))) |> 
  arrange(id, visit)

ggplot(pulse_data, aes(x = visit, y = bdi)) +
  geom_boxplot()
```

    ## Warning: Removed 879 rows containing non-finite outside the scale range
    ## (`stat_boxplot()`).

![](viz_2_files/figure-gfm/unnamed-chunk-28-1.png)<!-- -->
