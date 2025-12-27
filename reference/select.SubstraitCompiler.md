# dplyr verb implementations

dplyr verb implementations

## Usage

``` r
# S3 method for class 'SubstraitCompiler'
select(.data, ...)

# S3 method for class 'SubstraitCompiler'
rename(.data, ...)

# S3 method for class 'SubstraitCompiler'
rename_with(.data, .fn, .cols = dplyr::everything(), ...)

# S3 method for class 'SubstraitCompiler'
filter(.data, ...)

# S3 method for class 'SubstraitCompiler'
mutate(.data, ..., .keep = c("all", "used", "unused", "none"))

# S3 method for class 'SubstraitCompiler'
transmute(.data, ...)

# S3 method for class 'SubstraitCompiler'
arrange(.data, ..., .by_group = FALSE)

# S3 method for class 'SubstraitCompiler'
group_by(.data, ..., .add = FALSE, .drop = NULL)

# S3 method for class 'SubstraitCompiler'
ungroup(x, ...)

# S3 method for class 'SubstraitCompiler'
summarise(.data, ..., .groups = NULL)

# S3 method for class 'SubstraitCompiler'
summarize(.data, ..., .groups = NULL)

# S3 method for class 'SubstraitCompiler'
collect(x, ...)

# S3 method for class 'SubstraitCompiler'
relocate(.data, ..., .before = NULL, .after = NULL)

# S3 method for class 'SubstraitCompiler'
semi_join(x, y, by = NULL, ...)

# S3 method for class 'SubstraitCompiler'
anti_join(x, y, by = NULL, ...)

# S3 method for class 'SubstraitCompiler'
inner_join(x, y, by = NULL, suffix = c(".x", ".y"), ..., keep = NULL)

# S3 method for class 'SubstraitCompiler'
left_join(x, y, by = NULL, suffix = c(".x", ".y"), ..., keep = NULL)

# S3 method for class 'SubstraitCompiler'
right_join(x, y, by = NULL, suffix = c(".x", ".y"), ..., keep = NULL)

# S3 method for class 'SubstraitCompiler'
full_join(x, y, by = NULL, suffix = c(".x", ".y"), ..., keep = NULL)

# S3 method for class 'SubstraitCompiler'
distinct(.data, ..., .keep_all = FALSE)

# S3 method for class 'SubstraitCompiler'
count(.data, ..., wt = NULL, sort = FALSE, name = NULL)
```

## Arguments

- .data, x, y:

  A [`substrait_compiler()`](substrait_compiler.md)

- ...:

  - [`select()`](https://dplyr.tidyverse.org/reference/select.html): see
    [`dplyr::select()`](https://dplyr.tidyverse.org/reference/select.html)

    - [`rename()`](https://dplyr.tidyverse.org/reference/rename.html):
      see
      [`dplyr::rename()`](https://dplyr.tidyverse.org/reference/rename.html)

    - [`filter()`](https://dplyr.tidyverse.org/reference/filter.html):
      see
      [`dplyr::filter()`](https://dplyr.tidyverse.org/reference/filter.html)

    - [`mutate()`](https://dplyr.tidyverse.org/reference/mutate.html):
      see
      [`dplyr::mutate()`](https://dplyr.tidyverse.org/reference/mutate.html)

    - [`arrange()`](https://dplyr.tidyverse.org/reference/arrange.html):
      see
      [`dplyr::arrange()`](https://dplyr.tidyverse.org/reference/arrange.html)

    - [`count()`](https://dplyr.tidyverse.org/reference/count.html): see
      [`dplyr::count()`](https://dplyr.tidyverse.org/reference/count.html)

    - [`distinct()`](https://dplyr.tidyverse.org/reference/distinct.html):
      see
      [`dplyr::distinct()`](https://dplyr.tidyverse.org/reference/distinct.html)

- .fn:

  Function to transform selected `.cols`;
  see[`dplyr::rename_with()`](https://dplyr.tidyverse.org/reference/rename.html)

- .cols:

  Columns to rename;
  see[`dplyr::rename_with()`](https://dplyr.tidyverse.org/reference/rename.html)

- .keep:

  Which columns are retained in output; see
  [`dplyr::mutate()`](https://dplyr.tidyverse.org/reference/mutate.html)

- .by_group:

  sort by grouping variable?
  see[`dplyr::arrange()`](https://dplyr.tidyverse.org/reference/arrange.html)

- .add:

  Use `TRUE` to add the groupings to the current groupings and `FALSE`
  to reset the grouping.

- .drop:

  Not supported, see
  [`dplyr::group_by()`](https://dplyr.tidyverse.org/reference/group_by.html)

- .groups:

  One of "drop_last", "drop", or "keep" (see
  [`dplyr::summarise()`](https://dplyr.tidyverse.org/reference/summarise.html)).

- .before:

  Destination of columns to move; see
  [`dplyr::relocate()`](https://dplyr.tidyverse.org/reference/relocate.html)

- .after:

  Destination of columns to move; see
  [`dplyr::relocate()`](https://dplyr.tidyverse.org/reference/relocate.html)

- by:

  For joins, a join specifier or `NULL` to use common variables across
  `x` and `y`; see
  [`dplyr::inner_join()`](https://dplyr.tidyverse.org/reference/mutate-joins.html).

- suffix:

  A suffix used to disambiguate columns from `x` and `y` if a join would
  result in duplicate column names.

- keep:

  For joins, use `TRUE` to keep all output columns; see
  [`dplyr::inner_join()`](https://dplyr.tidyverse.org/reference/mutate-joins.html).

- .keep_all:

  If TRUE, keep all variables in .data; see
  [`dplyr::distinct()`](https://dplyr.tidyverse.org/reference/distinct.html)

- wt:

  Frequency weights; see
  [`dplyr::count()`](https://dplyr.tidyverse.org/reference/count.html)

- sort:

  If TRUE, will show the largest groups at the top; see
  [`dplyr::count()`](https://dplyr.tidyverse.org/reference/count.html)

- name:

  The name of the new column in the output; see
  [`dplyr::count()`](https://dplyr.tidyverse.org/reference/count.html)

## Value

A modified [`substrait_compiler()`](substrait_compiler.md)

## Examples

``` r
if (FALSE) { # has_duckdb_with_substrait()
library(dplyr)
compiler <- duckdb_substrait_compiler(mtcars)

select(compiler, mpg2 = mpg) %>% collect()
rename(compiler, mpg2 = mpg) %>% collect()
filter(compiler, mpg > 20) %>% collect()
mutate(compiler, mpg + 10) %>% collect()
transmute(compiler, mpg + 10) %>% collect()
arrange(compiler, desc(mpg)) %>% collect()
}
```
