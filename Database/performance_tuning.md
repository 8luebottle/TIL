# Performance Tuning

### Table of Contents

* [Avoid](#avoid)
  * [WHERE](#where)

## Avoid
### WHERE
Avoid using the below operators in a WHERE clause due to index search is not working.

1. `NOT IN`  
  Case: use `NOT IN`
    ```sql
    -- DON'T
    SELECT name, id
    FROM customer
    WHERE status NOT IN ('3');
    ```

    ```sql
    -- DO
    SELECT name, id
    FROM customer
    WHERE satus IN ('0', '1', '2', '4');
    ```

    Recommend to use:
    - `IN`
    - `EXISTS`, `NOT EXISTS` [CHECK]

1. `<>, !=`  
  Case: use not equal operator (`<>`, `!=`)
    ```sql
    -- DON'T
    SELECT *
    FROM user
    WHERE gender != 0;
    ```

    ```sql
    -- DO
    SELECT *
    FROM user
    WHERE gender > 0;
    ```

    Recommend to use:
    - `=`
    - `>`, `>=`,
    - `<`, `<=`

1. `NOT BETWEEN`  
    Case: ranges with `NOT BETWEEN`
    ```sql
    -- DON'T
    SELECT name, publisher, price
    FROM book
    WHERE price NOT BETWEEN 0 AND 149;
    ```

    ```sql
    -- DO
    SELECT name, publisher, price
    FROM book
    WHERE price BETWEEN 150 AND 300;
    ```

    Recommend to use:
    - `BETWEEN`

1. `NULL`  
    Case: compare to `NULL`
    ```sql
    SELECT id, name, class
    FROM credit
    WHERE score IS NOT NULL;
    ```

    ```sql
    SELECT id, name, class
    FROM credit
    WHERE score > ``;
    ```

1. `LIKE %x%`  
  Case: starts with `%`
    ```sql
    -- DON'T
    SELECT area_code
    FROM location
    WHERE city LIKE '%San%';
    ```

    ```sql
    -- DO
    SELECT area_code
    FROM location
    WHERE city LIKE 'San%';
    ```

    Recommend to use:
    - `x%`

1. `OR`  
    Case: use `OR`

    Recommend to use:
    - `UNION ALL`

1. Converting values
