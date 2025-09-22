## A. Replacing `NULL` Values

### 1. ISNULL(value, replacement_value) - Replaces `NULL` with a specified value.

- **SQL Server**: `ISNULL()`
- **MySQL**: `IFNULL()`
- **Oracle**: `NVL()`
- **Performance**: Fast

### 2. `COALESCE(value1, value2...valueN)` - Returns the first non-`NULL` value from the list.

- **Database Support**: Available in all major databases
- **Performance**: Slower compared to `ISNULL`

## 3. NULLIF(value1, value2)

- If both the values are equal, it returns NULL, otherwise first value will be returned
- **Example** - Preventing divide by zero.

## B. Checking for `NULL` Values - To identify missing information of particular entity & Left-Anti Join

1. `IS NULL` – Checks if a value is `NULL`
2. `IS NOT NULL` – Checks if a value is **not** `NULL`

## Handling NULL Usecases

1. **Handling `NULL` values before performing data aggregations**
   - Example - Primary Contact / Secondary Contact
   - Product prices: [10, NULL, 35]
   - The sum of non-NULL values is 10 + 35 = 45
   - Since NULL is ignored in aggregation, the average is calculated over 2 products, not 3
   - Average = 45 / 2 = 22.5
   - Aggregate functions in SQL ignore NULL values—except for `COUNT(*)`, which includes all rows regardless of NULL.
2. **Handling `NULL` values before mathematical operations**
   - Example: Concatenating `firstname` and `lastname`.
   - Example: Adding 10 bonus points (Score + 10) to each customer, even if they previously had no points.
3. **Handling `NULL` values before joining tables**
4. **Handling `NULL` values before sorting data**
