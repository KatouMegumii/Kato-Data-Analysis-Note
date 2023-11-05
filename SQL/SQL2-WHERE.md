### `SELECT`的重要子句：`WHERE`

按照指定条件筛选行，需要注意的是，`WHERE`子句需要在`FROM`子句，也就是表名之后给出
```SQL
SELECT prod_name, prod_price FROM Products WHERE prod_price = 3.49
```