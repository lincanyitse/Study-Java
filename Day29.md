# <h1>子查询、分页查询、集合操作、事务</h1>

## 子查询
---
  > 为了给查询提供数据而首先执行的查询语句叫做子查询,`子查询：嵌入在其它SQL语句中的SELECT语句, 大部分时候出现在WHERE子句中`, 子查询嵌入的语句称作`主查询`或`父查询`, 主查询可以是SELECT语句, 也可以是其它类型的语句比如DML或DDL语句;
### WHERE子句中的子查询
  > 根据返回结果的不同, 子查询可分为单行子查询、多行子查询及多行多列子查询:
  + 单行子查询：子查询结果为单行结果;
    ```SQL
    -- 查询Tom的班级编号
    select classno from student where sname='Tom';
    -- 查询Tom的同班同学
    select * from student where classno=(select classno from student where sname='Tom');
    ```
    > 注：单行子查询仅能使用 ` = > < >= <= <> != ` 进行比较;
  + 多行子查询：子查询结果为一个列;
    > 如果子查询返回多行, 主查询中要使用多行比较操作符, 包括IN、ALL、ANY等, 例：
    ```SQL
    -- 查询员工编号是别人的领导编号
    SELECT ename FROM employee_lzh WHERE empno IN ( SELECT DISTINCT mgr FROM employee_lzh) ;
    ```
  + 多行多列子查询：子查询结果为多行多列;
    > 多行多列使用的是：
    > + `exists` 判断子查询有没有数据返回 , 有则为 ture , 没有则为 false , 并且 exists 不关心子查询的结果 , 所以子查询中 select 后面写什么都可以, 推荐使用常量 1 ;

### HAVING子句中的子查询
  > 在`Having`子句中的子查询, 一般作用是过滤分组后的数据, 例：  
  ```SQL
  -- 1.查出30部门的最低薪水
  SELECT MIN(sal) FROM emp WHERE deptno = 30;
  -- 2.查出每个部门的最低薪水(先过滤掉没有部门的, 再按部门分组))
  SELECT deptno, MIN(sal) min_sal FROM emp WHERE deptno IS NOT NULL GROUP BY   deptno;
  -- 3.过滤, 找出比30部门高的
  SELECT deptno, MIN(sal) min_sal FROM emp WHERE deptno IS NOT NULL GROUP BY   deptno HAVING MIN(sal) > (SELECT MIN(sal) FROM emp WHERE deptno=30);
  ```

### FROM子句中的子查询
  > 在查询语句中, FROM子句用来指定要查询的表, 如果要在一个子查询的结果中继续查询, 则子查询出现在 FROM 子句中, 这个子查询可以理解为临时表, 只能在当前的SQL语句中有效;
  ```SQL
  --1.查询出每个部门的平均薪水 按部门分组求出平均薪水
  SELECT deptno, AVG(sal) avg_sal FROM emp GROUP BY deptno;
  --2.比较本部门的平均薪水
  SELECT e.deptno, e.ename, e.sal
  FROM emp e,
  (SELECT deptno, AVG(sal) avg_sal FROM emp GROUP BY deptno) a
  WHERE e.deptno = a.deptno
  and e.sal < a.avg_sal
  ORDER BY e.deptno;
  ```
### SELECT子句中的子查询
  > 把子查询放在SELECT子句部分, 可以认为是连接的另一种表现形式, 使用更灵活;
  ```SQL
  SELECT e.ename, e.sal, e.deptno,
  (SELECT d.deptno FROM dept d WHERE d.deptno = e.deptno) deptno
  FROM emp e;
  ```

---
## 分页查询
---

+ `Rownum` 被称作伪列, 是对结果集加序列号
  ```SQL
  SELECT ROWNUM, empno, ename, sal FROM emp;
  ```
  > 注：先要有结果集, 并且总是从1开始排起的, 不能从结果集中直接截取, 如果要用rownum进行截取的话, 需要先将ROWNUM查出作为临时表的一个列, 在主查询中就可以使用这个列值作为条件
