# Translation utilities

These functions are used to translate R function calls into Substrait
expressions that can be passed on to a consumer, compiled, and evaluated
there. Use `substrait_call()` to generate a
substrait.Expression.ScalarFunction based on a function name and a
series of arguments; use `substrait_eval()` to translate R code using
Substrait function translations where possible; and use
`substrait_eval_data()` translate R code using Substrait function
translations *and* the `.data` mask from the
[`current_compiler()`](current_compiler.md).

## Usage

``` r
substrait_call(.fun, ..., .output_type = NULL, .options = NULL)

substrait_call_agg(
  .fun,
  ...,
  .output_type = NULL,
  .phase = 0L,
  .invocation = 0L
)

substrait_eval(expr)

substrait_eval_data(expr)
```

## Arguments

- .fun:

  The name of a substrait function as a string that will be passed on to
  the consumer. The function will be registered with the compiler and
  assigned a new identifier if it has not already been used.

- ...:

  Function arguments. These will be coerced to a substrait.Expression if
  they have not been already. Translation functions should take care to
  handle R objects that do not readily translate into substrait types
  via `as_substrait_expression(x)` before passing them to
  `substrait_call()` or `substrait_call_agg()`.

- .output_type:

  The output type of the call. In the future this may be built in to the
  compiler since in theory the compiler should be able to predict this.

- .options:

  An optional list of substrait.FunctionOption messages to associate
  with this call.

- .phase:

  Describes the input type of the data describing what portion of the
  operation is required

- .invocation:

  Whether the function uses all or only distinct values in the
  aggregation calculation

- expr:

  An expression to evaluate with the translations defined by the current
  compiler. You can use this to define translations that use other
  translations in a more readable way. You can use tidy evaluation
  within `expr`, including unquoting (`!!`), `.data$some_column`, to
  access a column explicitly, and `.fns$some_function()` to access a
  translation explicitly.

## Value

All of these functions return an object that can be coerced to a
substrait.Expression via `as_substrait_expression(x)`.

## See also

[Substrait docs on aggregate function
properties](https://substrait.io/expressions/aggregate_functions/#aggregate-binding)

## Examples

``` r
# create a compiler
compiler <- substrait_compiler(data.frame(a = 1, b = 2))

# usually functions are defined in internal package code,
# but you can also define them for testing like this:
compiler$.fns$sqrt <- function(x) {
  substrait_call("sqrt", x, .output_type = substrait_fp64())
}

# substrait_eval() does not have access to column names
try(with_compiler(compiler, substrait_eval(b)))
#> Error : object 'b' not found

# ..but does have access to functions
with_compiler(compiler, substrait_eval(sqrt(4)))
#> message of type 'substrait.Expression.ScalarFunction' with 3 fields set
#> function_reference: 2
#> output_type {
#>   fp64 {
#>     nullability: NULLABILITY_NULLABLE
#>   }
#> }
#> arguments {
#>   value {
#>     literal {
#>       fp64: 4
#>     }
#>   }
#> }

# use substrait_eval_data() to do a more direct test of a translation
with_compiler(compiler, substrait_eval_data(sqrt(b)))
#> message of type 'substrait.Expression.ScalarFunction' with 3 fields set
#> function_reference: 2
#> output_type {
#>   fp64 {
#>     nullability: NULLABILITY_NULLABLE
#>   }
#> }
#> arguments {
#>   value {
#>     selection {
#>       direct_reference {
#>         struct_field {
#>           field: 1
#>         }
#>       }
#>       root_reference {
#>       }
#>     }
#>   }
#> }
```
