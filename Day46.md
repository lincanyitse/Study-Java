# Servlet 详解

## HttpServletRequest 类

> `HttpServletRequest` 对象代表客户端的请求 , 当客户端通过HTTP协议访问服务器时 , HTTP请求头中的所有信息都封装在这个对象中 , 开发人员通过这个对象的方法 , 可以获得客户这些信息;
> `request` 就是将请求文本封装而成的对象 , 所以通过 request 能获得请求文本中的所有内容 , 请求头、请求体、请求行;

### HttpServletRequest 属性

|头信息|描述|
|:---:|:---|
|`Accept`|这个头信息指定浏览器或其他客户端可以处理的 MIME 类型|值 image/png 或 image/jpeg 是最常见的两种可能值|
|`Accept-Charset`|这个头信息指定浏览器可以用来显示信息的字符集|例如 ISO-8859-1|
|`Accept-Encoding`|这个头信息指定浏览器知道如何处理的编码类型|值 gzip 或 compress 是最常见的两种可能值|
|`Accept-Language`|这个头信息指定客户端的首选语言 , 在这种情况下 , Servlet 会产生多种语言的结果|例如 , en、en-us、ru 等|
|`Authorization`|这个头信息用于客户端在访问受密码保护的网页时识别自己的身份|
|`Connection`|这个头信息指示客户端是否可以处理持久 HTTP 连接|持久连接允许客户端或其他浏览器通过单个请求来检索多个文件|值 Keep-Alive 意味着使用了持续连接|
|`Content-Length`|这个头信息只适用于 POST 请求 , 并给出 POST 数据的大小（以字节为单位）|
|`Cookie`|这个头信息把之前发送到浏览器的 cookies 返回到服务器|
|`Host`|这个头信息指定原始的 URL 中的主机和端口|
|`If-Modified-Since`|这个头信息表示只有当页面在指定的日期后已更改时 , 客户端想要的页面|如果没有新的结果可以使用 , 服务器会发送一个 304 代码 , 表示 Not Modified 头信息|
|`If-Unmodified-Since`|这个头信息是 If-Modified-Since 的对立面 , 它指定只有当文档早于指定日期时 , 操作才会成功|
|`Referer`|这个头信息指示所指向的 Web 页的 URL|例如 , 如果您在网页 1 , 点击一个链接到网页 2 , 当浏览器请求网页 2 时 , 网页 1 的 URL 就会包含在 Referer 头信息中|
|`User-Agent`|这个头信息识别发出请求的浏览器或其他客户端 , 并可以向不同类型的浏览器返回不同的内容|

### HttpServletRequest 方法

