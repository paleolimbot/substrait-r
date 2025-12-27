# Compiler context

When translation functions are called, the compiler that is evaluating
them is made available as a global variable accessible via
`current_compiler()`. Typically this is not needed directly within a
translation function but is used by
[`substrait_call()`](substrait_call.md) and other functions that need to
interact with the current compiler. Translation authors may find
`with_compiler()` and/or `local_compiler()` useful to test translation
functions directly.

## Usage

``` r
current_compiler()

with_compiler(compiler, code)

local_compiler(compiler, .local_envir = parent.frame())
```

## Arguments

- compiler:

  A [`substrait_compiler()`](substrait_compiler.md) or object that can
  be coerced to one.

- code:

  An expression to evaluate with `compiler` as the `current_compiler()`.

- .local_envir:

  The environment for which `compiler` should remain the
  `current_compiler()`. This should usually stay the default value of
  the calling environment.

## Value

- `current_compiler()` returns a
  [`substrait_compiler()`](substrait_compiler.md) or `NULL` if none has
  been registered.

- `with_compiler()` returns the result of evaluating `code`

- `local_compiler()` returns the result of coercing `compiler` to a
  [`substrait_compiler()`](substrait_compiler.md).

## Examples

``` r
current_compiler()
#> NULL

with_compiler(data.frame(a = 1L), {
  current_compiler()$schema
})
#> message of type 'substrait.NamedStruct' with 2 fields set
#> names: "a"
#> struct {
#>   types {
#>     i32 {
#>       nullability: NULLABILITY_NULLABLE
#>     }
#>   }
#> }

local({
  compiler <- local_compiler(data.frame(a = 1L))
  compiler$schema
  current_compiler()$schema
})
#> message of type 'substrait.NamedStruct' with 2 fields set
#> names: "a"
#> struct {
#>   types {
#>     i32 {
#>       nullability: NULLABILITY_NULLABLE
#>     }
#>   }
#> }

current_compiler()
#> NULL
```
