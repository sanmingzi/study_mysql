# 单纯的树 (Simple Tree)

## 场景

读者可以评论原文，甚至相互回复，设计 comments 。这种场景可以理解为如何处理存在递归关系的数据。

## 反模式

comments 表中添加 parent_id 字段，用来表示其父节点。

无法查询一个节点的所有后代，删除一个节点也会变得复杂。

## 路径枚举

comments 表添加字段 path 表示路径，比如 1/4/6/7/ 表示第 7 条评论的父节点有 1-4-6 。查询 #7 的所有父节点可以这样做：

```SQL
SELECT * FROM comments c
WHERE '1/4/6/7/' LIKE c.path || '%';
```

如果要查询一个节点的所有后代也非常简单。

```SQL
SELECT * FROM comments c
WHERE c.path LIKE '1/4/6/7/' || '%';
```

缺点：

这个做法会带来 “乱穿马路” 反模式所存在的问题。

1. 无法保证 path 的格式总是正确或者路径中的节点总是存在
2. 依赖逻辑代码来维护 path
3. 存在长度限制，不可能无限扩展

## 闭包表

comments 表只单纯的表示 comment ，并不带有任何树相关的信息。我们新建一张表 tree_paths 来表示树。

```SQL
CRETE TABLE tree_paths (
  ancestor BIGINT UNSIGNED NOT NULL,
  descendant BIGINT UNSIGNED NOT NULL,
  PRIMARY KEY(ancesrot, descendant),
  FOREIGN KEY (ancestor) REFERENCES comments(id),
  FOREIGN KEY (descendant) REFERENCES comments(id)
);
```

要获取 comment#7 的祖先，可以这样做：

```SQL
SELECT c.*
FROM comments c
JOIN tree_paths t ON c.id = t.ancestor
WHERE t.descendant = 7;
```

我们还可以通过加入字段 path_length 来直接获取某个节点的父子节点。获取 comment#7 的父节点：

```SQL
SELECT c.*
FROM comments c
JOIN tree_paths t ON c.id = t.ancestor
WHERE t.descendant = 7
AND t.path_length = 1;
```

## 结论 (Conclusion)

闭包表是最通用的设计，只有该设计可以满足允许一个节点属于多棵树。它使用一张额外的表来存储关系，使用空间换时间的方案来提高操作效率。
