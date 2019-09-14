# DQL：查询表中的记录
---
1. 基本用法展示表中的内容
```sql
select * from NameOfTable;--查看一个表中的所有数据
```

2. 语法总结
```sql
select 字段列表    from         表名列表
                  where        条件列表
                  group by     分组字段
                  having       分组之后的条件
                  order by     排序
                  limit        分页限定
```

3. 基础查询
```sql
--多个字段的查询。注意：如果查询所有字段，则可以使用*来替代字段列表。
select 字段名1，字段名2... from 表名；
    

--去除重复：
distinct
    

--计算列
--一般可以使用四则运算计算一些列的值。（一般只会进行数值型的计算）
--ifnull(表达式1,表达式2)：null参与的运算，计算结果都为null
--表达式1：哪个字段需要判断是否为null。如果该字段为null后的替换值。
    
    
--起别名,as也可以省略
as
```        

4. 条件查询(where子句后跟条件)
```
    < 、> 、<= 、>= 、= 、<>  
    BETWEEN...AND  
    IN( 集合)   
    LIKE：模糊查询   
    IS NULL  
    and  或 &&
    or  或 || 
    not  或 !  
    占位符：  
        _: 单个任意字符  
        %：多个任意字符     
```
```sql
-- 查询年龄大于20岁

SELECT * FROM student WHERE age > 20;

SELECT * FROM student WHERE age >= 20;

-- 查询年龄等于20岁
SELECT * FROM student WHERE age = 20;

-- 查询年龄不等于20岁
SELECT * FROM student WHERE age != 20;
SELECT * FROM student WHERE age <> 20;

-- 查询年龄大于等于20 小于等于30

SELECT * FROM student WHERE age >= 20 &&  age <=30;
SELECT * FROM student WHERE age >= 20 AND  age <=30;
SELECT * FROM student WHERE age BETWEEN 20 AND 30;

-- 查询年龄22岁，18岁，25岁的信息
SELECT * FROM student WHERE age = 22 OR age = 18 OR age = 25
SELECT * FROM student WHERE age IN (22,18,25);

-- 查询英语成绩为null
SELECT * FROM student WHERE english = NULL; -- 不对的。null值不能使用 = （!=） 判断

SELECT * FROM student WHERE english IS NULL;

-- 查询英语成绩不为null
SELECT * FROM student WHERE english  IS NOT NULL;



-- 查询姓马的有哪些？ like
SELECT * FROM student WHERE NAME LIKE '马%';
-- 查询姓名第二个字是化的人

SELECT * FROM student WHERE NAME LIKE "_化%";

-- 查询姓名是3个字的人
SELECT * FROM student WHERE NAME LIKE '___';


-- 查询姓名中包含德的人
SELECT * FROM student WHERE NAME LIKE '%德%';
```

5. 排序查询
```
* 语法：order by 子句
* order by 排序字段1 排序方式1 ，  排序字段2 排序方式2...

* 排序方式：
* ASC：升序，默认的。
* DESC：降序。

* 注意：
* 如果有多个排序条件，则当前边的条件值一样时，才会判断第二条件。
```

6. 聚合函数：将一列数据作为一个整体，进行纵向的计算。
```
    1. count：计算个数
    1. 一般选择非空的列：主键
    2. count(*)
    2. max：计算最大值
    3. min：计算最小值
    4. sum：计算和
    5. avg：计算平均值
```
    注意：聚合函数的计算，排除null值。
    解决方案：
        1. 选择不包含非空的列进行计算
        2. IFNULL函数

7. 分组查询:
```
    1. 语法：group by 分组字段；
    2. 注意：
        1. 分组之后查询的字段：分组字段、聚合函数
        2. where 和 having 的区别？
            1. where 在分组之前进行限定，如果不满足条件，则不参与分组。having在分组之后进行限定，如果不满足结果，则不会被查询出来
            2. where 后不可以跟聚合函数，having可以进行聚合函数的判断。
```
```sql
-- 按照性别分组。分别查询男、女同学的平均分
SELECT sex , AVG(math) FROM student GROUP BY sex;

-- 按照性别分组。分别查询男、女同学的平均分,人数
SELECT sex , AVG(math),COUNT(id) FROM student GROUP BY sex;

--  按照性别分组。分别查询男、女同学的平均分,人数 要求：分数低于70分的人，不参与分组
SELECT sex , AVG(math),COUNT(id) FROM student WHERE math > 70 GROUP BY sex;

--  按照性别分组。分别查询男、女同学的平均分,人数 要求：分数低于70分的人，不参与分组,分组之后。人数要大于2个人
SELECT sex , AVG(math),COUNT(id) FROM student WHERE math > 70 GROUP BY sex HAVING COUNT(id) > 2;

SELECT sex , AVG(math),COUNT(id) 人数 FROM student WHERE math > 70 GROUP BY sex HAVING 人数 > 2;

```

8. 分页查询
```
    1. 语法：limit 开始的索引,每页查询的条数;
    2. 公式：开始的索引 = （当前的页码 - 1） * 每页显示的条数  
    3. limit 是一个MySQL"方言"
```
```sql
-- 每页显示3条记录 

SELECT * FROM student LIMIT 0,3; -- 第1页

SELECT * FROM student LIMIT 3,3; -- 第2页

SELECT * FROM student LIMIT 6,3; -- 第3页
```    