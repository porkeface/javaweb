- # Web A 考点整理

  ## 选择题（14×2）

  ## HTML与Web基础 

  1. HTML form标签使用：
  
     ```html
         <!-- form 标签开始 -->
         <form action="/register" method="post" enctype="application/x-www-form-urlencoded">
             
             <!-- 文本输入框 -->
             <div class="form-group">
                 <label for="username">用户名:</label>
                 <input type="text" id="username" name="username" required 
                        placeholder="请输入用户名" minlength="4" maxlength="20">
             </div>
             
             <!-- 密码输入框 -->
             <div class="form-group">
                 <label for="password">密码:</label>
                 <input type="password" id="password" name="password" required
                        placeholder="请输入密码" minlength="6">
             </div>
             
             <!-- 邮箱输入框 -->
             <div class="form-group">
                 <label for="email">电子邮箱:</label>
                 <input type="email" id="email" name="email" required
                        placeholder="example@domain.com">
             </div>
             
             <!-- 单选按钮 -->
             <div class="form-group">
                 <label>性别:</label>
                 <label><input type="radio" name="gender" value="male" checked> 男</label>
                 <label><input type="radio" name="gender" value="female"> 女</label>
             </div>
             
             <!-- 下拉选择框 -->
             <div class="form-group">
                 <label for="country">国家/地区:</label>
                 <select id="country" name="country">
                     <option value="">--请选择--</option>
                     <option value="china">中国</option>
                     <option value="usa">美国</option>
                     <option value="uk">英国</option>
                 </select>
             </div>
             
             <!-- 多选框 -->
             <div class="form-group">
                 <label>兴趣爱好:</label>
                 <label><input type="checkbox" name="hobbies" value="reading"> 阅读</label>
                 <label><input type="checkbox" name="hobbies" value="sports"> 运动</label>
                 <label><input type="checkbox" name="hobbies" value="music"> 音乐</label>
             </div>
             
             <!-- 文件上传 -->
             <div class="form-group">
                 <label for="avatar">头像上传:</label>
                 <input type="file" id="avatar" name="avatar" accept="image/*">
             </div>
             
             <!-- 隐藏域 -->
             <input type="hidden" name="token" value="abc123xyz">
             
             <!-- 提交按钮 -->
             <button type="submit">注册</button>
             
             <!-- 重置按钮 -->
             <button type="reset">重置</button>
         </form>
         <!-- form 标签结束 -->
     ```
  
     - action属性（定义提交到哪）
  
       ## 1. action 属性的基本定义
  
       `action` 是 HTML `<form>` 标签的一个**必需属性**，它用于指定当用户提交表单时，表单数据应该发送到哪个服务器端程序或页面进行处理。
  
       ## 2. action 属性的语法
  
       ```html
       <form action="URL">
         <!-- 表单内容 -->
       </form>
       ```
  
       ## 3. action 属性的取值
  
       ### (1) 绝对 URL
  
       ```html
       <form action="https://example.com/process-form.php">
       ```
  
       - 提交到其他网站的指定地址
       - 需要完整的协议和域名
  
       ### (2) 相对 URL（最常用）
  
       ```html
       <form action="/submit-data">
       <form action="process.php">
       <form action="../handlers/save-info">
       ```
  
       - 提交到当前网站的不同路径
       - 可以是相对于当前页面的路径
  
       ### (3) 空值或当前页面
  
       ```html
       <form action="">
       <form>
       ```
  
       - 提交到当前页面本身
       - 常用于表单自处理（如PHP中检查`$_SERVER["REQUEST_METHOD"]`）
  
       ## 4. action 属性的工作原理
  
       1. 用户在表单中输入数据
       2. 点击提交按钮
       3. 浏览器收集表单数据
       4. 按照`action`指定的URL发送数据
       5. 服务器端程序接收并处理数据
  
       ## 5. 实际应用示例
  
       ### 示例1：提交到PHP处理页面
  
       ```html
       <form action="process_login.php" method="post">
         用户名: <input type="text" name="username">
         密码: <input type="password" name="password">
         <input type="submit" value="登录">
       </form>
       ```
  
       ### 示例2：提交到API接口
  
       ```html
       <form action="https://api.example.com/users" method="post">
         <!-- 注册表单内容 -->
       </form>
       ```
  
       ### 示例3：当前页面处理
  
       ```html
       <!-- 假设这是index.php文件 -->
       <form action="" method="post">
         <input type="text" name="search">
         <button type="submit">搜索</button>
       </form>
       
       <?php
       if ($_SERVER["REQUEST_METHOD"] == "POST") {
           // 处理表单提交
           $searchTerm = $_POST["search"];
           // 执行搜索逻辑...
       }
       ?>
       ```
  
       **文件上传**：
  
       - 如需上传文件，除了设置action外，还需要：
  
         ```html
         <form action="upload.php" method="post" enctype="multipart/form-data">
         ```
  
     - method属性（定义提交方式）
       
       - get、post两种请求方式
       
         ## 1. method 属性的基本定义
       
         `method` 是 HTML `<form>` 标签的关键属性，它定义了**表单数据如何发送到服务器**。它决定了HTTP请求的类型，直接影响数据如何传输以及如何在服务器端接收这些数据。
       
         ## 2. method 属性的可选值
       
         ### (1) GET 方法（默认值）
       
         ```html
         <form action="/search" method="get">
         ```
       
         ### (2) POST 方法
       
         ```html
         <form action="/login" method="post">
         ```
       
         ## 3. GET 与 POST 的核心区别
       
         | 特性              | GET 方法                   | POST 方法                    |
         | :---------------- | :------------------------- | :--------------------------- |
         | **数据位置**      | 附加在URL之后(?name=value) | 包含在HTTP请求体中           |
         | **可见性**        | 在浏览器地址栏可见         | 不可见                       |
         | **安全性**        | 较低（历史记录可查）       | 较高                         |
         | **数据长度限制**  | 有限制（约2048字符）       | 无限制                       |
         | **缓存**          | 可被缓存                   | 不会被缓存                   |
         | **后退/刷新行为** | 无害                       | 会重新提交数据               |
         | **书签**          | 可收藏为书签               | 不可收藏                     |
         | **幂等性**        | 幂等（多次执行结果相同）   | 非幂等                       |
         | **典型用途**      | 获取数据（搜索、筛选）     | 提交数据（登录、注册、修改） |
       
         ## 4. GET 方法详解
       
         ### 特点：
       
         - 表单数据附加在URL后，格式为：`?name1=value1&name2=value2`
         - 适合不敏感的小量数据传输
         - 可以被书签保存
       
         ### 示例：
       
         ```html
         <form action="/search" method="get">
           搜索词: <input type="text" name="q">
           <input type="submit" value="搜索">
         </form>
         ```
       
         提交后URL变为：`/search?q=用户输入的词`
       
         ### 适用场景：
       
         1. 搜索引擎查询
         2. 商品筛选过滤
         3. 分页导航
         4. 数据查询操作
       
         ## 5. POST 方法详解
       
         ### 特点：
       
         - 数据包含在HTTP请求体中
         - 适合传输敏感信息或大量数据
         - 支持文件上传
       
         ### 示例：
       
         ```html
         <form action="/register" method="post">
           用户名: <input type="text" name="username">
           密码: <input type="password" name="password">
           <input type="submit" value="注册">
         </form>
         ```
  
  2. javabean标签的使用
  
     ### 1. 定义JavaBean
  
     ```java
     // User.java
     package com.example;
     
     public class User implements Serializable {
         private String username;
         private int age;
         
         // 必须有无参构造
         public User() {}
         
         // getter和setter
         public String getUsername() { return username; }
         public void setUsername(String username) { this.username = username; }
         
         public int getAge() { return age; }
         public void setAge(int age) { this.age = age; }
     }
     ```
  
     ### 2. 在JSP中使用
  
     ```jsp
     <%@ page contentType="text/html;charset=UTF-8" %>
     <html>
     <head>
         <title>JavaBean示例</title>
     </head>
     <body>
     
     <!-- 1. 创建Bean -->
     <jsp:useBean id="user" class="com.example.User" scope="session"/>
     
     <!-- 2. 设置属性 -->
     <jsp:setProperty name="user" property="username" value="李四"/>
     <jsp:setProperty name="user" property="age" value="25"/>
     
     <!-- 3. 获取属性 -->
     <h2>用户信息：</h2>
     <p>姓名：<jsp:getProperty name="user" property="username"/></p>
     <p>年龄：<jsp:getProperty name="user" property="age"/></p>
     
     <!-- 4. 自动匹配表单参数 -->
     <form action="" method="post">
         用户名：<input type="text" name="username"><br>
         年龄：<input type="number" name="age"><br>
         <input type="submit" value="更新">
     </form>
     
     <jsp:setProperty name="user" property="*"/>
     
     </body>
     </html>
     ```
  
     ## 四、作用域管理
  
     JavaBean可以在不同作用域中共享：
  
     | 作用域      | 描述                     | 访问方式                            |
     | :---------- | :----------------------- | :---------------------------------- |
     | page        | 当前页面有效（默认）     | pageContext.getAttribute()          |
     | request     | 同一次请求有效（含转发） | request.getAttribute()              |
     | session     | 同一用户会话有效         | request.getSession().getAttribute() |
     | application | 整个应用有效             | application.getAttribute()          |
  
     ## 五、实际应用场景
  
     1. **用户登录信息存储**
  
     ```jsp
     <jsp:useBean id="loginUser" class="com.model.User" scope="session"/>
     <jsp:setProperty name="loginUser" property="*"/>
     ```
  
     1. **表单数据自动封装**
  
     ```jsp
     <!-- 表单字段名与Bean属性名匹配 -->
     <jsp:useBean id="formData" class="com.model.FormBean"/>
     <jsp:setProperty name="formData" property="*"/>
     ```
  
     1. **配置信息共享**
  
     ```jsp
     <jsp:useBean id="config" class="com.util.AppConfig" scope="application"/>
     ```
  
  3. jsp 获取客户端请求参数的内置对象
  
  4. ###  request 对象简介
  
     - 类型：`javax.servlet.http.HttpServletRequest`
     - 作用：封装了客户端的所有请求信息
     - 生命周期：一次请求期间有效（包括forward转发）
  
     ### 2. 主要方法
  
     #### (1) 获取单个参数值
  
     ```jsp
     String value = request.getParameter("参数名");
     ```
  
     示例：
  
     ```jsp
     <%
         String username = request.getParameter("username");
         String password = request.getParameter("password");
     %>
     ```
  
     #### (2) 获取多个同名参数值（如复选框）
  
     ```jsp
     String[] values = request.getParameterValues("参数名");
     ```
  
     示例：
  
     ```jsp
     <%
         String[] hobbies = request.getParameterValues("hobby");
         if(hobbies != null) {
             for(String hobby : hobbies) {
                 out.print(hobby + "<br>");
             }
         }
     %>
     ```
  
     #### (3) 获取所有参数名
  
     ```jsp
     Enumeration<String> paramNames = request.getParameterNames();
     ```
  
     示例：
  
     
  
     ```jsp
     <%
         Enumeration<String> names = request.getParameterNames();
         while(names.hasMoreElements()) {
             String name = names.nextElement();
             out.print(name + "=" + request.getParameter(name) + "<br>");
         }
     %>
     ```
  
     #### (4) 获取参数Map
  
     ```jsp
     Map<String, String[]> paramMap = request.getParameterMap();
     ```
  
  5. jdbc里边用来执行简单不带参的SQL语句的接口
     - 不带参数（Statement）
  
       ### 1. Statement 接口特点
  
       - 用于执行**静态 SQL 语句**（不包含参数）
       - 直接拼接 SQL 字符串，**有 SQL 注入风险**
       - 适合执行 DDL 语句或简单的查询
  
       ### 2. 主要方法
  
       | 方法                                 | 描述                           |
       | :----------------------------------- | :----------------------------- |
       | `ResultSet executeQuery(String sql)` | 执行查询语句，返回结果集       |
       | `int executeUpdate(String sql)`      | 执行增删改语句，返回受影响行数 |
       | `boolean execute(String sql)`        | 执行任意SQL，返回是否有结果集  |
  
       ### 3. 使用示例
  
       ```java
       // 1. 创建Statement对象
       Statement stmt = connection.createStatement();
       
       // 2. 执行查询
       ResultSet rs = stmt.executeQuery("SELECT * FROM products");
       
       // 3. 执行更新
       int rows = stmt.executeUpdate(
           "UPDATE users SET status=1 WHERE id=1001");
       
       // 4. 执行DDL
       stmt.execute("CREATE TABLE temp(id INT)");
       
       // 5. 关闭资源
       rs.close();
       stmt.close();
       ```
  
       ### 4. 优缺点
  
       **优点**：
  
       - 使用简单
       - 适合执行一次性SQL
  
       **缺点**：
  
       - SQL注入风险高
       - 性能较低（每次执行都需编译）
  
     - 带参数（PreparedStatement）
  
     - ### 1. PreparedStatement 特点
  
       - 继承自 Statement 接口
       - 使用**预编译**机制，**防止 SQL 注入**
       - 支持参数化查询（使用 `?` 占位符）
       - 性能更高（SQL预编译一次，多次执行）
  
       ### 2. 主要方法
  
       | 方法                                         | 描述                            |
       | :------------------------------------------- | :------------------------------ |
       | `void setXxx(int parameterIndex, Xxx value)` | 设置参数值（Xxx为各种数据类型） |
       | `ResultSet executeQuery()`                   | 执行查询（无需SQL参数）         |
       | `int executeUpdate()`                        | 执行更新（无需SQL参数）         |
       | `void addBatch()`                            | 添加到批处理                    |
       | `int[] executeBatch()`                       | 执行批处理                      |
  
       ### 3. 使用示例
  
       ```java
       // 1. 创建PreparedStatement（带?占位符）
       PreparedStatement pstmt = connection.prepareStatement(
           "SELECT * FROM users WHERE username=? AND password=?");
       
       // 2. 设置参数（索引从1开始）
       pstmt.setString(1, "admin");
       pstmt.setString(2, "123456");
       
       // 3. 执行查询
       ResultSet rs = pstmt.executeQuery();
       
       // 4. 批处理示例
       pstmt = connection.prepareStatement("INSERT INTO logs(message) VALUES(?)");
       pstmt.setString(1, "Log entry 1");
       pstmt.addBatch();
       
       pstmt.setString(1, "Log entry 2");
       pstmt.addBatch();
       
       int[] counts = pstmt.executeBatch();
       
       // 5. 关闭资源
       rs.close();
       pstmt.close();
       ```
  
       ### 4. 参数类型设置方法
  
       | 方法                           | 对应SQL类型   |
       | :----------------------------- | :------------ |
       | `setString(int, String)`       | VARCHAR, CHAR |
       | `setInt(int, int)`             | INTEGER       |
       | `setDouble(int, double)`       | DOUBLE        |
       | `setDate(int, Date)`           | DATE          |
       | `setTimestamp(int, Timestamp)` | TIMESTAMP     |
       | `setBoolean(int, boolean)`     | BOOLEAN       |
       | `setNull(int, int)`            | 设置NULL      |
  
       ### 5. 优缺点
  
       **优点**：
  
       - 防止SQL注入
       - 性能更高
       - 代码可读性好
       - 支持批处理
  
       **缺点**：
  
       - 编写稍复杂
       - 不适合动态表名/列名的情况
  
       **Statement vs PreparedStatement 对比**
  
       | 特性         | Statement                        | PreparedStatement                                |
       | :----------- | :------------------------------- | :----------------------------------------------- |
       | **参数支持** | 不支持                           | 支持(?占位符)                                    |
       | **SQL注入**  | 易受攻击                         | 防止注入                                         |
       | **性能**     | 每次执行都编译                   | 预编译，高效                                     |
       | **适用场景** | 简单查询、DDL                    | 参数化查询、用户输入                             |
       | **批处理**   | 支持但效率低                     | 高效批处理                                       |
       | **代码示例** | `stmt.executeQuery("SELECT...")` | `pstmt.setString(1,value); pstmt.executeQuery()` |
  
  6. Servlet生命周期：
     - ### 1. 初始化阶段 - init() 方法
  
       **执行时机**：
  
       - Servlet 容器（如 Tomcat）第一次加载 Servlet 时调用
       - 只执行一次
  
       **主要用途**：
  
       - 加载资源（数据库连接、配置文件等）
       - 初始化参数
  
       **示例**：
  
       ```java
       public class MyServlet extends HttpServlet {
           private DatabaseConnection dbConnection;
           
           @Override
           public void init() throws ServletException {
               // 初始化数据库连接
               dbConnection = new DatabaseConnection();
               dbConnection.connect();
               
               // 获取初始化参数（web.xml中配置的）
               String config = getInitParameter("configFile");
               System.out.println("Servlet初始化完成，配置文件：" + config);
           }
       }
       ```
  
       ### 2. 处理请求阶段 - service() 方法
  
       **执行时机**：
  
       - 每次客户端请求时调用（执行多次）
       - 根据请求类型调用 doGet() 或 doPost()
  
       **主要用途**：
  
       - 处理客户端请求
       - 生成响应
  
       **示例**：
  
       ```java
       public class MyServlet extends HttpServlet {
           protected void doGet(HttpServletRequest request, HttpServletResponse response) 
                   throws ServletException, IOException {
               
               response.setContentType("text/html");
               PrintWriter out = response.getWriter();
               out.println("<h1>处理GET请求</h1>");
               
               // 使用初始化阶段创建的数据库连接
               List<User> users = dbConnection.getUsers();
               // ...处理数据
           }
           
           protected void doPost(HttpServletRequest request, HttpServletResponse response) 
                   throws ServletException, IOException {
               
               String username = request.getParameter("username");
               // 处理表单提交...
               response.sendRedirect("/success.jsp");
           }
       }
       ```
  
       ### 3. 销毁阶段 - destroy() 方法
  
       **执行时机**：
  
       - Servlet 容器关闭或 Servlet 被移除时调用
       - 只执行一次
  
       **主要用途**：
  
       - 释放资源（关闭数据库连接等）
       - 保存状态信息
  
       **示例**：
  
       ```java
       public class MyServlet extends HttpServlet {
           @Override
           public void destroy() {
               // 关闭数据库连接
               if(dbConnection != null) {
                   dbConnection.close();
                   System.out.println("释放数据库连接");
               }
               
               // 保存日志信息等
               saveAccessLog();
           }
       }
       ```
  
       ### 计数器 Servlet(完整例子)
  
       ```java
       @WebServlet("/counter")
       public class CounterServlet extends HttpServlet {
           private int visitCount;
           
           @Override
           public void init() {
               visitCount = 0;
               System.out.println("计数器Servlet初始化");
           }
           
           @Override
           protected void doGet(HttpServletRequest request, HttpServletResponse response) 
                   throws IOException {
               
               visitCount++;
               response.setContentType("text/html");
               PrintWriter out = response.getWriter();
               out.println("<h2>访问次数: " + visitCount + "</h2>");
           }
           
           @Override
           public void destroy() {
               System.out.println("最终访问次数: " + visitCount);
               System.out.println("Servlet销毁");
           }
       }
       ```
  
  7. 作用域问题：
  
     - page、request、session、application
  
     - page、request、session、application各自用于共享数据的情况(哪个用于在多个用户之间共享数据)
  
     - page是给当前页面有效，request和session是一个用户一个，application是所有用户共用一个。
  
       ## 四大作用域对比
  
       | 作用域          | 对应的JSP对象 | 实现类                                  | 生命周期                             | 典型应用场景 |
       | :-------------- | :------------ | :-------------------------------------- | :----------------------------------- | :----------- |
       | **page**        | `pageContext` | `javax.servlet.jsp.PageContext`         | 当前页面执行期间                     | 页面临时变量 |
       | **request**     | `request`     | `javax.servlet.http.HttpServletRequest` | 同一次请求期间（包括forward）        | 请求参数传递 |
       | **session**     | `session`     | `javax.servlet.http.HttpSession`        | 用户会话期间（默认30分钟不活动失效） | 用户登录状态 |
       | **application** | `application` | `javax.servlet.ServletContext`          | 整个Web应用运行期间                  | 全局配置信息 |
  
       ## 二、各作用域详细说明
  
       ### 1. page 作用域
  
       **特点**：
  
       - 仅在当前 JSP 页面内有效
       - 页面刷新或跳转后数据丢失
       - 通过 `pageContext` 对象存取
  
       **示例代码**：
  
       ```jsp
       <%-- 设置page范围属性 --%>
       <%
           pageContext.setAttribute("pageVar", "临时数据", PageContext.PAGE_SCOPE);
           // 等效简写
           pageContext.setAttribute("pageVar", "临时数据");
       %>
       
       <%-- 获取page范围属性 --%>
       <p>Page变量值：<%= pageContext.getAttribute("pageVar") %></p>
       ```
  
       ### 2. request 作用域
  
       **特点**：
  
       - 在同一次请求周期内有效
       - 包括通过 `forward` 跳转的页面
       - 通过 `request` 对象存取
  
       **示例代码**：
  
       ```jsp
       <%-- 设置request属性 --%>
       <%
           request.setAttribute("reqVar", "请求数据");
       %>
       
       <%-- 转发到另一个JSP --%>
       <jsp:forward page="receiveRequest.jsp"/>
       ```
  
       在 `receiveRequest.jsp` 中：
  
       ```jsp
       <p>Request变量值：<%= request.getAttribute("reqVar") %></p>
       ```
  
       ### 3. session 作用域
  
       **特点**：
  
       - 在同一用户会话期间有效
       - 默认30分钟不活动后失效
       - 可跨多个请求
       - 通过 `session` 对象存取
  
       **示例代码**：
  
       ```jsp
       <%-- 设置session属性 --%>
       <%
           session.setAttribute("user", "张三");
       %>
       
       <%-- 在其他页面获取 --%>
       <p>当前用户：<%= session.getAttribute("user") %></p>
       
       <%-- 手动销毁session --%>
       <%
           session.invalidate();
       %>
       ```
  
       ### 4. application 作用域
  
       **特点**：
  
       - 整个Web应用范围内有效
       - 所有用户共享同一份数据
       - 服务器关闭或应用卸载时销毁
       - 通过 `application` 对象存取
  
       **示例代码**：
  
       ```jsp
       <%-- 设置application属性 --%>
       <%
           application.setAttribute("visitCount", 0);
       %>
       
       <%-- 访问计数器示例 --%>
       <%
           Integer count = (Integer) application.getAttribute("visitCount");
           application.setAttribute("visitCount", count + 1);
       %>
       <p>网站总访问量：<%= application.getAttribute("visitCount") %></p>
       ```
  
  8. web.xml配置（Web配置错误页面（使用范围）用什么标签）
     - 在这里面我们通常配置一些初始化参数，servlet过滤器、监听器，还有错误页面，那么我们如何在web.xml里面配置错误页面，使用哪个标签，就是说在web.xml里面用哪个标签来配置错误页面，比如说我们客户，我们用户从服务器的访问一个资源存在，那一般可以报错吧，然后我想把某一个页面，就把这一面更改成其他一面，那么这时候用哪个标签啊，这个大家要知道。
  
     - 错误页面：<error-page>
  
     - 初始化参数：<context-param>
  
       在 web.xml 文件中，使用 `<error-page>` 标签来配置错误页面，它允许开发者自定义当特定错误发生时显示给用户的页面。
  
       ## 一、基本配置语法
  
       ```xml
       <error-page>
           <error-code>错误代码</error-code>
           <exception-type>异常类型</exception-type>
           <location>错误处理页面路径</location>
       </error-page>
       ```
  
       ## 二、三种配置方式
  
       ### 1. 按 HTTP 错误代码配置
  
       ```xml
       <error-page>
           <error-code>404</error-code>
           <location>/error/404.html</location>
       </error-page>
       
       <error-page>
           <error-code>500</error-code>
           <location>/error/500.jsp</location>
       </error-page>
       ```
  
       ### 2. 按 Java 异常类型配置
  
       ```xml
       <error-page>
           <exception-type>java.lang.NullPointerException</exception-type>
           <location>/error/null.jsp</location>
       </error-page>
       
       <error-page>
           <exception-type>java.lang.Exception</exception-type>
           <location>/error/general.jsp</location>
       </error-page>
       ```
  
       ### 3. 默认错误页面配置
  
       ```xml
       <error-page>
           <location>/error/default.jsp</location>
       </error-page>
       ```
  
       ## 三、完整配置示例
  
       ```xml
       <?xml version="1.0" encoding="UTF-8"?>
       <web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
                xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
                xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee 
                                    http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
                version="4.0">
           
           <!-- 配置404错误页面 -->
           <error-page>
               <error-code>404</error-code>
               <location>/error/notFound.jsp</location>
           </error-page>
           
           <!-- 配置500错误页面 -->
           <error-page>
               <error-code>500</error-code>
               <location>/error/serverError.jsp</location>
           </error-page>
           
           <!-- 配置特定异常的处理页面 -->
           <error-page>
               <exception-type>java.sql.SQLException</exception-type>
               <location>/error/databaseError.jsp</location>
           </error-page>
           
           <!-- 默认错误页面 -->
           <error-page>
               <location>/error/defaultError.jsp</location>
           </error-page>
           
       </web-app>
       ```
  
       ## 四、错误页面中的可用对象
  
       在错误处理JSP页面中，可以通过以下对象获取错误信息：
  
       jsp
  
       
  
       复制
  
       
  
       下载
  
       ```
       <%@ page isErrorPage="true" %>
       <html>
       <head>
           <title>错误页面</title>
       </head>
       <body>
           <h2>错误信息</h2>
           <p>状态码：${pageContext.errorData.statusCode}</p>
           <p>请求URI：${pageContext.errorData.requestURI}</p>
           <p>异常：${pageContext.exception.message}</p>
           
           <%-- 如果是JSP页面，需要设置isErrorPage="true"才能访问exception对象 --%>
           <% if(exception != null) { %>
               <p>堆栈跟踪：<% exception.printStackTrace(new java.io.PrintWriter(out)); %></p>
           <% } %>
       </body>
       </html>
       ```
  
  9. Servlet生命周期中：
     - Init、destroy方法执行一次
     - service方法执行多次
  
  10. jdbc常用的一些类及其用途
  
     **实际对应的JDBC核心接口及用途**
  
     1. **`Statement`**
  
        - **作用**：执行**静态SQL语句**（不带参数）
  
        - **典型用途**：
  
          ```java
          // 1. 创建 Statement 对象
          Statement stmt = connection.createStatement();
          
          // 2. 执行不带参数的 SQL（如查询）
          String sql = "SELECT * FROM users";
          ResultSet rs = stmt.executeQuery(sql);
          
          // 3. 执行更新操作（INSERT/UPDATE/DELETE）
          int rowsAffected = stmt.executeUpdate("DELETE FROM users WHERE id = 1");
          
          // 4. 释放资源
          rs.close();
          stmt.close();
          ```
  
     2. **`PreparedStatement`**（可能被误识别为"PastSendLay"）
  
        - **作用**：执行**带参数的SQL语句**（防SQL注入）
  
        - **典型用途**：
  
          ```java
          PreparedStatement pstmt = conn.prepareStatement("INSERT INTO users VALUES(?,?)");
          pstmt.setInt(1, 101);//设置参数
          pstmt.setString(2, "张三");
          pstmt.executeUpdate();
          ```
  
     3. **`CallableStatement`**
  
        - **作用**：调用数据库**存储过程**
  
        - **典型用途**：
  
          ```java
          CallableStatement cstmt = conn.prepareCall("{call get_user_info(?)}");
          cstmt.setInt(1, 1001);
          cstmt.execute();
          ```
  
     4. **`ResultSet`**
  
        - **作用**：处理SQL查询返回的**结果集**
  
        - **典型用途**：
  
          ```java
          while(rs.next()){
              System.out.println(rs.getString("username"));
          }
          ```
  
  ## 判断题（10×1）
  
  1. for each语句
  
  2. jsp标记
  
  3. **MVC架构对比**
  
     - **Model1**：JSP+JavaBean（高耦合）
     - **Model2**：MVC分层（推荐）
  
     - model和model2各自优缺点
  
  4. servlet过滤器中的doFilter()方法
  
  5. session中的invalidate()方法
  
  6. request中的getRemoteHost()方法
  
  ## 填空题（8×3）
  
  1. HTTP请求方法功能：
     - GET：获取服务器信息，作为响应返回
     - POST/PUSH：用于客户端向服务器提交数据
  2. 运行程序类型：
     - CS、BS
     - Client server、browser server
  3. **Ajax核心**
     - 对象：`XMLHttpRequest`
     - 特点：异步无刷新通信
  4. URL（统一资源定位器）定义
  5. 配置命令中language的默认值
  6. **使用cookie基本步骤**
     - 创建cookie对象
     - 传送cookie对象
     - 读取cookie对象
     - 设置对象有效时间
  7. JavaBean：
     - 定义与功能
     - 实现结果与分类使用（将原来页面程序片段封装到javabean当中能够实现业务逻辑层与视图层的分离）
  
  ## 简答题（3×6）
  
  1. JSP：
     - 定义
     - 执行过程
  2. Servlet生命周期：
     - 初始化
     - 处理请求
     - 服务结果等
  3. MVC：
     - 基本概念
     - 基本原理
     - 优缺点
  
  ## 编程题 (1×20)
  
  1. 实现简单网页计算器（需补充代码，只需要补充js部分）：
     - 使用application对象