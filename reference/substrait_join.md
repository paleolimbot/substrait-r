# Append a Substrait Join relation

Append a Substrait Join relation

## Usage

``` r
substrait_join(
  compiler_left,
  compiler_right,
  by = NULL,
  type = "JOIN_TYPE_INNER",
  name_repair_func = join_name_repair_suffix_common(),
  output_mapping_func = join_emit_all()
)

join_name_repair_none()

join_name_repair_suffix_common(suffix = c(".x", ".y"))

join_emit_all()

join_emit_default()
```

## Arguments

- compiler_left, compiler_right:

  A [`substrait_compiler()`](substrait_compiler.md) or table-like object
  to use as inputs to the join relation. Currently only one of these can
  be a [`substrait_compiler()`](substrait_compiler.md).

- by:

  A join specifiation. Join specifications that are currently supported
  include a character vector of column names whose optional names
  indicate the name on `compiler_left` (e.g., `"common_name"` or
  `c("name_left" = "name_right")`).

- type:

  One of "JOIN_TYPE_INNER", "JOIN_TYPE_OUTER", "JOIN_TYPE_LEFT",
  "JOIN_TYPE_RIGHT", "JOIN_TYPE_SEMI", "JOIN_TYPE_ANTI", or
  "JOIN_TYPE_SINGLE".

- name_repair_func:

  A function of `output_mapping`, `names_left`, and `names_right` used
  to calculate the output names (e.g.,
  `join_name_repair_suffix_common()` or `join_name_repair_none()`).

- output_mapping_func:

  A function of `by`, `names_left`, and `names_right` used to calculate
  the zero-based indices of the output to include (e.g.,
  `join_emit_all()` or `join_emit_default()`).

- suffix:

  A length 2 character vector of suffixes to use to disambiguate columns
  from the left and right inputs whose name would be duplicated in the
  output.

## Value

A modified compiler.

## Examples

``` r
if (FALSE) { # has_duckdb_with_substrait()
left <- tibble::tibble(number = 1:3, letter = c("a", "b", "c"))
right <- tibble::tibble(number = 2:4, LETTER = c("B", "C", "D"))

# Default join keeps all columns
joined <- substrait_join(
  duckdb_substrait_compiler(left),
  right
)
joined$schema$names

# Use output_mapping_func to change the default output
joined <- substrait_join(
  duckdb_substrait_compiler(left),
  right,
  output_mapping_func = join_emit_default()
)
joined$schema$names
}
```
