### `SELECT`语句及其子句和注意用法

#### 1. 基础功能

通配符`*`可以返回表中所有列

关键字`DISTINCT`可以只返回列中不同的数据，并且只能放在列名前，作用于所有列名，例子中对`column_name1`和`column_name2`都会返回不同行

```sql
SELECT column_name FROM dataset
SELECT * FROM dataset
SELECT DISTINCT column_name1 column_name2 FROM dataset 
```

#### 2. `LIMIT`子句

在`PostgreSQL`和`SQLite`中，用来限制输出结果，例子中就只返回不超过5行的数据

##### `OFFSET`

可以指定从某处起的检索，比如`OFFSET 5`就是从第5行起（6-10行）数据，注意检索是从第0行开始的，如果想要从第一行开始检索应当使用`OFFSET 0`而非`OFFSET 1`，后者是从第2行起

在`MySQL	`中，可以使用简化的`LIMIT`子句，如`LIMIT 3,4`，其相当于`LIMIT 4 OFFSET 3`

```SQL
SELECT column_name FROM dataset LIMIT 5
SELECT column_name FROM dataset LIMIT 5 OFFSET 5
```

#### 3. `ORDER BY`子句

`ORDER BY`子句一定需要是SELECT语句中的最后一条子句，可以将选中列按排序列的首字母顺序排列，一般选中列和排序列是相同的，及将选中列按首字母排序，但完全可以使用另外一个未被检索的列作为排序依据

```sql
SELECT prod_name FROM Products ORDER BY prod_name
SELECT prod_id, prod_price, prod_name FROM Products ORDER BY prod_price, prod_name
```

同时可以看到，可以按多个列排序，排序的顺序是从前到后的，比如同时按`prod_price`和`prod_name`排序，只有在有多个相同的`prod_price`的情况下，这些相同行的内部才会按照`prod_name`排序，具体可以参照如下示例输出：

```sql
prod_id prod_price prod_name
------- ---------- --------------------
BNBG02  3.4900     Bird bean bag toy
BNBG01  3.4900 	   Fish bean bag toy
BNBG03  3.4900     Rabbit bean bag toy
RGAN01  4.9900     Raggedy Ann
BR01    5.9900     8 inch teddy bear
BR02    8.9900     12 inch teddy bear
RYL01   9.4900     King doll
RYL02   9.4900     Queen doll
BR03    11.9900    18 inch teddy bear
```

##### `DESC`关键字

```sql
SELECT prod_id, prod_price, prod_name FROM Products ORDER BY prod_price DESC
SELECT prod_id, prod_price, prod_name FROM Products ORDER BY prod_price DESC, prod_name
SELECT prod_id, prod_price, prod_name FROM Products ORDER BY prod_price DESC, prod_name DESC
```

`ORDER BY`的默认排序方向是升序，需要使用关键字`DESC`置顶排序方向为降序，且该关键字只作用于**直接**位于他前方的列名，比如代码中`prod_price`是降序排列，而`prod_name`就是升序排列，如果想要所有的降序排列，需要对每一个列名都使用关键字

升序也存在对应关键字`ASC`，但是该关键字几乎没有意义，因为默认的排序方向就是升序

##### TIPS

*在对文本性数据进行排序时，A 与 a 相同吗？a 位于 B 之前，还是 Z 之后？*

这些问题不是理论问题，其答案取决于数据库的设置方式。

在字典（dictionary）排序顺序中，A 被视为与 a 相同，这是大多数数据库管理系统的默认行为。但是，许多 DBMS 允许数据库管理员在需要时改变这种行为（如果你的数据库包含大量外语字符，可能必须这样做

这里的关键问题是，如果确实需要改变这种排序顺序，用简单的 `ORDER BY` 子句可能做不到。你必须请求数据库管理员的帮助

#### 4. `WHERE`子句

按照指定条件筛选行

