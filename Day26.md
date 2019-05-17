<h1 id="topbar">Oracle的基本操作</h1>

## Oracle命令行

### Oracle连接登录操作

> #### 命令行连接登录：
>
> ```cmd
> sqlplus 用户名/密码@地址:端口(1521)/数据库名(orcl)
> ```

### Oracle命令行用户操作

> #### 创建用户：
>
> ```SQL
> create user 用户名 identified by 密码;
> ```
>
> #### 修改用户密码：
>
> ```SQL
> alter user 用户名 identified by 新密码;
> ```
>
> #### 解锁用户：
>
> ```SQL
> alter user 用户名 account unlock;
> ```
>
> #### 权限：
>
> + 授予角色权限：
>
> ```SQL
> grant 权限 to 用户;
> ```
>
> + 授予权限：
>
> ```SQL
> grant create session to 用户名;
> ```
>
> + 收回权限
>
> ```SQL
> revoke 角色|权限 from 用户名;
> ```
>
> #### 删除用户
>
> ```SQL
> drop user 用户名[cascade];
> ```
>
> #### 查询用户名
>
> + 查询数据库所有用户
>
> ```SQL
> select * from dba_users; 
> ```
>
> + 查询当前能管理的所有用户
>
> ```SQL
> select * from all_users; 
> ```
>
> + 查询当前用户信息
>
> ```SQL
> select * from user_users;
> 
> ```
>
> + 显示当前用户
>
> ```SQL
> show user; 
> ```
>
> #### 切换用户：
>
> ```SQL
> connect 用户名/密码；
> ```
>
> #### 用户权限角色：
>
> + session(登录权限)
> + table(创建表权限)
> + index(创建索引权限)
> + view(创建视图权限)
> + sequence(创建序列权限)
> + trriger(创建触发器权限)
> + connect(连接数据库权限)
> + resource(取消空间限制)
> + ......

### 命令行表操作

> #### 查询当前用户下所有表：
>
> ```SQL
> select * from user_tables;
> ```
>
> #### 创建表：
>
> ```SQL
> create table 表名(字段1 数据类型 [not null] [primary key ], 字段2 数据类型 [not null], ...)
> ```
>
> #### 删除表：
>
> + 清空表数据
>
> ```SQL
> delete table 表名;
> // 或者
> truncate table 表名;
> ``` 
>
> + 立即删除表结构
>
> ```SQL
> drop table 表名 purge ;  
> ```
>
> + 把表结构放进回收站
>
> ```SQL
> drop table 表名;
> ```
>
> #### 修改表：
>
> + 重命名：
>
> ```SQL
> rename 旧表名 to 新表名;
> ```
>
> + 增加列：
>
> ```SQL
> alter table 表名 add (列名 数据类型 [default 表达式] [, 列名 数据类型…])
> ```
>
> + 删除列：
>
> ```SQL
> alter table 表名 drop (列名);
> ```
>
> + 修改列：
>
> ```SQL
> alter table 表名 modify(列名 数据类型 [default 表达式][, 列名 数据类型…])
> ```
>
> #### 查看表结构
>
> ```SQL
> desc 表名;
> ```
>
> #### 表回收站
>
> + 清空回收站
>
> ```SQL
> purge recyclebin; 
> ```
>
> + 删除回收站某个表
>
> ```SQL
> purge table "表名";
> ```
>

### 命令行数据操作

> #### 添加数据
>
> ```SQL
> insert into 表名[(列名1[, 列名2, ...])]values(值1[, 值2, ...]);
> ```
>
> #### 修改数据
>
> ```SQL
> update 表名 set 列名1=列值1[, 列名2=列值2,...][where 条件];
> ```
>
> #### 删除数据
>
> ```SQL
> delete [from] 表名 [where 条件];
> ```
>
> #### 查询数据
>
> ```SQL
> select 字段名1 [别名1][, 字段名2 [别名2], ...] from 表名 [where 条件];
> ```

###  设置
---
<span style="float:left;display:inline-block;">[上一章](Day25.md)</span>
<span style="margin-left:43%">[目录](SUMMARY.md)</span>
<span style="float:right;">[下一章](Day27.md)</span>