|序号|方法 & 描述|
|:---:|:---|
|1|`Cookie[] getCookies()`  返回一个数组 , 包含客户端发送该请求的所有的 Cookie 对象|
|2|`Enumeration getAttributeNames()` 返回一个枚举 , 包含提供给该请求可用的属性名称|
|3|`Enumeration getHeaderNames()` 返回一个枚举 , 包含在该请求中包含的所有的头名|
|4|`Enumeration getParameterNames()` 返回一个 String 对象的枚举 , 包含在该请求中包含的参数的名称|
|5|`HttpSession getSession()` 返回与该请求关联的当前 session 会话 , 或者如果请求没有 session 会话 , 则创建一个|
|6|`HttpSession getSession(boolean create)` 返回与该请求关联的当前 HttpSession , 或者如果没有当前会话 , 且创建是真的 , 则返回一个新的 session 会话|
|7|`Locale getLocale()` 基于 Accept-Language 头 , 返回客户端接受内容的首选的区域设置|
|8|`Object getAttribute(String name)` 以对象形式返回已命名属性的值 , 如果没有给定名称的属性存在 , 则返回 null|
|9|`ServletInputStream getInputStream()` 使用 ServletInputStream , 以二进制数据形式检索请求的主体|
|10|`String getAuthType()` 返回用于保护 Servlet 的身份验证方案的名称 , 例如 , "BASIC" 或 "SSL" , 如果JSP没有受到保护则返回 null|
|11|`String getCharacterEncoding()` 返回请求主体中使用的字符编码的名称|
|12|`String getContentType()` 返回请求主体的 MIME 类型 , 如果不知道类型则返回 null|
|13|`String getContextPath()` 返回指示请求上下文的请求 URI 部分|
|14|`String getHeader(String name)` 以字符串形式返回指定的请求头的值|
|15|`String getMethod()` 返回请求的 HTTP 方法的名称 , 例如 , GET、POST 或 PUT|
|16|`String getParameter(String name)` 以字符串形式返回请求参数的值 , 或者如果参数不存在则返回 null|
|17|`String getPathInfo()` 当请求发出时 , 返回与客户端发送的 URL 相关的任何额外的路径信息|
|18|`String getProtocol()` 返回请求协议的名称和版本|
|19|`String getQueryString()` 返回包含在路径后的请求 URL 中的查询字符串|
|20|`String getRemoteAddr()` 返回发送请求的客户端的互联网协议（IP）地址|
|21|`String getRemoteHost()` 返回发送请求的客户端的完全限定名称|
|22|`String getRemoteUser()` 如果用户已通过身份验证 , 则返回发出请求的登录用户 , 或者如果用户未通过身份验证 , 则返回 null|
|23|`String getRequestURI()` 从协议名称直到 HTTP 请求的第一行的查询字符串中 , 返回该请求的 URL 的一部分|
|24|`String getRequestedSessionId()` 返回由客户端指定的 session 会话 ID|
|25|`String getServletPath()` 返回调用 JSP 的请求的 URL 的一部分|
|26|`String[] getParameterValues(String name)` 返回一个字符串对象的数组 , 包含所有给定的请求参数的值 , 如果参数不存在则返回 null|
|27|`boolean isSecure()` 返回一个布尔值 , 指示请求是否使用安全通道 , 如 HTTPS|
|28|`int getContentLength()` 以字节为单位返回请求主体的长度 , 并提供输入流 , 或者如果长度未知则返回 -1|
|29|`int getIntHeader(String name)` 返回指定的请求头的值为一个 int 值|
|30|`int getServerPort()` 返回接收到这个请求的端口号|
|31|`int getParameterMap()` 将参数封装成 Map 类型|

### 实例

```Java

```

## HttpServletResponse 类

> `HttpServletResponse` 对象代表服务器的响应;这个对象中封装了向客户端发送数据、发送响应头 , 发送响应状态码的方法;

### HttpServletResponse 属性

|头信息|描述|
|:---:|:---|
|`Allow`|这个头信息指定服务器支持的请求方法（GET、POST 等）|
|`Cache-Control`|这个头信息指定响应文档在何种情况下可以安全地缓存|可能的值有：public、private 或 no-cache 等|Public 意味着文档是可缓存 , Private 意味着文档是单个用户私用文档 , 且只能存储在私有（非共享）缓存中 , no-cache 意味着文档不应被缓存|
|`Connection`|这个头信息指示浏览器是否使用持久 HTTP 连接|值 close 指示浏览器不使用持久 HTTP 连接 , 值 keep-alive 意味着使用持久连接|
|`Content-Disposition`|这个头信息可以让您请求浏览器要求用户以给定名称的文件把响应保存到磁盘|
|`Content-Encoding`|在传输过程中 , 这个头信息指定页面的编码方式|
|`Content-Language`|这个头信息表示文档编写所使用的语言|例如 , en、en-us、ru 等|
|`Content-Length`|这个头信息指示响应中的字节数|只有当浏览器使用持久（keep-alive）HTTP 连接时才需要这些信息|
|`Content-Type`|这个头信息提供了响应文档的 MIME（Multipurpose Internet Mail Extension）类型|
|`Expires`|这个头信息指定内容过期的时间 , 在这之后内容不再被缓存|
|`Last-Modified`|这个头信息指示文档的最后修改时间|然后 , 客户端可以缓存文件 , 并在以后的请求中通过 If-Modified-Since 请求头信息提供一个日期|
|`Location`|这个头信息应被包含在所有的带有状态码的响应中|在 300s 内 , 这会通知浏览器文档的地址|浏览器会自动重新连接到这个位置 , 并获取新的文档|
|`Refresh`|这个头信息指定浏览器应该如何尽快请求更新的页面|您可以指定页面刷新的秒数|
|`Retry-After`|这个头信息可以与 503（Service Unavailable 服务不可用）响应配合使用 , 这会告诉客户端多久就可以重复它的请求|
|`Set-Cookie`|这个头信息指定一个与页面关联的 cookie|

