# Substrait types

Substrait types

## Usage

``` r
substrait_boolean()

substrait_i8()

substrait_i16()

substrait_i32()

substrait_i64()

substrait_fp32()

substrait_fp64()

substrait_string()

substrait_binary()

substrait_timestamp()

substrait_timestamp_tz()

substrait_date()

substrait_time()

substrait_interval_year()

substrait_interval_day()

substrait_uuid()
```

## Value

A substrait.Type proto object

## Examples

``` r
substrait_boolean()
#> message of type 'substrait.Type' with 1 field set
#> bool {
#>   nullability: NULLABILITY_NULLABLE
#> }
substrait_i32()
#> message of type 'substrait.Type' with 1 field set
#> i32 {
#>   nullability: NULLABILITY_NULLABLE
#> }
substrait_fp64()
#> message of type 'substrait.Type' with 1 field set
#> fp64 {
#>   nullability: NULLABILITY_NULLABLE
#> }
substrait_string()
#> message of type 'substrait.Type' with 1 field set
#> string {
#>   nullability: NULLABILITY_NULLABLE
#> }
```
