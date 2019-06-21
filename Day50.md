# 第五十天

## 过滤器

### 登录过滤器

+ LoginFilter

    ```Java
    package com.dfbz.filter;

    import com.dfbz.model.User;
    import com.dfbz.utils.Check;
    import com.dfbz.utils.Select;

    import javax.servlet.*;
    import javax.servlet.annotation.WebFilter;
    import javax.servlet.http.HttpServletRequest;
    import javax.servlet.http.HttpServletResponse;
    import java.io.IOException;
    import java.util.*;

    @WebFilter(filterName = "loginFilter", value = "/*")
    public class LoginFilter implements Filter {
        public void destroy() {
            System.out.println("过滤器销毁！");
        }

        public void doFilter(ServletRequest req, ServletResponse resp, FilterChain chain) throws ServletException, IOException {
            req.setCharacterEncoding("utf-8");
            resp.setCharacterEncoding("utf-8");
            // 转型
            HttpServletRequest request = (HttpServletRequest) req;
            HttpServletResponse response = (HttpServletResponse) resp;
            System.out.println("过滤开始");
            boolean flag = false;
            // 获取访问资源路径
            String path = request.getRequestURI();
            // 获取权限路径集
            List<String> allowPath = new ArrayList<>(Arrays.asList("login.html", "loginServlet"));
            if (request.getSession().getAttribute("user") != null) {
                allowPath.addAll(Select.selectUrlPath(((User) request.getSession().getAttribute("user")).getId()));
            }
            // 判断路径是否需要过滤
            if (Check.checkPath(path, allowPath)) {
                flag = true;
            }
            // 执行
            if (flag) {
                System.out.println("成功路径" + path);
                chain.doFilter(req, resp);
            } else {
                System.out.println("失败路径" + path);
                response.sendRedirect("login.html");
            }
            System.out.println("过滤结束");
        }

        public void init(FilterConfig config) throws ServletException {
            System.out.println("过滤器初始化！");
        }

    }
    ```

+ LoginServlet

    ```Java
    package com.dfbz.servlet;

    import com.dfbz.model.User;
    import com.dfbz.utils.Select;

    import javax.servlet.ServletException;
    import javax.servlet.annotation.WebServlet;
    import javax.servlet.http.HttpServlet;
    import javax.servlet.http.HttpServletRequest;
    import javax.servlet.http.HttpServletResponse;
    import java.io.IOException;

    @WebServlet(name = "LoginServlet", urlPatterns = "/loginServlet")
    public class LoginServlet extends HttpServlet {
        protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
            doGet(request, response);
        }

        protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
            String username = request.getParameter("username");
            String password = request.getParameter("password");
            User user = Select.selectkUser(username, password);
            if (user != null) {
                request.getSession().setAttribute("user", user);
                request.getSession().setAttribute("username", user.getUsername());
                response.sendRedirect("indexServlet");
            } else {
                response.sendRedirect("login.html");
            }
        }
    }
    ```

+ Check

    ```Java
    package com.dfbz.utils;

    import java.util.List;

    public class Check {
        public static boolean checkPath(String current, List<String> paths) {
            for (String path : paths) {
                if (current.contains(path)) {
                    return true;
                }
            }
            return false;
        }


    }
    ```

+ Select

    ```Java
    package com.dfbz.utils;

    import com.dfbz.model.User;
    import com.lincanyitse.tools.Oracle;

    import java.sql.Connection;
    import java.sql.PreparedStatement;
    import java.sql.ResultSet;
    import java.sql.SQLException;
    import java.util.ArrayList;
    import java.util.List;

    public class Select {
        public static List<String> selectUrlPath(int uid) {
            List<String> pathList = new ArrayList<>();
            try {
                Connection conn = Oracle.getConnection();
                String sql = "select * from role0621 where user_id=?";
                PreparedStatement ps = conn.prepareStatement(sql);
                ps.setInt(1, uid);
                ResultSet rs = ps.executeQuery();
                while (rs.next()) {
                    pathList.add(rs.getString(2));
                }
                Oracle.closeAll(ps, rs);
            } catch (SQLException e) {
                e.printStackTrace();
            }
            return pathList;
        }

        public static User selectkUser(String username, String password) {
            User user = null;
            try {
                Connection conn = Oracle.getConnection();
                String sql = "select * from user0621 where username=? and password=?";
                PreparedStatement ps = conn.prepareStatement(sql);
                ps.setString(1, username);
                ps.setString(2, password);
                ResultSet rs = ps.executeQuery();
                if (rs.next()) {
                    user = new User();
                    user.setId(rs.getInt(1));
                    user.setUsername(rs.getString(2));
                    user.setPassword(rs.getString(3));
                }
                Oracle.closeAll(ps, rs);
            } catch (SQLException e) {
                e.printStackTrace();
            }
            return user;
        }
    }

    ```

## 监听器

### 访问监听

