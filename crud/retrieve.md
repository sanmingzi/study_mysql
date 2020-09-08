# retrieve

[Retrieving Information from a Table](https://dev.mysql.com/doc/mysql-tutorial-excerpt/5.7/en/retrieving-data.html)

## WHERE

- operators

|||
| - | - |
| = | equal |
| <> | not equal |
| > | greater than |
| < | less than |
| >= | greater than or equal |
| <= | less than or equal |
| BETWEEN | between an inclusive range |
| LIKE | search fro a pattern |
| IN | specify multiple possible values |

```SQL
SELECT column_name FROM table_name WHERE column_name IN (value1, valu2, ...);
SELECT column_name FROM table_name WHERE column_name BETWEEN value1 and value2;
SELECT column_name FROM table_name WHERE column_name LIKE "John%";
```

- AND / OR / NOT

```SQL
SELECT * FROM pet WHERE (species = 'cat' AND sex = 'm') OR (species = 'dog' AND sex = 'f');

SELECT column1, column2 FROM table_name
WHERE condition1 AND condition2 AND condition3;

SELECT column1, column2 FROM table_name
WHERE condition1 OR condition2;

SELECT column1, column2 FROM table_name
WHERE NOT condition1 AND NOT condition2;
```

- User-Defined Variables

```m
SELECT @min_price:=MIN(price),@max_price:=MAX(price) FROM shop;
SELECT * FROM shop WHERE price=@min_price OR price=@max_price;
```

- DISTINCT

```m
SELECT owner FROM pet;
SELECT DISTINCT owner FROM pet;
SELECT DISTINCT column1, column2 from table_name;

只要column1, column2有一个是不同的，则认为是不同的。
只有当column1, column2都是相同的，才会只显示一条记录。
```

- ORDER BY / DESC

```SQL
SELECT name, birth FROM pet ORDER BY birth;
SELECT name, birth FROM pet ORDER BY birth DESC;

默认是按照升序排列，通过DESC关键字可以按照降序排列。

SELECT name, birth FROM pet ORDER BY birth, name DESC;

DESC 关键字只会影响到其前面的第一个字段，所以上述结果会按照 birth 升序，然后再按照 name 降序排列。
```

```m
SELECT name, species, birth FROM pet ORDER BY species, birth DESC;


当我们根据多个字段进行排序时，放在前面的字段优先级最高。DESC关键字只会影响在其前面的第一个字段，上述例子中，只会影响birth字段。
```

- COUNT / AVG / SUM / MAX / MIN

```SQL
SELECT COUNT(column1) FROM table_name WHERE condition1;
SELECT AVG(column1) FROM table_name WHERE condition1;
SELECT SUM(column1) FROM table_name WHERE condition1;
SELECT MAX(article) AS article FROM shop;
```

```SQL
SELECT article, dealer, price FROM shop
WHERE  price=(SELECT MAX(price) FROM shop);

通过上述SQL我们可以找到最贵的商品的信息。
```

- GROUP BY

```SQL
SELECT owner, COUNT(*) FROM pet GROUP BY owner;

GROUP BY 经常和 COUNT / AVG / SUM / MAX / MIN 一起使用。
```

- HAVING

```SQL
WHERE 不能用于聚合函数，比如 COUNT / AVG / SUM 等等，但是 HAVING 可以。
简单来说就是 WHERE 用在 GROUP BY 之前，但是 HAVING 可以用在 GROUP BY 后面。

SELECT column1, column2 FROM table_name
WHERE condition
GROUP BY column1
HAVING condition
ORDER BY column1;

SELECT Email FROM Person GROUP BY Email HAVING COUNT(*) > 1;

这个查询语句能够查询出Person表中重复的Email。
```

- 第k大

- LIMIT / OFFSET

```SQL
SELECT column1, column2 FROM table_name
WHERE condition
LIMIT number;
```

- COALESCE

```SQL
COALESCE 会返回列表中的第1个非空数据.

SELECT COALESCE(NULL, NULL, NULL, NULL, 'Example.com');
```

- NULL

```SQL
SELECT name FROM persons WHERE name IS NOT NULL;
```

## practice

- [超过经理收入的员工](https://leetcode-cn.com/problems/employees-earning-more-than-their-managers/)
- [第二高的薪水](https://leetcode-cn.com/problems/second-highest-salary/)
- [第N高的薪水](https://leetcode-cn.com/problems/nth-highest-salary/)
- [连续出现的数字](https://leetcode-cn.com/problems/consecutive-numbers/)
- [查找重复的电子邮箱](https://leetcode-cn.com/problems/duplicate-emails/)
- [上升的温度](https://leetcode-cn.com/problems/rising-temperature/)
- [大的国家](https://leetcode-cn.com/problems/big-countries/)
- [有趣的电影](https://leetcode-cn.com/problems/not-boring-movies/)
- [重新格式化部门表](https://leetcode-cn.com/problems/reformat-department-table/)
- [部门工资最高的员工](https://leetcode-cn.com/problems/department-highest-salary/)
- [部门工资前三高的所有员工](https://leetcode-cn.com/problems/department-top-three-salaries/)
- [分数排名](https://leetcode-cn.com/problems/rank-scores/)
- [行程和用户](https://leetcode-cn.com/problems/trips-and-users/)
- [超过5名学生的课](https://leetcode-cn.com/problems/classes-more-than-5-students/)
- [体育馆的人流量](https://leetcode-cn.com/problems/human-traffic-of-stadium/)
- [换座位](https://leetcode-cn.com/problems/exchange-seats/)
