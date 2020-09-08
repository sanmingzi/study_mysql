# key_index

- https://www.cnblogs.com/sweet521/p/6203360.html
- https://www.cnblogs.com/yeyublog/p/5898588.html

## index

- 查看索引

```m
SHOW INDEX FROM table_name;
```

- 创建索引

```m
ALTER 可以用来创建普通索引、唯一索引、主键索引。

ALTER TABLE table_name ADD INDEX index_name (column0, column1 ...)
ALTER TABLE table_name ADD UNIQUE (column0, column1 ...)
ALTER TABLE table_name ADD PRIMARY KEY (column0, column1 ...)
```

```m
CREATE 可以用来创建普通索引、唯一索引。

CREATE INDEX index_name ON table_name (column0, column1 ...)
CREATE UNIQUE INDEX index_name ON table_name (column0, column1 ...)
```

- 删除索引

```m
DROP INDEX index_name ON talbe_name
ALTER TABLE table_name DROP INDEX index_name
ALTER TABLE table_name DROP PRIMARY KEY

删除PRIMARY KEY的时候需要注意，如果表中没有定义PRIMARY KEY索引，那么 MySQL 将删除第一个 UNIQUE 索引。
```

- 修改索引

```m
MySQL 没有修改索引的直接指令，所以我们需要删除原来的索引，再创建一个同名的索引。

DROP INDEX index_name ON table_name;
CREATE INDEX index_name ON table_name (column0, column1 ...);
```


- 检测 SQL 中索引是否有效

```m
我们使用 EXPLAIN 来检测某条 SQL 中是否使用了合适的索引。

EXPLAIN SELECT * FROM users WHERE age < 20;
```


## key

- 主键 & 复合主键

```m
主键是唯一索引，用于标识表中的一行数据，一个表只能有一个主键，主键是不能为空的。
如果表的主键由多个字段组成，那我们就称之为复合主键。
```

- 外键

```m
外键是用于加强两个表数据之间的链接的一列或者多列。
表的外键就是另一个表的主键。
一张表可以关联多张表，所以一张表可以有多个外键。
一般来讲，要删除一张表的主键，首先要确保其他表中没有相同的外键。
```

- 唯一索引

```m
```

##

- 外键检查