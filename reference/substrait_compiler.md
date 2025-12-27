# Initialize a Substrait Compiler

Creates a [SubstraitCompiler](SubstraitCompiler.md) instance initialized
with `object` (e.g., a
[`data.frame()`](https://rdrr.io/r/base/data.frame.html)).

## Usage

``` r
substrait_compiler(object, ...)

# S3 method for class 'SubstraitCompiler'
substrait_compiler(object, ...)

# Default S3 method
substrait_compiler(object, ...)
```

## Arguments

- object:

  A table-like object with which to create a compiler.

- ...:

  Passed to the [SubstraitCompiler](SubstraitCompiler.md) when creating
  a new compiler

## Value

An object of class 'substrait_compiler'

## Examples

``` r
substrait_compiler(data.frame(col1 = 1, col2 = "one"))
#> <SubstraitCompiler>
#>   Public:
#>     .agg_functions: NULL
#>     .data: list
#>     .fns: list
#>     add_named_table: function (object, ...) 
#>     add_relation: function (object, ...) 
#>     clone: function (deep = FALSE) 
#>     eval_mask: function (.data = TRUE) 
#>     evaluate: function (...) 
#>     extension_uri_anchor: function (name) 
#>     function_extension: function (id) 
#>     function_id: function (name, arg_types) 
#>     groups: NULL
#>     initialize: function (object = NULL, ...) 
#>     named_table: function (name) 
#>     named_table_list: function () 
#>     next_id: function () 
#>     plan: function () 
#>     rel: substrait_Rel, substrait_proto_message, substrait_proto
#>     resolve_function: function (name, args, template, output_type = NULL, options = NULL) 
#>     schema: substrait_NamedStruct, substrait_proto_message, substrait_proto
#>     validate: function () 
#>   Private:
#>     extension_uri: list
#>     function_extensions: list
#>     function_extensions_key: list
#>     id_counter: 2
#>     named_tables: list
#>     type_extensions: list
#>     type_variations: list
```
