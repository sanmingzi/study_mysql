# WHERE vs HAVING

## 区别

- WHERE 是将数据从磁盘读入内存的时候进行筛选的；HAVING 是将数据读入内存，然后再根据 HAVING 条件将不符合的数据删除；在 WHERE 和 HAVING 都能使用的情况下，WHERE 的效率更高
- HAVING 条件中可以使用字段别名，WHERE 不可以
- HAVING 条件中可以使用统计函数，WHERE 不可以
- HAVING 只能使用 SELECT 选中的字段，WHERE 条件中可以使用表中的全部字段

## 示例

```SQL
mysql> SELECT name AS n, sex AS s FROM students WHERE n = 'b';
ERROR 1054 (42S22): Unknown column 'n' in 'where clause'

mysql> SELECT name AS n, sex AS s FROM students HAVING n = 'b';
+------+------+
| n    | s    |
+------+------+
| b    | b    |
+------+------+
1 row in set (0.00 sec)
```

```SQL
mysql> SELECT name FROM students WHERE sex = 'b';
+------+
| name |
+------+
| b    |
+------+
1 row in set (0.00 sec)

mysql> SELECT name FROM students HAVING sex = 'b';
ERROR 1054 (42S22): Unknown column 'sex' in 'having clause'
```

```SQL
mysql> SELECT COUNT(name), birth FROM students WHERE COUNT(name) > 0 GROUP BY birth;
ERROR 1111 (HY000): Invalid use of group function

mysql> SELECT COUNT(name), birth FROM students GROUP BY birth HAVING COUNT(name) > 0;
+-------------+------------+
| COUNT(name) | birth      |
+-------------+------------+
|           1 | 1992-02-02 |
+-------------+------------+
1 row in set (0.00 sec)
```
