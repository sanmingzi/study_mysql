# union

UNION 操作可以将两个或者多个 SELECT 的查询结果合并为一个结果。使用 UNION 有一些前提条件：

- 多个 SELECT 查询的列数必须相同
- 多个 SELECT 查询的列名必须相同
- 多个 SELECT 查询的列的顺序必须相同
- 多个 SELECT 查询的列的类型必须相似

## UNION

```SQL
SELECT column1, column2 FROM table1
UNION
SELECT column1, column2 FROM table2;
```

## UNION ALL

UNION 操作默认去重，为了允许出现 duplicate values，我们需要使用 UNION ALL。

```SQL
SELECT column1, column2 FROM table1
UNION ALL
SELECT column1, column2 FROM table2;
```
