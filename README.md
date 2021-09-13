
# ufc.stats

## Data Source Used

https://s3-us-west-1.amazonaws.com/ufc.stats/final/ufc_stats.rda

## Usage in Python

Can download data from link above, unzip, and read with python

# read an R object into dictionary type struct with values as pandas dataframes
import pyreadr

data = pyreadr.read_r(file_location)
print(data.keys())
stats = data["ufc_stats"]
stats.head()























# Old Notes

<!-- README.md is generated from README.Rmd. Please edit that file -->

This package contains UFC fight statistics, continously updated with
data from latest events.

## Installation

You can install the development version from
[GitHub](https://github.com/) with:

``` r
# devtools::install_github("mtoto/ufc.stats")
data("ufc_stats")
```

Each row of `ufc_stats` represents the statistics of one fighter in a
single round of a fight. The `data.frame` contains 37 variables in
total. For full a description of each variable, please refer to the
[Data
Dictionary](http://tamaszilagyi.com/ufc.stats/articles/data-dictionary.html).

## Example usage

Who has the most significant strikes landed in UFC history?

``` r
library(dplyr)

ufc_stats %>% group_by(fighter) %>%
  summarise(total_significant_strikes = sum(significant_strikes_landed)) %>%
  arrange(-total_significant_strikes) %>%
  head()
#> # A tibble: 6 × 2
#>   fighter            total_significant_strikes
#>   <chr>                                  <int>
#> 1 Max Holloway                            2618
#> 2 Donald Cerrone                          1727
#> 3 Joanna Jedrzejczyk                      1711
#> 4 Frankie Edgar                           1705
#> 5 Michael Bisping                         1567
#> 6 Dustin Poirier                          1527
```

## Updating with latest fights

The package contains a single function `refresh_data()` that updates the
dataset contained within the package. Running `data("ufc_stats")`
subsequently, the latest version of the data.frame is loaded into
memory.
