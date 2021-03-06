isdparser
=========



[![Build Status](https://travis-ci.org/ropensci/isdparser.svg?branch=master)](https://travis-ci.org/ropensci/isdparser)
[![codecov.io](https://codecov.io/github/ropensci/isdparser/coverage.svg?branch=master)](https://codecov.io/github/ropensci/isdparser?branch=master)
[![cran version](http://www.r-pkg.org/badges/version/isdparser)](https://cran.r-project.org/package=isdparser)


`isdparser` is a parser for ISD/ISD NOAA files

Code liberated from `rnoaa` to focus on ISD parsing since it's sorta
complicated. Has minimal dependencies, so you can parse your ISD/ISH
files without needing the deps that `rnoaa` needs. Will be used by
`rnoaa` once on CRAN.

Documentation at ftp://ftp.ncdc.noaa.gov/pub/data/noaa/ish-format-document.pdf

## API:

* `isd_parse()` - parse all lines in a file, with parallel option
* `isd_parse_line()` - parse a single line - you choose which lines to parse
and how to apply the function to your lines
* `isd_transform()` - transform ISD data variables

## Installation

CRAN stable version


```r
install.packages("isdparser")
```

Dev version


```r
devtools::install_github("ropensci/isdparser")
```


```r
library('isdparser')
```

### Parse lines from an ISD file


```r
path <- system.file('extdata/024130-99999-2016.gz', package = "isdparser")
lns <- readLines(path, encoding = "latin1")
isd_parse_line(lns[1])
#> # A tibble: 1 × 42
#>   total_chars usaf_station wban_station     date  time date_flag latitude
#>         <chr>        <chr>        <chr>    <chr> <chr>     <chr>    <chr>
#> 1        0054       024130        99999 20160101  0000         4   +60750
#> # ... with 35 more variables: longitude <chr>, type_code <chr>,
#> #   elevation <chr>, call_letter <chr>, quality <chr>,
#> #   wind_direction <chr>, wind_direction_quality <chr>, wind_code <chr>,
#> #   wind_speed <chr>, wind_speed_quality <chr>, ceiling_height <chr>,
#> #   ceiling_height_quality <chr>, ceiling_height_determination <chr>,
#> #   ceiling_height_cavok <chr>, visibility_distance <chr>,
#> #   visibility_distance_quality <chr>, visibility_code <chr>,
#> #   visibility_code_quality <chr>, temperature <chr>,
#> #   temperature_quality <chr>, temperature_dewpoint <chr>,
#> #   temperature_dewpoint_quality <chr>, air_pressure <chr>,
#> #   air_pressure_quality <chr>,
#> #   AW1_present_weather_observation_identifier <chr>,
#> #   AW1_automated_atmospheric_condition_code <chr>,
#> #   AW1_quality_automated_atmospheric_condition_code <chr>,
#> #   N03_original_observation <chr>, N03_original_value_text <chr>,
#> #   N03_units_code <chr>, N03_parameter_code <chr>, REM_remarks <chr>,
#> #   REM_identifier <chr>, REM_length_quantity <chr>, REM_comment <chr>
```

Or, give back a list


```r
head(
  isd_parse_line(lns[1], as_data_frame = FALSE)
)
#> $total_chars
#> [1] "0054"
#> 
#> $usaf_station
#> [1] "024130"
#> 
#> $wban_station
#> [1] "99999"
#> 
#> $date
#> [1] "20160101"
#> 
#> $time
#> [1] "0000"
#> 
#> $date_flag
#> [1] "4"
```

### Parse an ISD file


```r
path <- system.file('extdata/024130-99999-2016.gz', package = "isdparser")
isd_parse(path)
#> # A tibble: 2,601 × 42
#>    total_chars usaf_station wban_station     date  time date_flag latitude
#>          <chr>        <chr>        <chr>    <chr> <chr>     <chr>    <chr>
#> 1         0054       024130        99999 20160101  0000         4   +60750
#> 2         0054       024130        99999 20160101  0100         4   +60750
#> 3         0054       024130        99999 20160101  0200         4   +60750
#> 4         0054       024130        99999 20160101  0300         4   +60750
#> 5         0054       024130        99999 20160101  0400         4   +60750
#> 6         0039       024130        99999 20160101  0500         4   +60750
#> 7         0054       024130        99999 20160101  0600         4   +60750
#> 8         0039       024130        99999 20160101  0700         4   +60750
#> 9         0054       024130        99999 20160101  0800         4   +60750
#> 10        0054       024130        99999 20160101  0900         4   +60750
#> # ... with 2,591 more rows, and 35 more variables: longitude <chr>,
#> #   type_code <chr>, elevation <chr>, call_letter <chr>, quality <chr>,
#> #   wind_direction <chr>, wind_direction_quality <chr>, wind_code <chr>,
#> #   wind_speed <chr>, wind_speed_quality <chr>, ceiling_height <chr>,
#> #   ceiling_height_quality <chr>, ceiling_height_determination <chr>,
#> #   ceiling_height_cavok <chr>, visibility_distance <chr>,
#> #   visibility_distance_quality <chr>, visibility_code <chr>,
#> #   visibility_code_quality <chr>, temperature <chr>,
#> #   temperature_quality <chr>, temperature_dewpoint <chr>,
#> #   temperature_dewpoint_quality <chr>, air_pressure <chr>,
#> #   air_pressure_quality <chr>,
#> #   AW1_present_weather_observation_identifier <chr>,
#> #   AW1_automated_atmospheric_condition_code <chr>,
#> #   AW1_quality_automated_atmospheric_condition_code <chr>,
#> #   N03_original_observation <chr>, N03_original_value_text <chr>,
#> #   N03_units_code <chr>, N03_parameter_code <chr>, REM_remarks <chr>,
#> #   REM_identifier <chr>, REM_length_quantity <chr>, REM_comment <chr>
```

process in parallel


```r
isd_parse(path, parallel = TRUE)
```

## Meta

* Please [report any issues or bugs](https://github.com/ropensci/isdparser/issues).
* License: MIT
* Get citation information for `isdparser` in R doing `citation(package = 'isdparser')`
* Please note that this project is released with a [Contributor Code of Conduct](CONDUCT.md). By participating in this project you agree to abide by its terms.

[![rofooter](http://ropensci.org/public_images/github_footer.png)](http://ropensci.org)
