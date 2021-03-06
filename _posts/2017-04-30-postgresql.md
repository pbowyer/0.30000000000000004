---
title: PostgreSQL
code:
 - 'SELECT 0.1::float + 0.2::float;'
 - 'SELECT 0.1 + 0.2;'
result:
 - '0.30000000000000004'
 - '0.3'
---
PostgreSQL treats decimal literals as [arbitrary precision numbers with fixed point](https://www.postgresql.org/docs/12/datatype-numeric.html#DATATYPE-NUMERIC-DECIMAL). Explicit type casts are required to get floating-point numbers.

PostgreSQL 11 and earlier outputs `0.3` as a result for query `SELECT 0.1::float + 0.2::float;`, but the result is rounded only for display, and under the hood it is still good old `0.30000000000000004`.

In PostgreSQL 12 default behavior for textual output of floats was changed from more human-readable rounded format to shortest-precise format. Format can be customized by the [`extra_float_digits`](https://www.postgresql.org/docs/12/runtime-config-client.html#GUC-EXTRA-FLOAT-DIGITS) configuration parameter.
