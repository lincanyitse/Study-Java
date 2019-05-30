# 序列、约束、视图、索引

## oracle 序列

---

+ 概述
    > 用来生成唯一数字值的数据库对象, 序列的值由Oracle程序按递增或递减顺序自动生成, 通常用来自动产生表的主键值

+ 创建：

    ```SQL
    create sequence 序列名
    [ start with 序列初值 ]
    [ increment by 递增值|递减值 ]
    [ maxvalue 最大值 | nomaxvalue ]
    [ minvalue 最小值 | nominvalue ]
    [ cycle | nocycle ] -- 表示在递增至最大值或递减至最小值之后是否继续循环
    [ cache 缓存数 | nocache ] -- 默认是20
    ```

+ 使用：

    ```SQL
    CREATE TABLE person_xxx(
    ID NUMBER,
    NAME VARCHAR2(60)
    );
    INSERT INTO person_xxx VALUES(seq_xxx.NEXTVAL,'张三');
    --查询刚刚生成的记录, id值将是1000：
    SELECT ID,NAME FROM person_xxx;
    --此时查询序列的当前值, 会得到1000的数字。
    SELECT seq_xxx.CURRVAL FROM dual;
    ```

    > 序列中有两个伪列：
    > + `序列名.nextval` 获取序列的下一个值;
    > + `序列名.currval` 获取序列的当前值;
    > 注：当序列创建以后, 必须先执行一次`nextval`, 之后才能使用`currval`;

---

## oracle 约束

---

+ 概述
    > 用于确保数据库数据满足特定的商业逻辑或者企业规则, 如果定义了约束, 并且数据不符合校验规则, 那么DML操作（INSERT、UPDATE、DELETE）将不能成功执行, 约束有五种:非空约束(`NOT NULL`)、唯一约束(`UNIQUE`)、主键约束(`PRIMARY KEY`)、外键约束(`FOREINGKEY`) 以及检查约束(`CHECK`)

+ 类型
  + 非空约束
        > 用于确保字段值不为空

  + 唯一约束
        > 用于保证字段或者字段的组合不出现重复值

  + 主键约束
        > + 从功能上看相当于非空（NOTNULL）且唯一（UNIQUE）的组合;
        > + 可以用来在表中唯一的确定一行数据;
        > + 既可以在列级定义, 也可以在表级定义

  + 外键约束
        > 外键约束条件定义在两个表的字段或一个表的两个字段上, 用于保证相关两个字段的关系;
        > 外键约束对一致性的保护
        > + 从表上定义的外键的列值, 必须从主表被参照的列值中选取, 或者为 NULL ;
        > + 当主表参照列的值被从表参照时, 主表的该行记录不允许被删除;

  + 检查约束
        > 用来强制在字段上的每个值都要满足Check中定义的条件

+ 操作

  + 建表时添加约束

    + `字段声明 [CONSTRAINT 约束名] 约束类型,` 列级约束：是与列的定义一起定义的

        ```SQL
        CREATE TABLE student_xxx(
        ID NUMBER PRIMARY KEY, -- 列级主键约束
        NAME VARCHAR2(50) CONSTRAINT student_name_un NOT NULL, -- 非空约束
        gender char(1) check(gender in ('F','M')), -- 列级检查约束
        phone VARCHAR2(18) CONSTRAINT student_phone_un UNIQUE, -- 唯一约束
        );
        ```

    + `[CONSTRAINT 约束名] 约束类型 (已声明的字段名,...)` 表级约束：是在列定义之后定义

            ```SQL
            create table class_xxx(
            ID NUMBER(2) PRIMARY KEY,
            NAME VARCHAR2(20)
            );

            CREATE TABLE student_xxx(
            ID NUMBER,
            NAME VARCHAR2(50),
            gender char(1),
            phone VARCHAR2(18),
            cid NUMBER(2),
            CONSTRAINT student_id_un primary key(id), -- 表级主键约束
            CONSTRAINT student_gender_un CHECK(gender IN('F', 'M') ) -- 表级检查约束
            constraint student_cls_un foreign key(cid) references class_xxx (id) on delete set null -- 外键
            );
            ```

  + 建表后添加约束

    + `alter table 表名 add [ constraint 约束名 ] 约束类型 (已声明的字段名,...)` 添加表级约束

    + `alter table 表名 modify (字段声明 [CONSTRAINT 约束名] 约束类型)` 给单个字段添加约束

  + 删除约束

    + `alter table 表名 drop constraint 约束名`

---

## 视图

---

+ 概述
    > 视图(`VIEW`)被称为虚表, 是一个虚拟的表, 并不是真实存在的;
    > 视图是映射到数据库表的查询语句, 当数据库表发生变化时, 视图数据也随着发生变化;

+ 类型
    > 根据视图所对应的子查询种类分为几种类型:
    >   + SELECT语句是基于单表建立的, 且不包含任何函数运算、表达式或分组函数, 叫做`简单视图`, 此时视图是基表的子集；
    >   + SELECT语句同样是基于单表, 但包含了单行函数、表达式、分组函数或GROUP BY子句, 叫做`复杂视图`；
    >   + SELECT语句是基于多个表的, 叫做`连接视图`。

