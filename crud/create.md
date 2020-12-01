# Create

## INSERT

```m
INSERT INTO table_name (column1, column2 ...) VALUES (valu21, value2 ...);
INSERT INTO table_name (column1, column2 ...) VALUES (value1, value2 ...), (value1, value2 ...);
```

## REPLACE

```m
REPLACE INTO table_name (column1, column2 ...) VALUES (valu21, value2 ...);
```

## INSERT vs REPLACE

```m
REPLACE 和 INSERT 都能向数据库中添加新数据，但是他们有一个很大的区别。
如果插入的数据的主键已经存在于数据库中，那么使用 INSERT 会报错，但是使用 REPLACE 不会，REPLACE 会将原来的数据删除，然后插入新的数据。
```
