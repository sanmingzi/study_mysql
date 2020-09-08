# delete

## 清空表

```
DELETE FROM table_name;
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

## Practice

- [Leetcode_0196](https://leetcode-cn.com/problems/delete-duplicate-emails/)