+ 操作

  + 创建视图

        ```SQL
            CREATE [OR REPLACE] [{FORCE|NOFORCE}] VIEW 视图名[(列1 别名[, 列2 别名,…])]
            AS select_statement
            [WITH {READ ONLY|CHECK OPTION}];
        ```
        > 语法解析：
        > + `OR REPLACE`：如果视图已经存在, 则替换旧视图;
        > + `FORCE`：即使基表不存在, 也可以创建该视图, 但是该视图不能正常使用, 当基表创建成功后, 视图才能正常使用;
        > + `NOFORCE`：如果基表不存在, 无法创建视图, 该项是默认选项;
        > + `select_statement`：是 SELECT 查询语句, 对应的表被称作基表;
        > + `WITH READ ONLY`：默认可以通过视图对基表执行增删改操作, 但是有很多在基表上的限制(比如：基表中某列不能为空, 但是该列没有出现在视图中, 则不能通过视图执行insert操作), `WITH READ ONLY`说明视图是只读视图, 不能通过该视图进行增删改操作。现实开发中, 基本上不通过视图对表中的数据进行增删改操作;
        > + `WITH CHECK OPTION`：短语表示, 通过视图所做的修改, 必须在视图的可见权限范围内:
        >     1. 假设进行 INSERT 操作后, 新增的记录在视图中可查看到
        >     2. 假设 UPDATE 操作后, 修改后的结果必须能通过视图查看到
        >     3. 假设进行 DELETE 操作, 只能删除现有视图里能查到的记录
        >
        > 注：创建视图的DDL语句是 CREATE VIEW , 用户必须有创建视图的系统权限, 才能创建视图;数据库管理员可以通过DCL语句授予用户创建视图的权限, 例：
        >   ```SQL
        >   GRANT CREATE VIEW TO oracle; -- 授权oracle创建视图的权限
        >   ```
        > 解析：oracle是用户名

  + 查询视图

    + 查询简单视图
        > 查询视图和查询表的操作相同
        >
        >   ```SQL
        >   SELECT * FROM 视图名;
        >   ```
        >
        > 注：创建视图时可以指定列名, 此时视图的列名, 和创建时指定的列名一致, 不一定是基表的原列名;

    + 查询复杂视图
        > 复杂视图指在子查询中包含了表达式、单行函数或分组函数的视图;
        > 复杂视图不能进行增删改操作, 例：
        >
        > ```SQL
        > SELECT * FROM 视图名;
        > ```
        >
        > 注意：复杂视图不允许DML操作, 会报错;

  + 通过数据字典查询视图信息
    > 要查询视图的相关信息比如数据库有哪些视图等, 需要用到oracle数据字典;
    >
    > 与视图相关的数据字典有：
    > + `USER_OBJECTS` 例：
    >
    > ```SQL
    > SELECT object_name FROM user_objects WHERE object_type = 'VIEW';
    > ```
    >
    > + `USER_VIEWS` 例：
    >
    > ```SQL
    > SELECT text FROM user_views WHERE view_name = 'V_EMP_LZH';
    > ```
    >
    > + `USER_UPDATABLE_COLUMNS` 例：
    >
    > ```SQL
    > SELECT column_name, insertable, updatable, deletable FROM user_updatable_columns
    > WHERE table_name = 'V_EMP_LZH';
    > ```

  + 删除视图
        > 当不再需要视图的定义, 可以使用DROP VIEW语句删除视图, 语法如下：
    + `DROP VIEW 视图名;`

---

## 索引

---

+ 概述
    > 索引是一种允许直接访问数据表中某一数据行的树型结构, 为了提高查询效率而引入, 是独立于表的对象, 可以存放在与表不同的表空间（TABLESPACE）中, 索引记录中存有索引关键字和指向表中数据的指针（地址）;
    >
    > 索引一旦被建立就将被Oracle系统自动维护, 查询语句中不用指定使用哪个索引, 是一种提高查询效率的机制索引的结构是以数据+地址( 如：凹凸曼+xx路xx号xx楼xx房)的方式的, 而地址是唯一的, 通过查找地址可以找到记录, 从而达到提高查询效率(java中有类似的HashMap结构);

+ 操作

  + 创建索引

    ```SQL
    CREATE [UNIQUE] INDEX index_name ON table(column[, column…]);
    ```

    >语法解析：
    > + `index_name` 表示索引名称
    > + `table` 表示表名
    > + `column` 表示建立索引列名, 可以建立单列索引或复合索引
    > + `UNIQUE` 表示唯一索引,当某列任意两行的值都不相同的时候可以建立, 而当建立 Primary Key( 主键)或者
    > + `Unique constraint` (唯一约束)时, 唯一索引将被自动建立

  + 重建索引

    ```SQL
    ALTER INDEX index_name REBUILD;
    ```

  + 删除索引

    ```SQL
    DROP INDEX index_name;
    ```
  
    > 为提升查询效率, 创建和使用索引的原则：
    > + 为经常出现在WHERE子句中的列创建索引
    > + 为经常出现在ORDER BY、DISTINCT后面的字段建立索引。
    > + 如果建立的是复合索引, 索引的字段顺序要和这些关键字后面的字段顺序一致
    > + 为经常作为表的连接条件的列上创建索引
    > + 不要在经常做DML操作的表上建立索引
    > + 一般来说, 不需要为比较小的表创建索引,限制表上的索引数目, 索引并不是越多越好
    > + 删除很少被使用的、不合理的索引
