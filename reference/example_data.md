# Example data

Data for use in examples and tests with multiple different data types

## Usage

``` r
example_data
```

## Format

An object of class `tbl_df` (inherits from `tbl`, `data.frame`) with 10
rows and 9 columns.

## Examples

``` r
example_data
#> # A tibble: 10 × 9
#>      int      dbl  dbl2 lgl   false chr   verses    padded_strings some_negative
#>    <int>    <dbl> <dbl> <lgl> <lgl> <chr> <chr>     <chr>                  <dbl>
#>  1 -3212  -999     -Inf NA    FALSE a     Por cada… " a "                     -1
#>  2     2   -99        5 TRUE  FALSE b     En Jerus… "  b  "                    2
#>  3     3    -9        5 NA    FALSE c     Y mil vi… "   c   "                 -3
#>  4    NA     0        5 TRUE  FALSE d     Por cada… "    d    "               NA
#>  5     5     9        5 FALSE FALSE e     Yo soy p… "     e     "             -5
#>  6     6     3.14     5 FALSE FALSE NA    Y aunque… "      f     …             6
#>  7     7    99        5 NA    FALSE g     Y cada p… "       g    …            -7
#>  8     8 10000        5 TRUE  FALSE h     Guarda m… "        h   …             8
#>  9     9 10000        5 FALSE FALSE i     No hay u… "         i  …            -9
#> 10  3212    NA        5 TRUE  FALSE j     Que valg… "          j …            10
```
