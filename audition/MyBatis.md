# MyBatis 面试题

## 1.MyBatis 的了解

> Mybatis 是一个半 ORM（对象关系映射）框架，它内部封装了 JDBC，开发时只需要关注 SQL 语句 本身，不需要花费精力去处理加载驱动、创建连接、创建 statement 等繁杂的过程;程序员直接编写原生 态 sql，可以严格控制 sql 执行性能，灵活度高;MyBatis 可以使用 XML 或注解来配置和映射原生信息，将 POJO 映射成数据库中的记录，避免了 几乎所有的  JDBC 代码和手动设置参数以及获取结果集;通过 xml 文件或注解的方式将要执行的各种 statement 配置起来，并通过 java 对象和 statement 中 sql 的动态参数进行映射生成最终执行的 sql 语句，最后由 mybatis 框架执行 sql 并将结果映射为 java 对象并返回;（从执行 sql 到返回 result 的过程）

## 2.MyBatis 的优缺点

+ 优点
  
  1. 基于 SQL 语句编程，相当灵活，不会对应用程序或者数据库的现有设计造成任何影响，SQL 写在 XML 里，解除 sql 与程序代码的耦合，便于统一管理;提供 XML 标签，支持编写动态 SQL 语句，并可重用;

  2. 与 JDBC 相比，减少了 50%以上的代码量，消除了 JDBC 大量冗余的代码，不需要手动开关连接;

  3. 很好的与各种数据库兼容（因为 MyBatis 使用 JDBC 来连接数据库，所以只要 JDBC 支持的数据库 MyBatis 都支持）;

  4. 能够与 Spring 很好的集成;

  5. 提供映射标签，支持对象与数据库的 ORM 字段关系映射;提供对象关系映射标签，支持对象关系组 件维护

+ 缺点
  
  1. SQL 语句的编写工作量较大，尤其当字段多、关联表多时，对开发人员编写 SQL 语句的功底有一定 要求;
  2. SQL 语句依赖于数据库，导致数据库移植性差，不能随意更换数据库;

## 3.MyBatis 与 Hibernate 的区别

1. Mybatis 和 hibernate 不同，它不完全是一个 ORM 框架，因为 MyBatis 需要程序员自己编写 Sql 语句;

2. Mybatis 直接编写原生态 sql，可以严格控制 sql 执行性能，灵活度高，非常适合对关系数据模型要 求不高的软件开发，因为这类软件需求变化频繁，一但需求变化要求迅速输出成果;但是灵活的前提是 mybatis 无法做到数据库无关性，如果需要实现支持多种数据库的软件，则需要自定义多套 sql 映射文件， 工作量大;

3. Hibernate 对象/关系映射能力强，数据库无关性好，对于关系模型要求高的软件，如果用 hibernate 开发可以节省很多代码，提高效率