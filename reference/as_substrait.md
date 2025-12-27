# Convert to and from 'Substrait' messages

Convert to and from 'Substrait' messages

## Usage

``` r
as_substrait(x, .ptype = NULL, ...)

from_substrait(msg, x, ...)

as_substrait_expression(x, ...)

as_substrait_type(x, ...)
```

## Arguments

- x:

  An object to convert to or from a 'Substrait' message. Note that both
  `as_substrait()` and `from_substrait()` dispatch on `x`.

- .ptype:

  A string of the `.qualified_name` or a prototype message of the
  correct type.

- ...:

  Passed to S3 methods

- msg:

  A substrait message (e.g., created using
  [`substrait_create()`](substrait_create.md)).

## Value

An RProtoBuf::Message or substrait_proto_message (e.g., created by
[`substrait_create()`](substrait_create.md))

## Examples

``` r
as_substrait(substrait$Type$Boolean$create(type_variation_reference = 1))
#> message of type 'substrait.Type.Boolean' with 1 field set
#> type_variation_reference: 1
as_substrait_expression(4L)
#> message of type 'substrait.Expression' with 1 field set
#> literal {
#>   i32: 4
#> }
as_substrait_expression(3.14)
#> message of type 'substrait.Expression' with 1 field set
#> literal {
#>   fp64: 3.14
#> }
```