### HttpServletResponse 方法

|序号|方法|描述|
|:---:|:---:|:---|
|1|`String encodeRedirectURL(String url)`|为 sendRedirect 方法中使用的指定的 URL 进行编码，或者如果编码不是必需的，则返回 URL 未改变|
|2|`String encodeURL(String url)`|对包含 session 会话 ID 的指定 URL 进行编码，或者如果编码不是必需的，则返回 URL 未改变|
|3|`boolean containsHeader(String name)`|返回一个布尔值，指示是否已经设置已命名的响应报头|
|4|`boolean isCommitted()`|返回一个布尔值，指示响应是否已经提交|
|5|`void addCookie(Cookie cookie)`|把指定的 cookie 添加到响应|
|6|`void addDateHeader(String name, long date)`|添加一个带有给定的名称和日期值的响应报头|
|7|`void addHeader(String name, String value)`|添加一个带有给定的名称和值的响应报头|
|8|`void addIntHeader(String name, int value)`|添加一个带有给定的名称和整数值的响应报头|
|9|`void flushBuffer()`|强制任何在缓冲区中的内容被写入到客户端|
|10|`void reset()`|清除缓冲区中存在的任何数据，包括状态码和头|
|11|`void resetBuffer()`|清除响应中基础缓冲区的内容，不清除状态码和头|
|12|`void sendError(int sc)`|使用指定的状态码发送错误响应到客户端，并清除缓冲区|
|13|`void sendError(int sc, String msg)`|使用指定的状态发送错误响应到客户端|
|14|`void sendRedirect(String location)`|使用指定的重定向位置 URL 发送临时重定向响应到客户端|
|15|`void setBufferSize(int size)`|为响应主体设置首选的缓冲区大小|
|16|`void setCharacterEncoding(String charset)`|设置被发送到客户端的响应的字符编码（MIME 字符集）例如，UTF-8|
|17|`void setContentLength(int len)`|设置在 HTTP Servlet 响应中的内容主体的长度，该方法设置 HTTP Content-Length 头|
|18|`void setContentType(String type)`|如果响应还未被提交，设置被发送到客户端的响应的内容类型|
|19|`void setDateHeader(String name, long date)`|设置一个带有给定的名称和日期值的响应报头|
|20|`void setHeader(String name, String value)`|设置一个带有给定的名称和值的响应报头|
|21|`void setIntHeader(String name, int value)`|设置一个带有给定的名称和整数值的响应报头|
|22|`void setLocale(Locale loc)`|如果响应还未被提交，设置响应的区域|
|23|`void setStatus(int sc)`|为该响应设置状态码|

## Web小实战

### Web下载

+ 源码：

    ```Java
    import java.io.*;
    import java.net.*;
    import javax.servlet.ServletException;
    import javax.servlet.annotation.WebServlet;
    import javax.servlet.http.*;

    @WebServlet(name = "downloadServlet", urlPatterns = { "/downloadServlet" })
    public class DownloadServlet extends HttpServlet {
        private static final long serialVersionUID = 1L;

        public DownloadServlet() {
            super();
            // TODO Auto-generated constructor stub
        }

        protected void toGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException{
            String filename = request.getParameter("filename");
            FileInputStream fis = new FileInputStream(filename);
            // 设置头部信息
            response.setContentType("application/x-mxdownload");
            response.setHeader("Content-disposition","attachment;filename=" + URLEncoder.encode(filename,"utf-8"));
            long length= new File(filename).length();
            response.setHeader("Content length",String.valueOf(length));
            // 返回文件流
            OutputStream os = response.getOutputStream();
            int len=0;
            byte[] bytes=new byte[8192];
            while ((len=fis.read(bytes))!=-1){
                os.write(bytes,0,len);
            }
            os.flush();
            os.close();
            fis.close();
        }

        protected void toPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
            toGet(request,response);
        }
    }
    ```

### Web上传

+ 源码：

    ```Java

    ```
