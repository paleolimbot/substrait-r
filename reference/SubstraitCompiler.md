# Substrait Compiler

Substrait Compiler

Substrait Compiler

## Details

The SubstraitCompiler defines a mutable object that accumulates
information needed to evaluate a `substrait.Rel` tree. In addition to
the `substrait.Rel` tree itself, the compiler must keep track of
function identifiers, column names, and the R objects (e.g., data
frames) that will be used as leaf nodes when the plan is evaluated.
Specific consumers will need to subclass the SubstraitCompiler and
implement the `$evaluate()` and/or `$resolve_function()` methods.
Typically users will not interact with R6 methods but will use the
pipeable interface (e.g. [`substrait_select()`](substrait_project.md)).
The pipeable interface clones the compiler before it is modified to
minimize the user's interaction to R6 reference semantics.

Get a function reference identifier for a given function/input argument
combination.

## Public fields

- `rel`:

  The root of the current `substrait.Rel` tree.

- `schema`:

  A `substrait.NamedStruct` containing the field names and field types
  of `rel`.

- `.data`:

  An environment or list containing `substrait.Expression` objects. For
  a fresh compiler, this will be a list of field references with the
  same length as `schema$names`; however, during evaluation this may be
  updated to contain temporary columns before a relation is finalized.

- `.fns`:

  An environment or list containing functions that can be translated by
  this compiler.

