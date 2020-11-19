```jsp
定义全局变量、方法
<%!
	public String bookName = "Java从入门到入土";
	public void init() {
		System.out.println(bookName);
	}
%>
局部变量、Java语句
<%
	String name = "张三";
	out.println() 不能回车换行
	out.println("<h1>Hello, World</h1>");
	init();
%>
输出表达是
<%=
	"Hello" + name
%>
```

```jsp
网页开头这个叫做指令
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
page指定的属性
language：jsp页面使用的脚本语言
import：导入类/包
pageEncoding：jsp文件自身编码  jsp -> java用的编码
contentType：浏览器解析jsp的编码
```

```
jsp内置对象
out：输出对象，向客户端输出内容
request：请求对象，存储“客户端向服务端请求信息”
  常见方法
  	String getParameter(String name) : 根据请求的字段名key，返回字段值value，根据标签的name属性值拿value值
  	String[] getParameterValues(String name) : 根据请求的字段名key，返回多个字段值values (checkbox)
  	void setCharacterEncoding("编码格式utf-8") : 设置请求编码
  	getRequestDispatcher(b).forward() : 请求转发的方式跳转页面 A -> B
  	servletContext getServerContext() : 获取项目的servletContext对象
reponse：响应对象
  提供的方法：
	void addCookie(Cookie cookie) 服务端向客户端增加cookie对象
    void sendRedirect(String location) throws IOException; 重定向
    void setContentType(String type) 设置服务端响应编码
pageContext
session
config
page
exception
```

