# optimize

## 索引优化

### 单列索引 vs 复合索引

- http://www.open-open.com/lib/view/open1370089357102.html

## 收缩数据

- http://www.thinksaas.cn/group/topic/136/

```m
mysql删除数据后体积不变，所以需要手动优化收缩数据。可以使用如下命令：
OPTIMIZE TABLE tablename;

但是一定要注意，OPRIMIZE TABLE的过程中，mysql会锁定表。所以这种做法存在一定的风险，当表比较大的时候该方法耗时较长，也就意味着将比较长时间锁定表，这对于数据库读写是极为不利的。
```

## 解释查询

- http://www.open-open.com/lib/view/open1370089357102.html

```m
简单来说，就是 EXPLAIN 用来解释但并不执行某条SQL语句。我们能够通过解释的结果来判断该条SQL语句是否高效，数据库是否还能继续优化。

在解释的结果中，type 字段的内容很重要，如果 type 的内容是 range，说明优化比较成功。如果 type 为 index，说明该查询首先会查询索引表，然后再检索实际的数据，实际上也是全表扫描，只不过是先扫描有序的索引表，所以会比全表扫描快一些，但是还可以进一步优化。如果 type 为 all，会进行全表扫描，优化失败。
```
