ServletConfig 

servlet 的这个init 方法被调用的时候，容器会传入一个 ServletConfig的 参数进来，
这个参数就是我们在web.xml里对这个servlet的定义。

这个  ServletConfig对象里有个对象是 ServletContext 
ServletContext 表示这个应用本身，就是当下web应用， 在ServletContext存放的数据，servlet 之间是可以共享的



ServletContext 源代码的类解释如下：


  Defines a set of methods that a servlet uses to communicate with its
  servlet container, for example, to get the MIME type of a file,
  dispatch requests, or write to a log file.
  
  ServletContext 即是，各个servlet 用来获取当前所处容器的信息例如，写日志的路径的一个桥梁，也是各个sevlet之间相互沟通
  的一个桥梁。
 
  <p>There is one context per "web application" per Java Virtual Machine.  (A
  "web application" is a collection of servlets and content installed under a
  specific subset of the server's URL namespace such as <code>/catalog</code>
  and possibly installed via a <code>.war</code> file.)
  
  所谓的java web 应用，其本质就是一堆servlet的集合，通过一个容器把这些servlet都管理起来。
  
  
 
  <p>In the case of a web
  application marked "distributed" in its deployment descriptor, there will
  be one context instance for each virtual machine.  In this situation, the
  context cannot be used as a location to share global information (because
  the information won't be truly global).  Use an external resource like
  a database instead.
 
  <p>The <code>ServletContext</code> object is contained within
  the {@link ServletConfig} object, which the Web server provides the
  servlet when the servlet is initialized.
 
 根据这些资料的描绘，我大致可以这么理解ServletContext 就是tomcat 里的Contain 容器本身，就是指servlet容器本身。
 
 同样在 spring中也会有 ApplicationContext, WebApplicationContext 这样的概念，类推，其实这些context,指的也是
 容器本身，只是各自指的容器不一样。
 
 其余资料的描述
 
 ApplicationContext applicationContext.xml是每个Web应用程序的根上下文配置。 
 Spring加载applicationContext.xml文件，并为整个应用程序创建ApplicationContext。 
 每个Web应用程序将只有一个应用程序上下文。 
 如果您没有使用contextConfigLocation参数在web.xml中显式声明上下文配置文件名，
 Spring将在WEB-INF文件夹下搜索applicationContext.xml，如果找不到该文件，则抛出FileNotFoundException。
 
 WebApplicationContext除了ApplicationContext，单个Web应用程序中可以有多个WebApplicationContext。 
 简单来说，每个DispatcherServlet与单个WebApplicationContext关联。 xxx-servlet.xml文件特定于DispatcherServlet，
 Web应用程序可以配置多个DispatcherServlet来处理请求。 
 在这样的场景中，每个DispatcherServlet将配置一个单独的xxx-servlet.xml。 
 但是，applicationContext.xml对于所有的servlet配置文件将是常见的。 
 Spring将默认从webapps WEB-INF文件夹中加载名为“xxx-servlet.xml”的文件，其中xxx是web.xml中的servlet名称。 
 如果要更改该文件名的名称或更改位置，请使用contextConfigLocation作为参数名称添加启动参数。
 
 
 
 也就是说，一个spring应用中，只有一个springcontext , 但是可以有多个webapplicationcontext