+ ServerListener

    ```Java
    package com.dfbz.listener;

    import com.sun.corba.se.impl.interceptors.ServerRequestInfoImpl;

    import javax.servlet.ServletContextEvent;
    import javax.servlet.ServletContextListener;
    import javax.servlet.ServletRequestEvent;
    import javax.servlet.annotation.WebListener;
    import javax.servlet.http.*;

    @WebListener()
    public class ServerListener implements ServletContextListener,
            HttpSessionListener, HttpSessionAttributeListener {

        // Public constructor is required by servlet spec
        public ServerListener() {
            System.out.println("监听器构造");
        }

        // -------------------------------------------------------
        // ServletContextListener implementation
        // -------------------------------------------------------
        public void contextInitialized(ServletContextEvent sce) {
        /* This method is called when the servlet context is
            initialized(when the Web application is deployed). 
            You can initialize servlet context related data here.
        */
            System.out.println("监听器：context创建");
        }

        public void contextDestroyed(ServletContextEvent sce) {
        /* This method is invoked when the Servlet Context 
            (the Web application) is undeployed or 
            Application Server shuts down.
        */
            System.out.println("监听器：context销毁");
        }

        // -------------------------------------------------------
        // HttpSessionListener implementation
        // -------------------------------------------------------
        public void sessionCreated(HttpSessionEvent se) {
            /* Session is created. */
            System.out.println("监听器：session创建");
        }

        public void sessionDestroyed(HttpSessionEvent se) {
            /* Session is destroyed. */
            System.out.println("监听器：session销毁");
        }

        // -------------------------------------------------------
        // HttpSessionAttributeListener implementation
        // -------------------------------------------------------

        public void attributeAdded(HttpSessionBindingEvent sbe) {
        /* This method is called when an attribute 
            is added to a session.
        */
            System.out.println("监听器：attribute添加");
        }

        public void attributeRemoved(HttpSessionBindingEvent sbe) {
        /* This method is called when an attribute
            is removed from a session.
        */
            System.out.println("监听器：attribute移除");
        }

        public void attributeReplaced(HttpSessionBindingEvent sbe) {
        /* This method is invoked when an attibute
            is replaced in a session.
        */
            System.out.println("监听器：attribute更改");
        }

        public void requestInitialized(ServletRequestEvent sre){
            System.out.println("监听器：request创建");
        }

        public void requestDestroyed(ServletRequestEvent sre){
            System.out.println("监听器：request销毁");
        }
    }
    ```

## web.xml配置

### 配置和映射Servlet

+ 实例

    ```xml
    <!-- 配置单Servlet -->
    <servlet>
        <!-- 配置Servlet名 -->
        <servlet-name>controlServlet</servlet-name>
        <!-- 配置Servlet包全路径-->
        <servlet-class>com.xxx.ControlServlet</servlet-class>
        <!-- 配置Servlet初始化参数 -->
        <init-param>
            <!-- 配置Servlet初始化参数的键名 -->
            <param-name>myParam</param-name>
            <!-- 配置Servlet初始化参数的键值 -->
            <param-value>paramValue</param-value>
        </init-param>
        <!-- Servlet容器加载时执行顺序 -->
        <load-on-startup>1</load-on-startup>
    </servlet>

    <!-- 映射Servlet -->
    <servlet-mapping>
        <!-- 映射到Servlet名 -->
        <servlet-name>controlServlet</servlet-name>
        <!-- 什么url地址映射到Servlet -->
        <url-pattern>*.html</url-pattern>
    </servlet-mapping>
    ```

    在对应的 Servlet 里的 init 获取初始化参数

    ```Java
    public void init(ServletConfig servletConfig) throws ServletException{
        this.myParam = servletConfig.getInitParameter("myParam");
    }
    ```

### 全局变量

+ 实例

    ```xml
    <!-- 配置全局变量 -->
    <context-param>
        <!-- 全局变量名 -->
        <param-name>myParam</param-name>
        <!-- 全局变量值 -->
        <param-value>the value</param-value>
    </context-param>
    ```

    ```Java
    String myContextParam = request.getSession().getServletContext().getInitParameter("myParam");
    ```

### web.xml 过滤器

+ 实例

    ```xml
    <!-- 配置过滤器 -->
    <filter>
        <!-- 设置过滤器名 -->
        <filter-name>encodeFilter</filter-name>
        <!-- 设置过滤器包全路径 -->
        <filter-class>com.dfbz.filter.AllFilter</filter-class>
        <!-- 过滤器容器执行顺序 -->
        <load-on-startup>1</load-on-startup>
    </filter>
    <!-- 映射过滤器 -->
    <filter-mapping>
        <!-- 映射过滤器名 -->
        <filter-name>encodeFilter</filter-name>
        <!-- 什么路径进入过滤器 -->
        <url-pattern>/*</url-pattern>
    </filter-mapping>
    ```

### web.xml 监听器

+ 实例

    ```xml
    <!-- 配置监听器 -->
    <listener>
        <!-- 设置监听器包全路径 -->
            <listener-class>com.dfbz.listener.AllListener</listener-class>
    </listener>
    ```

### web.xml 启动页面

+ 实例

    ```xml
    <!-- 配置启动页面 -->
    <welcome-file-list>
        <!-- 从上到下，如果第一条对应文件不存在，则加载第二条对应文件 -->
        <welcome-file>index.html</welcome-file>
        <welcome-file>index.jsp</welcome-file>
        <welcome-file>form.html</welcome-file>
    </welcome-file-list>
    ```

### web.xml 错误页面

+ 实例

    ```xml
    <!-- 配置地址错误 -->
    <error-page>
        <!-- 错误状态码 -->
        <error-code>404</error-code>
        <!-- 状态码对应文件 -->
        <location>/error.html</location>
    </error-page>
    <!-- 配置后台异常 -->
    <error-page>
        <!-- 异常全类名 -->
        <exception-type>java.lang.NullPointerException</exception-type>
        <!-- 异常对应文件 -->
        <location>/index.html</location>
    </error-page>
    ```
