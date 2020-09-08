# functions

## CASE

```SQL
SELECT OrderID, Quantity,
  CASE
    WHEN Quantity > 30 THEN "The quantity is greater than 30"
    WHEN Quantity = 30 THEN "The quantity is 30"
    ELSE "The quantity is under 30"
  END
FROM OrderDetails;
```

## COALESCE

Return the first non-null value in a list.

```SQL
SELECT COALESCE(NULL, NULL, NULL, NULL, 'Example.com');
```

## IF

```SQL
IF(condition, value_if_true, value_if_false)

SELECT OrderID, Quantity, IF(Quantity>10, "MORE", "LESS")
FROM OrderDetails;
```

## IFNULL

Returns a specified value if the expression is NULL.

```SQL
IFNULL(expression, alt_value)

SELECT IFNULL(NULL, "W3Schools.com");
```