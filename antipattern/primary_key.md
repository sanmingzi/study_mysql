# 主键 (Primary Key)

## 场景

使用了主键却混淆了主键的本质而造成的反模式。比如有一张交叉表 bug_products 是这样设计的：

```SQL
CREATE TABLE bug_products (
  id SERIAL PRIMARY KEY,
  bug_id BIGINT UNSIGNED NOT NULL,
  product_id BIGINT UNSIGNED NOT NULL,
  FOREIGN KEY (bug_id) REFERENCES bugs (id),
  FOREIGN KEY (product_id) REFERENCES products (id)
);
```

这张表使用了惯例 id 作为主键，但是 id 并没有办法保证 (bug_id product_id) 的唯一性。

## 反模式

```SQL
CREATE TABLE bug_products (
  -- ...
  UNIQUE KEY (bug_id, product_id)
  -- ...
);
```

id 是伪主键，而真正用来确保唯一性的应该是 (bug_id, product_id) 。这时候我们是否可以删掉 id 了呢？ TODO ???

## 裁剪设计

```ruby
class Bug < ActiveRecord::Base
  set_primary_key 'bug_id'
end
```

约定大于配置 ??? TODO ???
