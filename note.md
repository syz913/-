### 目录

- [HTTP的持续连接和非持续连接](#HTTP的持续连接和非持续连接)
  - [非持续连接](#HTTP1.0采用非持续(Non-persistent)连接方式：)
  - [持续连接](#HTTP 1.1 引入持续(persistent)连接方式)
- [TCP连接中的ACK和seq](#TCP连接中的ACK和seq)

### HTTP的持续连接和非持续连接
#### HTTP1.0采用非持续(Non-persistent)连接方式： 
 新建一个TCP连接需要RTT，然后每次HTTP请求需要1RTT，如果有N个内嵌对象，先请求HTML，再请求N个对象
 响应时间为: (N+1)*2RTT + 传输时间 
 
 <img src="https://img-blog.csdn.net/20180626120814323?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3did2FuZzE5OTg=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70" width="80%">
 
#### HTTP 1.1 引入持续(persistent)连接方式 
> 在收到HTTP响应时暂时不关闭TCP连接，而是等待一段时间 

由于不需要每次新建TCP连接，所以需要的时间为RTT + (N+1)RTT = (N+2)RTT

非流水线方式的持续连接： 
  . 发送第一个请求，收到第一个响应 
  . 发送第二个请求，收到第二个响应…. 
  
流水线方式(pipelining)的持续连接 
  . 发送第一个请求，收到第一个响应(HTML页面) 
  . 发送第2、3、4...个HTTP请求，收到第2、3、4...个HTTP响应 
  . 要求HTTP响应自身能够决定边界（即结束的位置） 
  . Head of line blocking: 按照请求的顺序发送HTTP响应，如果一个对象较大，阻塞后面的对象 
  . 如果中间通过代理服务器，会有实现不兼容的问题 
  . 绝大部分浏览器缺省关闭流水线方式
  
<img src="https://img-blog.csdn.net/20180626120740145?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3did2FuZzE5OTg=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70" width="80%">
流水线方式第一个请求2RTT，然后发送所有请求，如果所有响应可以容纳在TCP段中 3RTT + 传输时间

#### get post
application/x-www-form-urlencoded:表单数据
传输表单数据时，
GET请求的数据会附在URL之后（就是把数据放置在HTTP协议头中），以?分割URL和传输数据，参数之间以&相连，如：login.action?name=hyddd&password=idontknow&verify=%E4%BD%A0%E5%A5%BD。如果数据是英文字母/数字，原样发送，如果是空格，转换为+，如果是中文/其他字符，则直接把字符串用BASE64加密，得出如：%E4%BD%A0%E5%A5%BD，其中％XX中的XX为该符号以16进制表示的ASCII。
#### URI URL
> URI = URL+URN

URI，是统一资源标识符，用来唯一的标识一个资源。而URL是统一资源定位器，它是一种具体的URI，即URL可以用来标识一个资源，而且还指明了如何locate这个资源。而URN，统一资源命名，是通过名字来标识资源，比如mailto:java-net@java.sun.com。也就是说，URI是以一种抽象的，高层次概念定义统一资源标识，而URL和URN则是具体的资源标识的方式。URL和URN都是一种URI；

URL一般由三部组成:
①协议(或称为服务方式)
②存有该资源的主机IP地址(有时也包括端口号)
③主机资源的具体地址。如目录和文件名等

URI一般由三部组成:
①访问资源的命名机制
②存放资源的主机名
③资源自身的名称，由路径表示，着重强调于资源。

### TCP连接中的ACK和seq

