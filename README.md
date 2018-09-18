file:///D:/1/Spring+MVC%252BMYBatis%E4%BC%81%E4%B8%9A%E5%BA%94%E7%94%A8%E5%AE%9E%E6%88%98%2540www.java1234.com.pdf

报表平台注册码：5f532249-eecf53c84-33bb-cc0729e6ab43

<%@ page trimDirectiveWhitespaces="true" %>
这个命令可以使jsp输出的html时去除多余的空行（jsp上使用EL和tag会产生大量的空格和空行）。
但是这个命令是从JSP2.1规范以后才得到支持。
所以在tomcat 6.0之前的版本上如果使用这个命令就会抛出异常：
Page directive has invalid attribute: trimDirectiveWhitespaces
解决方法是：
1.升级tomcat至6.0以上版本
2.Tomcat 5.5.x+，不要使用trimDirectiveWhitespaces，改用这种方法：
在Tomcat安装目录/conf/web.xml中找到名叫"jsp"的servlet，添加下面一段代码：
<init-param>
       <param-name>trimSpaces</param-name>
       <param-value>true</param-value>
</init-param>
查看JSP版本可以使用下面的命令：
JSP version: <%= JspFactory.getDefaultFactory().getEngineInfo().getSpecificationVersion() %>


request.getcontextPath() 详解
文章分类:Java编程
<%=request.getContextPath()%>是为了解决相对路径的问题，可返回站点的根路径。
但不用也可以，比如<a href="<%=request.getContextPath()%>/catalog.jsp">，可以直接用<a href="catalog.jsp">也行，这两个文件是在同一个目录下的。比如你要生成一个文件放在服务器上得一个目录下,可以使用request.getContextPath()+/dir,组成一个完整得目录结构!
但在JSP文件里,有时通过request.getContextPath()得到的路径却为空,为什么? 
context中没有配置path属性，所以你的工程文件就是在根目录下，相当于path="";
即是你直接在浏览器中输入你的服务器ip就会到你的jsp页面，而不是tomcat的默认页面；所以你通过request.getContextPath()得到的字符串是为空的；它是获得虚目录的；
如果你想得到工程文件的实际物理路径，可通过：<%=request.getRealPath("/")%>，这样页面就会输出：d:/web。
参考servlet中的接口：
request.getScheme();
返回的协议名称,默认是http
request.getServerName()
返回的是你浏览器中显示的主机名，你自己试一下就知道了
getServerPort()
获取服务器端口号
request.getContextPath()应该是得到项目的名字，如果项目为根目录，则得到一个""，即空的字条串。如果项目为abc, <%=request.getContextPath()% > 将得到abc，服务器端的路径则会自动加上，<a href="XXXX.jsp"> 是指当前路径下的这个xxx.jsp页面，有时候也可以在head里设置html:base来解决路径的问题，不过用的最多的还是request.getContextPath。
在js文件中得到request.getContextPath()的值，不想在JSP中写太多的Javascript代码：
一种方法是用hidden:
<input type=hidden name=contextPath value=<%= request.getContextPath()>
 
再就是在本页面的js里面也是可以使用Scriptlet来赋值的：
var a = '<%= request.getContextPath()>'
或者你赋值给一个hidden的控件都是可以的，然后js取，这样js可以不用写在jsp里。
实际应用中，一般用来解决jsp测试和生产环境路径不同的问题： 
<%
 String appContext = request.getContextPath();
 String basePath = request.getScheme()+"://"+request.getServerName()+":"+ request.getServerPort() + appContext; 
%>



jquery对象.load(url,params,function(数据){});
$.get(url,params,function(参数){},type);
发送get请求的ajax
url:请求的路径
params:请求的参数 参数为key\value的形式 key=value {"":"","":""}
fn:回调函数 参数就是服务器发送回来的数据
type:返回内容格式，xml, html, script, json, text, _default。 以后用"json"

