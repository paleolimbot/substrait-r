# Create an DuckDB Substrait Compiler

Create an DuckDB Substrait Compiler

## Usage

``` r
duckdb_substrait_compiler(object, ...)
```

## Arguments

- object:

  A [`data.frame()`](https://rdrr.io/r/base/data.frame.html),
  [arrow::Table](https://arrow.apache.org/docs/r/reference/Table-class.html),
  [arrow::RecordBatch](https://arrow.apache.org/docs/r/reference/RecordBatch-class.html),
  or
  [arrow::Dataset](https://arrow.apache.org/docs/r/reference/Dataset.html),
  or anything else that can be written to a parquet file using
  [`arrow::write_parquet()`](https://arrow.apache.org/docs/r/reference/write_parquet.html).

- ...:

  Unused.

## Value

A [SubstraitCompiler](SubstraitCompiler.md) subclass.
