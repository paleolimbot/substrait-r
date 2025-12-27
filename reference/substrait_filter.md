# Append a Substrait Project Relation

Append a Substrait Project Relation

## Usage

``` r
substrait_filter(.compiler, ...)
```

## Arguments

- .compiler:

  A [`substrait_compiler()`](substrait_compiler.md) or object that can
  be coerced to one

- ...:

  Filter expressions

## Value

A modified `.compiler`

## Examples

``` r
substrait_filter(
  duckdb_substrait_compiler(data.frame(a = 1, b = "one")),
  a > 0
)
#> <DuckDBSubstraitCompiler>
#>   Inherits from: <SubstraitCompiler>
#>   Public:
#>     .agg_functions: sum mean max min n n_distinct
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
#>     initialize: function (...) 
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
#>     id_counter: 3
#>     named_tables: list
#>     type_extensions: list
#>     type_variations: list
```