$.post(url,params,function(数据){},type);
发送post请求的ajax

若结果为json格式, 打印返回值的时候是一个对象 
例如若json为 {"result":"success","msg":"成功"}
获取msg 只需要	参数.msg

$.ajax([选项]);
选项的可选值:
url:请求路径
type:请求方法
data:发送到服务器的数据
success:fn 成功以后的回调
error:fn 异常之后的回调
dataType:返回内容格式 经常使用json
async:设置是否是异步请求
例如:
$.ajax({
url:"<%=basePath%>customer/detail.action",
type:"get",

data:{"id":1},

success:function(data) {

$("#edit_cust_id").val(data.cust_id);
$("#edit_customerName").val(data.cust_name);
$("#edit_customerFrom").val(data.cust_source)
$("#edit_custIndustry").val(data.cust_industry)
$("#edit_custLevel").val(data.cust_level)
$("#edit_linkMan").val(data.cust_linkman);
$("#edit_phone").val(data.cust_phone);
$("#edit_mobile").val(data.cust_mobile);
$("#edit_zipcode").val(data.cust_zipcode);
$("#edit_address").val(data.cust_address);
}

error:function(){},
dataType:"json"

});



3.1、需要的Jar包

　　①Spring：

　　　　spring-aop-4.3.0.RELEASE.jar
　　　　spring-aspects-4.3.0.RELEASE.jar
　　　　spring-beans-4.3.0.RELEASE.jar
　　　　spring-context-4.3.0.RELEASE.jar
　　　　spring-context-support-4.3.0.RELEASE.jar
　　　　spring-core-4.3.0.RELEASE.jar
　　　　spring-expression-4.3.0.RELEASE.jar
　　　　spring-jdbc-4.3.0.RELEASE.jar
　　　　spring-tx-4.3.0.RELEASE.jar
　　　　spring-web-4.3.0.RELEASE.jar
　　　　spring-webmvc-4.3.0.RELEASE.jar

　　　　spring-webmvc-portlet-4.3.0.RELEASE.jar
　　　　spring-websocket-4.3.0.RELEASE.jar

　　　　com.springsource.net.sf.cglib-2.2.0.jar
　　　　com.springsource.org.aopalliance-1.0.0.jar
　　　　com.springsource.org.aspectj.weaver-1.6.8.RELEASE.jar
　　　　commons-logging-1.2.jar

　　③MyBatis：

　　　　mybatis-3.1.1.jar

　　　　log4j-1.2.16.jar
　　　　mybatis-spring-1.2.1.jar

　　④文件上传/下载：

　　　　commons-fileupload-1.2.2.jar
　　　　commons-io-2.4.jar

　　⑤C3P0数据源：

　　　　c3p0-0.9.5.1.jar

　　　　mchange-commons-java-0.2.10.jar

　　　　classmate-0.8.0.jar

　　⑥MySQL：

　　　　mysql-connector-java-5.0.8-bin.jar

　　⑦JSTL：

　　　　taglibs-standard-compat-1.2.5.jar
　　　　taglibs-standard-impl-1.2.5.jar
　　　　taglibs-standard-jstlel-1.2.5.jar
　　　　taglibs-standard-spec-1.2.5.jar

　　⑧JSON：

　　　　jackson-annotations-2.6.0.jar
　　　　jackson-core-2.6.0.jar
　　　　jackson-databind-2.6.0.jar

　　⑨Hibernate Validate：

　　　　hibernate-validator-4.3.0.Final.jar

　　　　validation-api-1.0.0.GA.jar
　　　　validation-api-1.1.0.CR1.jar

　　　　jboss-logging-3.1.0.CR2.jar
　　　　jboss-logging-3.1.1.GA.jar


 http://mvnrepository.com/ 
C:\Users\cunqing.wei\AppData\Roaming\npm    cli脚手架地址

E:\Python\Python36;
E:\Python\Python36\Scripts\;E:\Python\Python36\;
