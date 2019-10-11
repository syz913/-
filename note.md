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