+ 使用`Rownum`进行分页
  > 在ORACLE中利用`Rownum`的功能来进行分页
  ```SQL
  SELECT * FROM
  (SELECT ROWNUM rn , e.* FROM emp e )
  WHERE rn BETWEEN 5 AND 10;
  ```
  > 注：不能查询出分页后排序, 应该是在该分页的5条数据中排序, 例：
  > ```SQL
  > --- 查询 5 - 10 条记录
  > SELECT * FROM
  > (SELECT ROWNUM rn , t.* FROM
  > (SELECT empno,ename,sal FROM emp ORDER BY sal DESC) t)
  > WHERE rn BETWEEN 5 AND 10;
  > ```

---
## 判断查询
---

+ `decode(判断条件 , 匹配1 , 值1 , 匹配2 , 值2 , … , 默认值)` 函数是 Oracle 中类似java的 switch case 语句的函数,用于进行逻辑判断;
  ```SQL
  --- 查询职员表, 根据部门加薪, 计算加薪后金额
  select ename,deptno,
  decode(
    deptno,
    10,sal*1.1,
    20,sal*1.2,
    30,sal*1.05,
    sal
    ) new_sal 
  from emp order by deptno;
  ```

+ `case 判断条件 when 匹配1 then 值1 when 匹配2 then 值2...else 默认值 end` oracle还提供了和DECODE函数功能相似的CASE语句, 实现类似于if-else的操作;
  ```SQL
  --- 查询职员表, 根据部门加薪, 计算加薪后金额
  SELECT ename, sal,deptno,
  CASE deptno 
  WHEN 10 THEN sal * 1.1
  WHEN 20 THEN sal * 1.2
  WHEN 30 THEN sal * 1.05
  ELSE sal END
  bonus
  FROM emp order by deptno;
  ```
+ decode 运用于分组查询
  + decode 函数可以按字段内容分组, 例：
    ```SQL
    -- 计算职位的人数,  analyst/manager 职位属于 HIGH _ MANA , 其余是普通员工 OPERATION
    SELECT DECODE(JOB, 'ANALYST', 'HIGH_MANA','MANAGER', 'HIGH_MANA','OPERATION') JOB, 
    COUNT(*) job_cnt
    FROM emp
    GROUP BY DECODE(job, 'ANALYST', 'HIGH_MANA', 'MANAGER', 'HIGH_MANA', 'OPERATION');
    ```
  + decode 函数也可以按字段内容排序, 例：
    ```SQL
    -- Dept表中按 ”RESEARCH” 、 “SALES” 、 “OPERATIONS” 顺序排序
    SELECT deptno, dname, loc
    FROM dept
    ORDER BY DECODE(dname, 'RESEARCH',1,'SALES',2,'OPERATIONS',3), loc;
    ```

---
## 排序查询
---

+ `Row_number() OVER(PARTITION BY 分组条件 ORDER BY 组内排序条件)` 该函数计算的值就是每组内部排序后的顺序编号, 组内连续且唯一, 例：
  ```SQL
  -- 查询员工表, 按照部门号分组显示, 每组内按员工号排序, 并赋予组内编号
  SELECT deptno, ename, empno, ROW_NUMBER() OVER (PARTITION BY deptno ORDER BY empno) AS emp_id FROM emp;
  ```
  > 注：`ROWNUM` 是伪列,  `ROW_NUMBER` 功能更强, 可以直接从结果集中取出子集进行处理

+ `Rank() over(PARTITION BY 分组条件 ORDER BY 组内排序条件)` 该函数特点是跳跃排序, 如果有相同数据, 则排名相同, 比如并列第二, 则两行数据都标记为2, 但下一位将是第四名, 例：
  ```SQL
  -- 查询员工表, 按照部门号分组, 同组内按薪水倒序排序, 相同薪水则按奖金数顺序排序, 并给予组内排序编号, 用Pay_ID表示
  SELECT deptno, ename, sal, comm,
  RANK() OVER (PARTITION BY deptno ORDER BY sal DESC, comm) "Pay_ID" --区分大小写要用""
  FROM emp;
  ```
  > 注：`RANK` 与 `ROW_NUMBER` 的区别是有结果有重复值, 而 `ROW_NUMBER` 没有

