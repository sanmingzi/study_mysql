# Update

```m
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition1;
```

## Demo

| id | name | sex | salary |
|----|------|-----|--------|
| 1  | A    | m   | 2500   |
| 2  | B    | f   | 1500   |
| 3  | C    | m   | 5500   |
| 4  | D    | f   | 500    |

```sql
现在要求变更每一行的 sex，只能写一条 UPDATE，并且不能使用 SELECT。

UPDATE salary SET sex = (CASE sex WHEN 'm' THEN 'f' ELSE 'm' END);
```

## Practice

- [LeetCode 0627 变更性别](https://leetcode-cn.com/problems/swap-salary/submissions/)
