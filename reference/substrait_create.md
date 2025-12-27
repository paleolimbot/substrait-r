# Create 'Substrait' message objects

The 'Substrait' system of objects is made up of a series of nested types
serializable to the Protocol Buffer binary format. You can create these
objects using `substrait_create()`, or the namespace-style constructor
object substrait. Convert an existing object to a Substrait message
using [`as_substrait()`](as_substrait.md), and convert an existing
object back to an R object using [`from_substrait()`](as_substrait.md).

## Usage

``` r
substrait_create(.qualified_name, ...)

substrait
```

## Format

An object of class `list` of length 37.

## Arguments

- .qualified_name:

  The fully qualified name of the message type or enum (e.g.,
  "substrait.Type.Boolean")

- ...:

  Arguments passed to the constructor. rlang-style tidy dots are
  supported.

## Value

An object of class "substrait_proto".

## Details

Under the hood, substrait objects are
[`raw()`](https://rdrr.io/r/base/raw.html) vectors containing the
underlying binary protocol buffer serialization. This may not be the
case in the future, but is done here to separate the protocol buffer
reader/writer (currently RProtoBuf) from object conversion to facilitate
getting started on the conversion code.

## Examples

``` r
substrait_create("substrait.Type.Boolean", type_variation_reference = 1)
#> message of type 'substrait.Type.Boolean' with 1 field set
#> type_variation_reference: 1
substrait$Type$Boolean$create(type_variation_reference = 1)
#> message of type 'substrait.Type.Boolean' with 1 field set
#> type_variation_reference: 1
```
