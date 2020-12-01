# Delete

## 删除数据

```
DELETE FROM table_name WHERE conditions;
DELETE table0, table1 FROM table0, table1 WHERE conditions;
```

## 清空表

```
DELETE FROM table_name;
DELETE table0, table1 FROM table0, table1;
TRUNCATE TABLE table_name;
```

- truncate是整体删除，delete是逐条删除，truncate速度更快
- truncate不写服务器log，delete写log，这也是truncate比delete效率高的原因
- truncate不激活trigger，但是会重置Identity，自增列会被重置为初始值。而delete删除后，Identity会接着被删除的最近一条记录的ID加1
- delete可以配合where用于删除部分记录，而truncate只能清空整个表

## 删除表

```
DROP TABLE table_name;
```

## Demo

| Id | Email            |
|----|------------------|
| 1  | john@example.com |
| 2  | bob@example.com  |
| 3  | john@example.com |

```
要求删除重复的电子邮件，重复的邮箱只保留 Id 最小的那个。
```

- 方法1

```sql
DELETE FROM person WHERE Id NOT IN
  (SELECT min_id 
    FROM (SELECT MIN(Id) as min_id FROM person GROUP BY email) AS min_ids);
```

- 方法2

```sql
DELETE p1 FROM person AS p1, person AS p2
  WHERE p1.Email = p2.Email AND p1.Id > p2.Id;
```

## Practice

- [LeetCode 0196 删除重复的电子邮箱](https://leetcode-cn.com/problems/delete-duplicate-emails/)
