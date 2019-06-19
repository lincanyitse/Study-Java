# 第四十七天

## Java连接数据库

### 步骤

1. 加载驱动

2. 获取连接

3. 获取执行语句对象

4. 完善执行语句

5. 提交执行

6. 关闭连接

### 实例

+ oracle 版本

  + 添加数据

    ```Java
    // 导入jre包后
    import java.sql.DriverManager;
    import java.sql.Connection;
    import java.sql.PreparedStatement;
    ```

    ```Java
    try{
        // 加载驱动
        Class.forName("oracle.jdbc.OracleDriver");
        // 获取连接
        Connection conn=DriverManager.getConnection("jdbc:oracle:thin:@localhost:端口:orcl","用户","密码");
        // 执行语句对象
        String sql="insert into 表名 values(自增序列名.nextval,?,?,to_date(?,'yyyy-MM-dd'))"; // 添加sql语句
        PreparedStatement pstm= sconn.prepareStatement(sql);
        // 添加数据
        pstm.setString(1,"张三"); // 设置上述sql语句第一个问号?内容
        pstm.setInt(2,9); // 设置上述sql语句第二个问号?内容
        pstm.setString(3, "2019-06-18"); // 设置上述sql语句第三个问号?内容
        // 返回结果
        int row=pstm.executeUpdate();
        System.out.println("成功:" + row);
        // 关闭连接
        pstm.close();
        conn.close();
    }catch(Exception ex){
        ex.printStackTrace();
    }
    ```

  + 删除数据

     ```Java
    // 导入jre包后
    import java.sql.DriverManager;
    import java.sql.Connection;
    import java.sql.PreparedStatement;
    ```

    ```Java
    try{
        // 加载驱动
        Class.forName("oracle.jdbc.OracleDriver");
        // 获取连接
        Connection conn=DriverManager.getConnection("jdbc:oracle:thin:@localhost:端口:orcl","用户","密码");
        // 执行语句对象
        String sql="delete [from] 表名 [where 条件]"; // 添加sql语句
        PreparedStatement pstm= sconn.prepareStatement(sql);
        // 返回结果
        int row=pstm.executeUpdate();
        System.out.println("成功:" + row);
        // 关闭连接
        pstm.close();
        conn.close();
    }catch(Exception ex){
        ex.printStackTrace();
    }
    ```

  + 修改数据

     ```Java
    // 导入jre包后
    import java.sql.DriverManager;
    import java.sql.Connection;
    import java.sql.PreparedStatement;
    ```

    ```Java
    try{
        // 加载驱动
        Class.forName("oracle.jdbc.OracleDriver");
        // 获取连接
        Connection conn=DriverManager.getConnection("jdbc:oracle:thin:@localhost:端口:orcl","用户","密码");
        // 执行语句对象
        String sql="update 表名 set 列名1=列值1[, 列名2=列值2,...][where 条件];"; // 添加sql语句
        PreparedStatement pstm= sconn.prepareStatement(sql);
        // 返回结果
        int row=pstm.executeUpdate();
        System.out.println("成功:" + row);
        // 关闭连接
        pstm.close();
        conn.close();
    }catch(Exception ex){
        ex.printStackTrace();
    }
    ```

  + 查询数据

    ```Java
    // 导入jre包后
    import java.sql.DriverManager;
    import java.sql.Connection;
    import java.sql.PreparedStatement;
    import java.sql.ResultSet;
    ```

    ```Java
    try{
        // 加载驱动
        Class.forName("oracle.jdbc.OracleDriver");
        // 获取连接
        Connection conn=DriverManager.getConnection("jdbc:oracle:thin:@localhost:端口:orcl","用户","密码");
        // 执行语句对象
        String sql="select 字段名1 [别名1][, 字段名2 [别名2], ...] from 表名 [where 条件]"; // 查询sql语句
        PreparedStatement pstm= sconn.prepareStatement(sql);
        // 获取结果
        ResultSet rs=pstm.executeUpdate();
        while(rs.next){
            system.out.print(rs.getInt(1) + ",");
            system.out.print(rs.getString(2) + ",");
            system.out.print(rs.getDate(3));
            system.out.println();
        }
        // 关闭连接
        pstm.close();
        conn.close();
    }catch(Exception ex){
        ex.printStackTrace();
    }
    ```

  + 模糊查询

    ```Java
    // 导入jre包后
    import java.sql.DriverManager;
    import java.sql.Connection;
    import java.sql.PreparedStatement;
    import java.sql.ResultSet;
    ```

    ```Java
    try{
        // 加载驱动
        Class.forName("oracle.jdbc.OracleDriver");
        // 获取连接
        Connection conn=DriverManager.getConnection("jdbc:oracle:thin:@localhost:端口:orcl","用户","密码");
        // 执行语句对象
        String sql="select 字段名1 [别名1][, 字段名2 [别名2], ...] from 表名 where 列名 LIKE '匹配方法' "; // 查询sql语句
        PreparedStatement pstm= sconn.prepareStatement(sql);
        // 获取结果
        ResultSet rs=pstm.executeUpdate();
        while(rs.next){
            system.out.print(rs.getInt(1) + ",");
            system.out.print(rs.getString(2) + ",");
            system.out.print(rs.getDate(3));
            system.out.println();
        }
        // 关闭连接
        pstm.close();
        conn.close();
    }catch(Exception ex){
        ex.printStackTrace();
    }
    ```
