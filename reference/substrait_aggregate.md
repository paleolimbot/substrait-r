# Aggregate

Aggregate

## Usage

``` r
substrait_aggregate(.compiler, ...)

substrait_group_by(.compiler, ...)

substrait_ungroup(.compiler)
```

## Arguments

- .compiler:

  A [`substrait_compiler()`](substrait_compiler.md) or object that can
  be coerced to one

- ...:

  - `substrait_aggregate()`: A named list of expressions to be evaluated
    in the context of the aggregation.

    - `substrait_group_by()`: A list of expressions to be used as
      groupings for aggregation.

## Value

A modified `.compiler`.
