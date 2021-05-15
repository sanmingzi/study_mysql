# 外键 (Foreign Key)

## 场景

引用完整性约束：当一列或者多列声明外键约束后，这些列中的数据必须在其父表的主键或者唯一字段的列中存在。

## 反模式

不使用外键的原因：
- 数据更新和删除有可能和约束冲突
- 当前数据库设计太灵活，不支持引用完整性约束
- 数据库为外键建立的索引会影响性能
- 当前使用的数据库不支持外键

如果无视约束的话就需要编写程式代码来确保数据间的关系。

```SQL
SELECT bug_id FROM bugs WHERE reported_id = 1;
DELETE FROM accounts WHERE account_id = 1;
```

我们在删除 account#1 之前必须先确认没有 bugs 引用了该记录，然后才能进行删除。

如果 account#1 恰巧在删除操作的查询和删除语句的间隙插入了一条 bug 记录，就会产生一条由不存在的用户提交的 bug 。

为了解决这个问题，我们有两个方案：
1. 必须在删除操作的时候，锁住 bugs 表。但是这在高并发和大数据的情况下十分影响性能。
2. 编写脚本检查数据库中存在的错误数据，对错误数据进行清理 / 修复。但问题接踵而至，如何执行脚本，多久执行一次脚本。

## 声明外键约束

```SQL
CREATE TABLE bugs (
  -- ...
  reported_by BIGINT UNSIGNED NOT NULL,
  status VARCHAR(20) NOT NULL DEFAULT 'NEW',
  FOREIGN KEY (reported_by) REFERENCES accounts(account_id)
    ON UPDATE CASCADE
    ON DELETE RESTRICT,
  FOREIGN KEY (status) REFERENCES bug_status(status)
    ON UPDATE CASCADE
    ON DELETE SET DEFAULT
);
```

通过使用外键，能够避免编写不必要的代码，并且外键支持同步更新和删除。

好处：
- 不需要在更新和删除记录前执行 SELECT 进行检查
- 在同步修改时不需要再锁住整张表
