# DuckDB Substrait Interface

DuckDB Substrait Interface

## Usage

``` r
duckdb_get_substrait(sql, tables = list())

duckdb_from_substrait(
  plan,
  tables = list(),
  col_names = plan$relations[[1]]$root$names,
  as_data_frame = TRUE
)

has_duckdb_with_substrait()
```

## Arguments

- sql:

  An SQL expression from which to generate a Substrait plan

- tables:

  A named list of tables to populate the database

- plan:

  A substrait.Plan proto object

- col_names:

  The final column names for the result

- as_data_frame:

  Use `FALSE` to return an
  [arrow::Table](https://arrow.apache.org/docs/r/reference/Table-class.html)
  instead of a data.frame.

## Value

- `duckdb_get_substrait()`: a substrait.Plan protobuf object

- `duckdb_from_substrait()`: A data.frame or arrow Table

## Examples

``` r
if (FALSE) { # has_duckdb_with_substrait()
plan <- duckdb_get_substrait(
  "SELECT * from mtcars WHERE mpg > 30",
  tables = list(mtcars = mtcars)
)

duckdb_from_substrait(plan, tables = list(mtcars = mtcars))
}
```
