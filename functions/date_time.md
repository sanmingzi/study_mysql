# Date and Time Function

- [w3schools](https://www.w3schools.com/sql/func_mysql_adddate.asp)

## 当前日期 / 时间

```SQL
SELECT CURDATE() AS DATE;
SELECT CURRENT_DATE() AS DATE;
+------------+
| DATE       |
+------------+
| 2021-01-05 |
+------------+

SELECT CURTIME() AS TIME;
SELECT CURRENT_TIME() AS TIME;
+----------+
| TIME     |
+----------+
| 07:00:35 |
+----------+

SELECT NOW() AS NOW;
SELECT CURRENT_TIMESTAMP() AS NOW;
+---------------------+
| NOW                 |
+---------------------+
| 2021-01-05 06:59:01 |
+---------------------+
```

## 当前年月日时分秒

```SQL
SELECT YEAR(CURDATE()) AS YEAR;

SELECT MONTH(CURDATE()) AS MONTH;
SELECT MONTHNAME(CURDATE()) AS MONTH;
+---------+
| MONTH   |
+---------+
| January |
+---------+

SELECT DAY(CURDATE()) AS DAY;
SELECT DAYNAME(CURDATE()) AS DAY;
+---------+
| DAY     |
+---------+
| Tuesday |
+---------+

-- 0 = Monday, 1 = Tuesday, 2 = Wednesday, 3 = Thursday, 4 = Friday, 5 = Saturday, 6 = Sunday
SELECT WEEKDAY(CURDATE()) AS WEEKDAY;
+---------+
| WEEKDAY |
+---------+
|       1 |
+---------+

-- 1=Sunday, 2=Monday, 3=Tuesday, 4=Wednesday, 5=Thursday, 6=Friday, 7=Saturday.
SELECT DAYOFWEEK(CURDATE()) AS DAYOFWEEK;
+-----------+
| DAYOFWEEK |
+-----------+
|         3 |
+-----------+

SELECT DAYOFYEAR(CURDATE()) AS DAYOFFYEAR;
+------------+
| DAYOFFYEAR |
+------------+
|          5 |
+------------+

-- (a number from 1 to 53)
SELECT WEEKOFYEAR(CURDATE()) AS WEEKOFYEAR;
+------------+
| WEEKOFYEAR |
+------------+
|          1 |
+------------+

SELECT HOUR(CURTIME()) AS HOUR;
SELECT MINUTE(CURTIME()) AS MINUTE;
SELECT SECOND(CURTIME()) AS SECOND;
SELECT MICROSECOND("2017-06-20 09:34:00.000023") AS MICROSECOND;

-- January-March returns 1
-- April-June returns 2
-- July-Sep returns 3
-- Oct-Dec returns 4
SELECT QUARTER(CURTIME()) AS QUARTER;
```

## 最后一天

```SQL
SELECT LAST_DAY("2021-01-05") AS LAST_DAY;
+------------+
| LAST_DAY   |
+------------+
| 2021-01-31 |
+------------+
```

## 修改时间

```SQL
SELECT ADDDATE("2017-06-15", INTERVAL 10 DAY);
SELECT ADDDATE("2017-06-15 09:34:21", INTERVAL 15 MINUTE);
SELECT ADDDATE("2017-06-15 09:34:21", INTERVAL -3 HOUR);

SELECT SUBDATE("2017-06-15", INTERVAL 10 DAY);

SELECT DATE_ADD("2017-06-15", INTERVAL 10 DAY);
SELECT DATE_SUB("2017-06-15", INTERVAL 10 DAY);

SELECT ADDTIME("2017-06-15 09:34:21", "2") AS NEW_TIME;
+---------------------+
| NEW_TIME            |
+---------------------+
| 2017-06-15 09:34:23 |
+---------------------+

SELECT ADDTIME("2017-06-15 09:34:21.000001", "5 2:10:5.000003") AS NEW_TIME;
+----------------------------+
| NEW_TIME                   |
+----------------------------+
| 2017-06-20 11:44:26.000004 |
+----------------------------+

SELECT ADDTIME("2017-06-15 09:34:21.000001", "-15 2:10:5.000003") AS NEW_TIME;
+----------------------------+
| NEW_TIME                   |
+----------------------------+
| 2017-05-31 07:24:15.999998 |
+----------------------------+

-- 下面这个例子是有问题的，06-15 增加 100 天之后并不是 07-20
-- 第 2 个参数中的 day 太大了，导致结果错误
-- 暂时并没有找到 day 的限制大小
-- 如果需要增加 day 的话还是建议使用 ADDDATE
SELECT ADDTIME("2017-06-15 09:34:21.000001", "100 2:10:5.000003") AS NEW_TIME;
+----------------------------+
| NEW_TIME                   |
+----------------------------+
| 2017-07-20 08:34:20.000001 |
+----------------------------+

SELECT SUBTIME("2017-06-15 10:24:21.000004", "5.000001");
```

## 时间差

```SQL
SELECT DATEDIFF("2017-06-25 09:34:21", "2017-06-15 15:25:35") AS DATEDIFF;
SELECT DATEDIFF("2017-06-25 00:00:00", "2017-06-15 23:59:59") AS DATEDIFF;
SELECT DATEDIFF("2017-06-25", "2017-06-15") AS DATEDIFF;
+----------+
| DATEDIFF |
+----------+
|       10 |
+----------+

SELECT TIMEDIFF("13:10:11", "13:10:10") AS TIMEDIFF;
+----------+
| TIMEDIFF |
+----------+
| 00:00:01 |
+----------+
```

## 格式化

- [w3schools MySQL DATE_FORMAT()](https://www.w3schools.com/sql/func_mysql_date_format.asp)

- [w3schools MySQL TIME_FORMAT()](https://www.w3schools.com/sql/func_mysql_time_format.asp)

```SQL
SELECT DATE_FORMAT("2021-01-05", "%M %D %Y") AS DATE;
+------------------+
| DATE             |
+------------------+
| January 5th 2021 |
+------------------+

SELECT DATE_FORMAT("2021-01-05", "%m-%d-%Y") AS DATE;
+------------+
| DATE       |
+------------+
| 01-05-2021 |
+------------+

SELECT TIME_FORMAT("19:30:10", "%H %i %s") AS TIME;
+----------+
| TIME     |
+----------+
| 19 30 10 |
+----------+
```
