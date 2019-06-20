# 第四十八天

## 数据库事务

### 转账事务

+ 实现

    ```Java
    public boolean tran(int id1,int id2,double money){
        boolean flag=false;
        try{
            Connection conn=DBU.getConn();
            conn.setAutoCommit(false);//自动提交关闭
            String sql="update copyemp018 set sal=sal+? where empno = ?";
            PreparedStatement pstm=(PreparedStatement) conn.prepareStatement(sql);

            pstm.setDouble(1, -money);
            pstm.setInt(2, id1);
            int row1=pstm.executeUpdate();
            pstm.setDouble(1, money);
            pstm.setInt(2, id2);
            int row2=pstm.executeUpdate();

            if(row1==1&&row2==1){
                conn.commit();
                flag=true;
            }else{
                conn.rollback();
            }
            conn.setAutoCommit(true);
            DBU.closeAll(conn, pstm, null);
        }catch(Exception e){
            e.printStackTrace();
        }
        return flag;
    }
    ```

## 批处理

### 批量添加

+ 实现

    ```Java
    //批处理----添加1000条数据的方法(采用批处理后处理时间由5.5秒左右变为1秒左右)
    public int[] batch(){
        int[] rows = new int[10000];
        try{
            Connection conn=DBU.getConn();
            String sql="insert into user0618 values(seq_user0618.nextval,?,?,to_date(?,'yyyy-MM-dd'))";
            PreparedStatement pstm=(PreparedStatement) conn.prepareStatement(sql);
            for(int i=0;i<rows.length;i++){
                pstm.setString(1, "数据"+i+"号");
                pstm.setInt(2, i);
                pstm.setString(3, "2019-06-19");
                pstm.addBatch();/////////重点,采用批处理后不再是10000条sql语句而是一条
                //rows[i]=pstm.executeUpdate();
            }
            rows=pstm.executeBatch();/////////重点
            for(int i=0;i<rows.length;i++){
                if(rows[i]==0){
                    System.out.println("第"+i+"条数据失败！");
                }
            }
            DBU.closeAll(conn, pstm, null);
        }catch(Exception e){
            e.printStackTrace();
        }
        return rows;
    }
    ```

## 数据池

### 步骤

1. 加载配置文件

2. 得到数据源

3. 获取连接

### 实例二

+ druid

    ```Java
    import com.alibaba.druid.pool.DruidDataSourceFactory;

    import javax.sql.DataSource;
    import java.io.FileInputStream;
    import java.sql.Connection;
    import java.util.Properties;

    public class DruidDBU {
        public static DataSource ds=null;

        static {
            try {
                // 加载配置文件
                FileInputStream fis = new FileInputStream("src/db.properties");
                Properties p = new Properties();
                p.load(fis);
                // 得到数据源
                ds = DruidDataSourceFactory.createDataSource(p);
            } catch (Exception e) {
                e.printStackTrace();
            }
        }

        public static Connection getConnection() throws Exception{
            // 获取连接
            return ds.getConnection();
        }
    }
    ```

+ tomcat

    ```Java
    import javax.naming.Context;
    import javax.naming.InitialContext;
    import javax.naming.NamingException;
    import javax.sql.DataSource;
    import java.sql.Connection;

    public class JndiDBU {
        public static DataSource dSource = null;

        static {
            try{
                Context context = new InitialContext();
                dSource = (DataSource) context.lookup("java:comp/env/jdbc/local");
            } catch (NamingException e) {
                e.printStackTrace();
            }
        }

        public static Connection getConnection() throws Exception{
            // 获取连接
            return dSource.getConnection();
        }
    }
    ```
