---
title: "Nifty Redshift SQL Techniques"
subtitle: "Lesser-known but useful Redshift SQL functions and techniques"
category: SQL
tags: [sql, redshift, aws, techniques]
order: 4
---

A collection of Redshift SQL functions and techniques that don't get enough attention but can significantly simplify your queries.

## Querying Techniques

### Subqueries / WITH Clauses (CTEs)

Break larger queries into manageable sections, enabling sequential dataset transformations before reaching final results. Simple and efficient for building up complex logic incrementally.

### LISTAGG()

Aggregate function that concatenates row values within groups into a single string:

```sql
LISTAGG( [DISTINCT] aggregate_expression [, 'delimiter'] )
  WITHIN GROUP (ORDER BY order_list)
```

Complementary function: `split_to_array()` for the reverse operation.

### ROW_NUMBER()

Assigns sequential ordinal numbers to rows within partitioned groups, resetting for each partition:

```sql
SELECT ROW_NUMBER() OVER(
  [PARTITION BY expr_list]
  [ORDER BY order_list]
) FROM table_name;
```

### QUALIFY and HAVING

`QUALIFY` filters window function results without requiring subqueries — addressing a common pain point where you'd otherwise need to nest your query just to filter on a window function result.

### CONNECT BY

Designed for hierarchical, tree-structured data. Enables retrieving records at specified degrees of separation from a reference point. Useful for org charts, category trees, and similar recursive structures.

## Data Transformation

### GROUPING SETS

Equivalent to running multiple `GROUP BY` queries with `UNION ALL`, but in a single pass:

```sql
SELECT category, product, sum(cost) as total
FROM orders
GROUP BY GROUPING SETS(category, product);
```

### ROLLUP

Returns subtotal rows at all grouping levels plus grand totals:

```sql
GROUP BY ROLLUP((a), (b))
```

### CUBE

Similar to `ROLLUP` but returns subtotal rows for **all** column combinations:

```sql
GROUP BY CUBE(category, product) ORDER BY 1, 2;
```

### PIVOTS

Transposes data for alternative perspectives on a dataset. Especially useful for reporting where you need columns to represent what were previously row values.

## Data Experimentation

### CHECKSUM with MOD()

Useful for stratified sampling and pipeline validation:

```sql
WHERE mod(checksum(customer_id), 1000) = 1
```

### SHOW COLUMNS

Quick way to retrieve column metadata:

```sql
WITH temp_col AS (SHOW COLUMNS FROM TABLE dev.public.tb)
SELECT count(*) FROM temp_col;
```
