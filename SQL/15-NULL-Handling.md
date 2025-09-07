## A. Replacing `NULL` Values

### 1. `ISNULL(value, replacement_value)`

Replaces `NULL` with a specified value.

- **SQL Server**: `ISNULL()`
- **MySQL**: `IFNULL()`
- **Oracle**: `NVL()`
- **Examples**:
  - `ISNULL(primary_contact, secondary_contact)`
  - `ISNULL(email, 'unknown')`
- **Performance**: Fast

### 2. `COALESCE(value1, value2...valueN)`

Returns the first non-`NULL` value from the list.

- **Example**: `COALESCE(primary_contact, secondary_contact, 'unknown')`
- **Database Support**: Available in all major databases
- **Performance**: Slower compared to `ISNULL`

## 3. `NULLIF(value1, value2)`

- If both the values are equal, it returns NULL, otherwise first value will be returned
- **Example** - Preventing divide by zero.

## B. Checking for `NULL` Values - To identify missing information of particular entity & Left-Anti Join

1. `IS NULL` – Checks if a value is `NULL`
2. `IS NOT NULL` – Checks if a value is **not** `NULL`

## Handling NULL Usecases

1. **Handling `NULL` values before performing data aggregations**
   - Example: Calculating the average salary of all employees.
2. **Handling `NULL` values before mathematical operations**
   - Example: Concatenating `firstname` and `lastname`.
   - Example: Adding 10 bonus points to each customer, even if they previously had no points.
3. **Handling `NULL` values before joining tables**
4. **Handling `NULL` values before sorting data**
