# Shiro 面试题

## 1.Shiro 的了解

> Apache Shiro 是 Java 的一个安全框架; 使用 shiro 可以非常容易的开发出足够好的应用，其不仅可以用在 JavaSE 环境，也可以用在 JavaEE 环境; Shiro 可以帮助我们完成：认证、授权、加密、会话管理、与Web集成、缓存等;

三个核心组件

+ Subject
  > 即“当前操作用户”; 但是，在 Shiro 中，Subject 这一概念并不仅仅指人，也可以是第三方进程、后台帐户（Daemon Account）或其他类似事物; 它仅仅意味着“当前跟软件交互的东西”; 但考虑到大多数目的和用途，你可以把它认为是 Shiro 的“用户”概念; Subject 代表了当前用户的安全操作，SecurityManager 则管理所有用户的安全操作;

+ SecurityManager
  > 它是 Shiro 框架的核心，典型的 Facade 模式，Shiro 通过SecurityManager 来管理内部组件实例，并通过它来提供安全管理的各种服务;

+ Realm
  > Realm 充当了 Shiro 与应用安全数据间的“桥梁”或者“连接器”; 也就是说，当对用户执行认证（登录）和授权（访问控制）验证时，Shiro 会从应用配置的 Realm 中查找用户及其权限信息;

## 2.Shiro 主要的四个组件

+ SecurityManager
  > 典型的 Facade，Shiro 通过它对外提供安全管理的各种服务;

+ Authenticator
  > 对“Who are you ？”进行核实; 通常涉及用户名和密码;  这个组件负责收集 principals 和 credentials，并将它们提交给应用系统; 如果提交的 credentials 跟应用系统中提供的 credentials 吻合，就能够继续访问，否则需要重新提交 principals 和 credentials， 或者直接终止访问;

+ Authorizer
  > 身份份验证通过后，由这个组件对登录人员进行访问控制的筛查，比如“who can do what”， 或者“who can do which actions”;  Shiro 采用“基于  Realm”的方法，即用户（又称 Subject）、 用户组、角 色和 permission 的聚合体;

+ Session Manager
  > 这个组件保证了异构客户端的访问，配置简单; 它是基于 POJO/J2SE 的，不跟任何的客户 端或者协议绑定;

## 3.Shiro 的运行原理

Application Code -> Subject -> SecurityManage -> Realm;

1. Application Code:
   > 应用程序代码，就是我们自己的编码，如果在程序中需要进行权限控制，需要调用 Subject 的 API;

2. Subject:
   > 主体，代表的了当前用户; 所有的 Subject 都绑定到 SecurityManager， 与 Subject 的所有交互都会委托给 SecurityManager,可以将 Subject 当成一个门面，而真正执行者是 SecurityManager ;

3. SecurityManage:
   > 安全管理器，所有与安全有关的操作都会与 SecurityManager 交互，并且它管理所有的 Subject ;

4. Realm:
   > 域 shiro 是从 Realm 来获取安全数据（用户，角色，权限）; 就是说 SecurityManager 要验证用户身份， 那么它需要从 Realm 获取相应的用户进行比较以确定用户身份是否合法；也需要从Realm 得到用户相应的角色/权限进行验证用户是否能进行操作； 可以把 Realm 看成 DataSource，即安全数据源 ;

## 4.Shiro 的四种权限控制方式

1. 在自定义的 realm 中进行权限控制
2. 使用 shiro 注解为用户授权
3. 使用 shiro 标签进行权限控制
4. 编程方式实现用户权限控制

## 5.什么是粗颗粒和细颗粒权限

+ 粗颗粒权限
  > 针对url链接的控制;

+ 细颗粒权限
  > 针对数据级别的控制;

## 6.粗颗粒和细颗粒如何授权

+ 粗颗粒权限
  > 可以使用过虑器统一拦截url;

+ 细颗粒权限
  > 在service中控制，在程序级别来控制，个性化编程
  