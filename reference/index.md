# Package index

## Dplyr verbs

Implementations of dplyr verbs that can be used to generate Substrait
plans

- [`select(`*`<SubstraitCompiler>`*`)`](select.SubstraitCompiler.md)
  [`rename(`*`<SubstraitCompiler>`*`)`](select.SubstraitCompiler.md)
  [`rename_with(`*`<SubstraitCompiler>`*`)`](select.SubstraitCompiler.md)
  [`filter(`*`<SubstraitCompiler>`*`)`](select.SubstraitCompiler.md)
  [`mutate(`*`<SubstraitCompiler>`*`)`](select.SubstraitCompiler.md)
  [`transmute(`*`<SubstraitCompiler>`*`)`](select.SubstraitCompiler.md)
  [`arrange(`*`<SubstraitCompiler>`*`)`](select.SubstraitCompiler.md)
  [`group_by(`*`<SubstraitCompiler>`*`)`](select.SubstraitCompiler.md)
  [`ungroup(`*`<SubstraitCompiler>`*`)`](select.SubstraitCompiler.md)
  [`summarise(`*`<SubstraitCompiler>`*`)`](select.SubstraitCompiler.md)
  [`summarize(`*`<SubstraitCompiler>`*`)`](select.SubstraitCompiler.md)
  [`collect(`*`<SubstraitCompiler>`*`)`](select.SubstraitCompiler.md)
  [`relocate(`*`<SubstraitCompiler>`*`)`](select.SubstraitCompiler.md)
  [`semi_join(`*`<SubstraitCompiler>`*`)`](select.SubstraitCompiler.md)
  [`anti_join(`*`<SubstraitCompiler>`*`)`](select.SubstraitCompiler.md)
  [`inner_join(`*`<SubstraitCompiler>`*`)`](select.SubstraitCompiler.md)
  [`left_join(`*`<SubstraitCompiler>`*`)`](select.SubstraitCompiler.md)
  [`right_join(`*`<SubstraitCompiler>`*`)`](select.SubstraitCompiler.md)
  [`full_join(`*`<SubstraitCompiler>`*`)`](select.SubstraitCompiler.md)
  [`distinct(`*`<SubstraitCompiler>`*`)`](select.SubstraitCompiler.md)
  [`count(`*`<SubstraitCompiler>`*`)`](select.SubstraitCompiler.md) :
  dplyr verb implementations

## Create substrait relations

Functions used to create substrait relations

- [`substrait_sort()`](substrait_sort.md)
  [`substrait_sort_field()`](substrait_sort.md) : Append a Substrait
  Project Relation
- [`substrait_project()`](substrait_project.md)
  [`substrait_select()`](substrait_project.md) : Append a Substrait
  Project Relation
- [`substrait_filter()`](substrait_filter.md) : Append a Substrait
  Project Relation
- [`substrait_aggregate()`](substrait_aggregate.md)
  [`substrait_group_by()`](substrait_aggregate.md)
  [`substrait_ungroup()`](substrait_aggregate.md) : Aggregate
- [`substrait_fetch()`](substrait_fetch.md) : Append a Substrait Fetch
  Relation
- [`substrait_join()`](substrait_join.md)
  [`join_name_repair_none()`](substrait_join.md)
  [`join_name_repair_suffix_common()`](substrait_join.md)
  [`join_emit_all()`](substrait_join.md)
  [`join_emit_default()`](substrait_join.md) : Append a Substrait Join
  relation

## Create substrait objects

Functions used to create substrait objects

- [`substrait_create()`](substrait_create.md)
  [`substrait`](substrait_create.md) : Create 'Substrait' message
  objects
- [`as_substrait()`](as_substrait.md)
  [`from_substrait()`](as_substrait.md)
  [`as_substrait_expression()`](as_substrait.md)
  [`as_substrait_type()`](as_substrait.md) : Convert to and from
  'Substrait' messages
- [`substrait_boolean()`](substrait-type.md)
  [`substrait_i8()`](substrait-type.md)
  [`substrait_i16()`](substrait-type.md)
  [`substrait_i32()`](substrait-type.md)
  [`substrait_i64()`](substrait-type.md)
  [`substrait_fp32()`](substrait-type.md)
  [`substrait_fp64()`](substrait-type.md)
  [`substrait_string()`](substrait-type.md)
  [`substrait_binary()`](substrait-type.md)
  [`substrait_timestamp()`](substrait-type.md)
  [`substrait_timestamp_tz()`](substrait-type.md)
  [`substrait_date()`](substrait-type.md)
  [`substrait_time()`](substrait-type.md)
  [`substrait_interval_year()`](substrait-type.md)
  [`substrait_interval_day()`](substrait-type.md)
  [`substrait_uuid()`](substrait-type.md) : Substrait types

## Substrait compilers

Functions for creating substrait compilers

- [`substrait_compiler()`](substrait_compiler.md) : Initialize a
  Substrait Compiler
- [`arrow_substrait_compiler()`](arrow_substrait_compiler.md) : Create
  an Arrow Substrait Compiler
- [`duckdb_substrait_compiler()`](duckdb_substrait_compiler.md) : Create
  an DuckDB Substrait Compiler

## DuckDB Substrait Interface

An interface to the DuckDB Substrait Implementation

- [`duckdb_get_substrait()`](duckdb_get_substrait.md)
  [`duckdb_from_substrait()`](duckdb_get_substrait.md)
  [`has_duckdb_with_substrait()`](duckdb_get_substrait.md) : DuckDB
  Substrait Interface

## Low-level compiler details

Tools for developing substrait compiler interfaces

- [`SubstraitCompiler`](SubstraitCompiler.md) : Substrait Compiler
- [`current_compiler()`](current_compiler.md)
  [`with_compiler()`](current_compiler.md)
  [`local_compiler()`](current_compiler.md) : Compiler context
- [`substrait_call()`](substrait_call.md)
  [`substrait_call_agg()`](substrait_call.md)
  [`substrait_eval()`](substrait_call.md)
  [`substrait_eval_data()`](substrait_call.md) : Translation utilities

## Example datasets

- [`example_data`](example_data.md) : Example data