- `groups`:

  A named list of `substrait.Expression` to be used for future grouping
  (e.g., after calling
  [`dplyr::group_by()`](https://dplyr.tidyverse.org/reference/group_by.html)).

## Methods

### Public methods

- [`SubstraitCompiler$new()`](#method-SubstraitCompiler-new)

- [`SubstraitCompiler$eval_mask()`](#method-SubstraitCompiler-eval_mask)

- [`SubstraitCompiler$add_relation()`](#method-SubstraitCompiler-add_relation)

- [`SubstraitCompiler$add_named_table()`](#method-SubstraitCompiler-add_named_table)

- [`SubstraitCompiler$named_table()`](#method-SubstraitCompiler-named_table)

- [`SubstraitCompiler$named_table_list()`](#method-SubstraitCompiler-named_table_list)

- [`SubstraitCompiler$validate()`](#method-SubstraitCompiler-validate)

- [`SubstraitCompiler$plan()`](#method-SubstraitCompiler-plan)

- [`SubstraitCompiler$evaluate()`](#method-SubstraitCompiler-evaluate)

- [`SubstraitCompiler$resolve_function()`](#method-SubstraitCompiler-resolve_function)

- [`SubstraitCompiler$function_id()`](#method-SubstraitCompiler-function_id)

- [`SubstraitCompiler$extension_uri_anchor()`](#method-SubstraitCompiler-extension_uri_anchor)

- [`SubstraitCompiler$function_extension()`](#method-SubstraitCompiler-function_extension)

- [`SubstraitCompiler$next_id()`](#method-SubstraitCompiler-next_id)

- [`SubstraitCompiler$clone()`](#method-SubstraitCompiler-clone)

------------------------------------------------------------------------

### Method `new()`

Create a new SubstraitCompiler.

#### Usage

    SubstraitCompiler$new(object = NULL, ...)

#### Arguments

- `object`:

  An object, most commonly a data.frame or table-like object.

- `...`:

  Passed to `add_relation()` if `object` is not `NULL`

------------------------------------------------------------------------

### Method `eval_mask()`

Returns the [data
mask](https://rlang.r-lib.org/reference/as_data_mask.html) that will be
used within [`substrait_eval()`](substrait_call.md).

#### Usage

    SubstraitCompiler$eval_mask(.data = TRUE)

#### Arguments

- `.data`:

  Use `FALSE` to return a mask containing only function members with no
  columns.

------------------------------------------------------------------------

### Method `add_relation()`

Sets the `rel` of this compiler to a `substrait.Rel` (usually a
`substrait.Rel.ReadRel`) and sets `schema` and `mask` to represent the
root of the relation tree.

#### Usage

    SubstraitCompiler$add_relation(object, ...)

#### Arguments

- `object`:

  An object, most commonly a data.frame or table-like object.

- `...`:

  Unused by the default method

------------------------------------------------------------------------

### Method `add_named_table()`

Registers an object for use as a named table with this compiler.

#### Usage

    SubstraitCompiler$add_named_table(object, ...)

#### Arguments

- `object`:

  An object, most commonly a data.frame or table-like object.

- `...`:

  Unused by the default method

#### Returns

A substrait.ReadRel that refers to `object` when used with this
compiler.

------------------------------------------------------------------------

### Method `named_table()`

Retrieve a named table

#### Usage

    SubstraitCompiler$named_table(name)

#### Arguments

- `name`:

  A table name

#### Returns

The `object` that was passed

------------------------------------------------------------------------

### Method `named_table_list()`

Retrieve all named tables as a
[`list()`](https://rdrr.io/r/base/list.html)

#### Usage

    SubstraitCompiler$named_table_list()

#### Returns

a named [`list()`](https://rdrr.io/r/base/list.html) of objects

------------------------------------------------------------------------

### Method `validate()`

Validates a compiler after it was modified. This is an opportunity to
provide meaningful feedback (e.g., errors, warnings)

#### Usage

    SubstraitCompiler$validate()

#### Returns

`self`

------------------------------------------------------------------------

### Method `plan()`

Assembles a `substrait.Plan` from the current information available to
the compiler.

#### Usage

    SubstraitCompiler$plan()

#### Returns

A `substrait.Plan`

------------------------------------------------------------------------

### Method `evaluate()`

Evaluates the plan being built by the compiler.

#### Usage

    SubstraitCompiler$evaluate(...)

#### Arguments

- `...`:

  Extra arguments specific to the compiler type.

#### Returns

A table-like object whose structure is defined by the SubstraitCompiler
class. The returned object should have a
[`as.data.frame()`](https://rdrr.io/r/base/as.data.frame.html) method.

------------------------------------------------------------------------

### Method `resolve_function()`

Resolves an R function call as a Substrait function call.

#### Usage

    SubstraitCompiler$resolve_function(
      name,
      args,
      template,
      output_type = NULL,
      options = NULL
    )

#### Arguments

- `name`:

  The fully-qualified name of the function as it was called (e.g.,
  `pkg::fun`). If no package name was explicitly specified, the package
  name will not be present in `name`.

- `args`:

  A [`list()`](https://rdrr.io/r/base/list.html) of arguments. These may
  be R objects or Substrait objects created while evaluating the
  user-provided arguments (e.g., field references or function calls).

- `template`:

  A `substrait.Expression.ScalarFunction`, a
  `substrait.Expression.WindowFunction`, or a
  `substrait.AggregateFunction`.

- `output_type`:

  An explicit output type to use or a function accepting one type per
  `args`.

- `options`:

  An optional list of `substrait.FunctionOptions` message specifying
  function options for this call.

#### Returns

A modified `template` with `function_reference`, `args`, and
`output_type` set.

------------------------------------------------------------------------

### Method `function_id()`

#### Usage

    SubstraitCompiler$function_id(name, arg_types)

#### Arguments

- `name`:

  The fully-qualified name of the function as it was called (e.g.,
  `pkg::fun`). If no package name was explicitly specified, the package
  name will not be present in `name`.

- `arg_types`:

  A [`list()`](https://rdrr.io/r/base/list.html) of `substrait.Type`
  objects.

#### Returns

An integer function reference

------------------------------------------------------------------------

### Method `extension_uri_anchor()`

Get the extension uri anchor value for a given function

#### Usage

    SubstraitCompiler$extension_uri_anchor(name)

#### Arguments

- `name`:

  The name of the function

#### Returns

The uri anchor value

------------------------------------------------------------------------

### Method `function_extension()`

Retrieve a function extension by anchor/reference

#### Usage

    SubstraitCompiler$function_extension(id)

#### Arguments

- `id`:

  An function_anchor/function_reference identifier

#### Returns

A `substrait.extensions.SimpleExtensionDeclaration.ExtensionFunction`.

------------------------------------------------------------------------

### Method `next_id()`

Get the next unique identifier.

#### Usage

    SubstraitCompiler$next_id()

#### Returns

An integer that has not been returned by a previous call to `next_id()`
for this instance.

------------------------------------------------------------------------

### Method `clone()`

The objects of this class are cloneable with this method.

#### Usage

    SubstraitCompiler$clone(deep = FALSE)

#### Arguments

- `deep`:

  Whether to make a deep clone.
