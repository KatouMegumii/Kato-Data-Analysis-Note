### 基础知识
SQL是不区分大小写的，但是对关键字（泛指，具体包括语句 子句和关键字）一般约定俗成使用大写

SQL中的空格是会被忽略的

SQL没有严格的语法规定，一条SQL命令可以分多行写也可以在一行写完，单条的命令在大部分数据库上都可以不使用分号`;`分隔，但是如果是多行命令，则必须对每条命令使用分号分隔

```SQL
/* 这三种写法是完全一样的 */
SELECT prod_name
FROM Products;

SELECT prod_name FROM Products; 

SELECT
prod_name
FROM
Products; 
```

SQL中写注释的方式很多
```SQL
# 这是一条注释（虽然不知道为什么markdown不识别）
-- 可以内嵌在语句内的注释
/* 类似于括号，需要头尾框起来成为注释 */
```


### 一些中英对照
**database** 数据库 

**table** 表 

**column** 列 

**row** 行

**primary key** 主键（例如ID，用来识别行的列）

**statement** 语句

**clause** 子句

**keyword** 关键字