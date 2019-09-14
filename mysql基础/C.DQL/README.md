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
> < 、> 、<= 、>= 、= 、<>  
> BETWEEN...AND  
> IN( 集合)   
> LIKE：模糊查询   
> IS NULL  
> and  或 &&
> or  或 || 
> not  或 !  
> 占位符：  
>> _: 单个任意字符  
>> %：多个任意字符     

+ 案例
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