# Append a Substrait Fetch Relation

Append a Substrait Fetch Relation

## Usage

``` r
substrait_fetch(.compiler, offset = 0, count)
```

## Arguments

- .compiler:

  A [`substrait_compiler()`](substrait_compiler.md) or object that can
  be coerced to one

- offset:

  Number of rows to skip before returning rows

- count:

  Number of rows to return

## Value

A modified `.compiler`

## Examples

``` r
if (FALSE) { # has_duckdb_with_substrait()
substrait_fetch(
  duckdb_substrait_compiler(data.frame(x = 1:10)),
  offset = 2,
  count = 2
)
}
```