+ `DENSE_RANK() OVER(PARTITION BY 分组条件 ORDER BY 组内排序条件)` 该函数特点是连续排序, 如果有并列第二, 下一个排序将是三, 这一点是与 RANK 的区别,  RANK 是跳跃排序, 例：
  ```SQL
  -- 关联员工表和部门表, 按照部门号分组, 每组内按照员工薪水排序, 列出员工的部门名字、姓名和薪水
  SELECT d.dname, e.ename, e.sal,
  DENSE_RANK() OVER (PARTITION BY e.deptno ORDER BY e.sal) drank
  FROM emp e join dept d
  on e.deptno = d.deptno;
  ```

---
## 集合操作
---
> 为了合并多个SELECT语句的结果, 可以使用集合操作符, 实现集合的并、交、差
+ 集合操作符
  > 语法格式：
  > ```SQL
  > SELECT 集合1
  > [union | union all | intersect | minus]
  > SELECT 集合2;
  > ```
  + `union` 操作符会自动去掉合并后的重复记录,并对查询结果第一列升序排序,例：
    ```SQL
    SELECT empno,ename,hiredate,sal FROM emp WHERE hiredate > to_date('1985-1-1','yyyy-mm-dd')
    UNION
    SELECT empno,ename,hiredate,sal FROM emp WHERE sal > 2900;
    ```
  + `union all` 返回两个结果集中的所有行, 包括重复的行, 并且对查询结果不排序, 例：
    ```SQL
    SELECT empno,ename,hiredate,sal FROM emp WHERE hiredate > to_date('1985-1-1','yyyy-mm-dd')
    UNION ALL
    SELECT empno,ename,hiredate,sal FROM emp WHERE sal > 2900;
    ```
  + `intersect` 函数获得两个结果集的交集, 只有同时存在于两个结果集中的数据, 才被显示输出,并且结果集会以第一列的数据作升序排列, 例：
    ```SQL
    SELECT ename, deptno, sal FROM emp WHERE deptno = 20
    INTERSECT
    SELECT ename, deptno, sal FROM emp WHERE sal > 2500;
    ```
  + `minus` 函数获取两个结果集的差集, 例：
    ```SQL
    SELECT ename, deptno, sal FROM emp WHERE deptno = 20
    MINUS
    SELECT ename, deptno, sal FROM emp WHERE sal >= 2500;
    ```
  > 注：当列的个数、列的顺序、列的数据类型一致时 , 我们称这两个结果集结构相同, 只有结构相同的结果集才能做集合操作

---
## 事务
---

> 事务是一组 增删查改 操作的逻辑单元 , 用来保证数据的一致性 , 事务控制语言 TCL( Transaction Control Language )包括下面的语句
  + `commit` 事务提交 将所有的数据改变提交
  + `rollback` 事务回滚 回退到事务之初 , 数据的状态和事务开始之前完全一致
  + `savepoint` 事务保存点( 较少常用 ), 例：
    ```SQL
    INSERT INTO A VALUES(3) ;
    savepoint FIRST ; -- 设置保存点 , 名为 FIRST
    INSERT INTO A VALUES(4) ;
    savepoint TWO; -- 设置保存点 , 名为 TWO
    insert into A values(5) ;
    ROLLBACK TO FIRST ;
    -- 回滚到保存点 FIRST , 注意： FIRST 之后的保存点全部被取消
    SELECT * FROM A ; --3 被插入数据库 , 4、 5 没有被插入
    ```

### 事务的开始与结束
 + `事务开始` 事务开始于上一个事务的终止或者第一条 DML 语句
 + `事务终止` 事务终止于 commit/rollback 显式操作( 即输入 commit/rollback 命令)
>
> 注：如果连接关闭 , 事务( Transaction )将隐式提交 DDL 操作( 比如 create ) , 事务将隐式提交如果出现异常 , 事务将隐式回滚

### 事务与数据
> 1. 事务会对操作的数据加锁 , 不允许其它事务操作(类似java的同步锁), 如果提交( commit )后 , 数据的改变被确认 , 则所有的连接都能看到被改变的结果 ;
> 2. 数据上的锁被释放 ;
> 3. 保存数据的临时空间被释放
> 4. 如果回滚( rollback ) , 则数据的改变被取消 ;
> 5. 数据上的锁被释放 ;
> 6. 临时空间被释放

---
<span style="float:left;display:inline-block;">[上一章](Day28.md)</span>
<span style="margin-left:43%">[目录](SUMMARY.md)</span>
<span style="float:right;">[下一章](Day30.md)</span>