title: 计算机网络入门
date: 2019-11-29 18:00:00
desc: 
tags: [network] 
index_img: https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/network/network_1_title.jpg
banner_img: https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/network/network_1_title.jpg
---

网络构建成了社会，计算机网络也只是其中一个。

计算机网络对于计算机的发展起到了相当关键的作用。

但是从现有的计算机科学整体角度来看，计算机网络的出现会不会是历史必然呢？

<!-- more -->

# 现有的分层体系

网络理论模型有很多种，尽管理论有少许区别，但是核心内容应该是一样的。

![](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/network/model.png)

## OSI 七层模型

OSI七层协议模型分为：应用层（Application）、表示层（Presentation）、会话层（Session）、传输层（Transport）、网络层（Network）、数据链路层（Data Link）、物理层（Physical）

## TCP/IP 体系结构

TCP/IP 体系结构分为：应用层，运输层，网络层，网络接口层

## 五层体系结构

五层体系结构分为：应用层、运输层、网络层、数据链路层和物理层

## 对比

三个模型中都有的是应用层、运输层、网络层。在实际的开发当中，我们往往也只提及这三层。我们可以发现 TCP/IP 模型当中包含了 OSI 的应用层、表示层、会话层，然后使用网络接口层包括了数据链路层和物理层。

五层协议应该是对两种模型的取舍的结果。因此我们初步得出结论：

- OSI 模型当中的数据链路层、物理层分离是合理的
- OSI 模型当中的应用层、表示层、会话层分开不合理

## 为什么要提及网络分层模型

因为网络分层模型很好的解释了网络是如何工作的。一次 HTTP 请求，一层一层剥开，就可以很清楚了解每一层干了什么，每一层的意义是什么。

# 应用层（Application）

应用层位于 OSI 模型的最上层，有很多常见的协议，例如 HTTP（超文本传输协议，我们熟悉的网页）、FTP（文件传输协议，FTP 服务器）、SMTP（简单邮件传输协议）、POP3（邮局协议第三版）。

应用层提供为应用软件而设的接口，以设置与另一应用软件之间的通信。

比较令人惊讶的应该是 DNS 了，他是七层的，针对域名的转发通常称作七层转发。

部分博客谈到的 Gopher、TELNET、RPC 等均被维基百科认为是七层的。

# 表示层（Presentation）

把数据转换为能与接收者的系统格式兼容并适合传输的格式。

起初我也很困惑。

```
例如 PC 程序与另一台计算机进行通信

其中一台计算机使用扩展二一十进制交换码（EBCDIC）

而另一台则使用美国信息交换标准码（ASCII）来表示相同的字符。

如有必要，表示层会通过使用一种通格式来实现多种数据格式之间的转换。 　　
```

显然该层被弃用的理由不难推测，大家约定俗成就行，也与网络无关。

而维基百科给出的理由是应用层的 HTTP、FTP、Telnet 等协议有类似的功能。传输层的 TLS/SSL 也有类似功能。

# 会话层（Session）

负责在数据传输中设置和维护电脑网络中两台电脑之间的通信连接。

可以感觉在会话层并像其他层级那样是垂直的，更像一点并行的关系。

维基百科给出的理由是应用层的HTTP、RPC、SDP、RTCP等协议有类似的功能。

# 应用层小节

我们可以看到表示层和会话层被取代的理由基本都是由于应用层协议本身考虑到了相应的问题，给出了相应的解决方法，这两层已经没有了存在的意义。

# 应用层协议选讲

## HTTP

一个 HTTP 请求返回的东西，不只是我们显示在浏览器当中的网页（不是 HTML）。

### HTTP 报文

![]( https://image-static.segmentfault.com/287/070/2870706633-5bcbdc404eb45_articlex )

如图是一次 HTTP 请求的请求报文。如果对某个参数想了解更多请自行搜索。

```
HTTP/1.1 200 OK
Date: Sat, 31 Dec 2005 23:59:59 GMT
Content-Type: text/html;charset=ISO-8859-1
Content-Length: 122

＜html＞
＜head＞
＜title＞Wrox Homepage＜/title＞
＜/head＞
＜body＞
＜!-- body goes here --＞
＜/body＞
＜/html＞
```

如上，则是 HTTP 响应报文，响应报文分为四个部分，第一行为 HTTP_STATUS，然后接下来第二部分是响应的 header，第三部分是一个空行，第四部分则是响应报文的 body。第三部分恒定是一个空行。

### HTTP 长连接

客户端和服务端建立连接后不进行断开，之后客户端再次访问这个服务器上的内容时，继续使用这一条连接通道。

### HTTP 2.0

HTTP/2 相对于 HTTP/1.1 来说做出了很多优化。

[演示链接](https://http2.akamai.com/demo) 实际上，这个网页速度应该左边比右边慢，但是我测出来右边反而比左边慢。。。

#### 多路复用

![]( https://pic3.zhimg.com/80/b1e608ddb7493608efea3e76912aabe1_hd.jpg )

如图所示。HTTP/2 可以实现多流并行，而不是建立多个 TCP 连接来加速。

#### 报头压缩

![](https://www.ibm.com/developerworks/cn/web/wa-http2-under-the-hood/hpack_header_compression.png)

通过这种减少冗余的方式优化。

#### 服务器端推送

服务器端推送通过预测客户端需要的资源，主动推送。

例如：客户端请求index.html，服务器端能够额外推送script.js和style.css。如果客户端在有缓存的情况下请求，则会通知服务器不需要哪些资源。

#### 二进制分帧层

 ![img](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/network/binary.png) 
 
HTTP/2 性能提升核心在于此，他采用二进制传输，而不是文本格式。

## DNS

域名系统（英语：Domain Name System，缩写：DNS）是互联网的一项服务。它作为将域名和IP地址相互映射的一个分布式数据库，能够使人更方便地访问互联网。

### 域名解析

如果要请求 image.google.com，我们需要知道对应的 ip 地址。

以查询 image.google.com 为例：

- 客户端发送查询报文"query  image.google.com"至DNS服务器，DNS服务器首先检查自身缓存，如果存在记录则直接返回结果。
- 如果记录老化或不存在，则：
  ~~改用百度~~ 
  1. DNS服务器向根域名服务器发送查询报文"query  image.google.com"，根域名服务器返回顶级域 .com 的权威域名服务器地址。
  2. DNS服务器向 .org 域的权威域名服务器发送查询报文"query  image.google.com"，得到二级域 .google.com 的权威域名服务器地址。
  3. DNS服务器向 .google.com 域的权威域名服务器发送查询报文"query image.google.com"，得到主机 image 的A记录，存入自身缓存并返回给客户端。
  当然谁知道谁就返回了。

## RPC

### 什么是 RPC

RPC（Remote Procedure Call）远程过程调用，它是一种通过网络从远程计算机程序上请求服务，而不需要了解底层网络技术的协议。也就是说两台服务器A，B，一个应用部署在A服务器上，想要调用B服务器上应用提供的方法，由于不在一个内存空间，不能直接调用，需要通过网络来表达调用的语义和传达调用的数据。

### RPC 与 RESTful 的区别

RESTful 比较特别的有：

- 利用 HTTP 方法让接口统一化

```Text
GET /posts     获取文章             GET /getPosts       获取文章 
POST /posts    发布文章             GET /addPosts       发布文章 
PUT /posts     修改文章             GET /editPosts      修改文章 
DELETE /posts  删除文章             GET /deletePosts    删除文章 
```

左右的区别在于左边有 HTTP method 的区别，同时都对 posts 进行操作；右边则是动宾短语，用谓语表达操作行为，用宾语表达操作对线。左边符合 REST 设计风格。

相应的，由于 RPC 的设计为函数调用，其命名方式应该接近于右边采用谓语命名法。

- 利用HTTP状态码返回状态信息

```Text
Status Code: 200 OK
Status Code: 400 Bed Request
Status Code: 404 Not Found
Status Code: 500 Internal Server Error 
```

REST 依赖 HTTP Status Code 来判断请求结果，而 RPC 调用应该分为调用的网络请求是否成功，调用成功后结果是否成功。

RESTful 是建立在 HTTP 的基础上。gRPC 就是在 HTTP 上进行数据传输的；Netty 是基于 TCP、UDP 上进行传输的。

### RPC 与 SDK 的区别

之前我与 Leader 和其他同事争论其中的区别。

SDK 的代码应该是在本地运行的。而 RPC 的业务代码是在服务器端的。

但是 SDK 可以包含网络请求啊，网络请求之后那部分算不算 RPC 呢？

关键其实就是如何定义 Remote，如何定义 Procedure。

你品，你细品。

### RPC 是如何工作的

![img](https://dubbo.apache.org/img/blog/rpc/rpc-work-principle.png)

如图所示步骤 1-10：

1. Client 像调用本地服务似的调用远程服务；
2. Client Stub 接收到调用后，将方法、参数序列化
3. 客户端通过 sockets 将消息发送到服务端
4. Server Stub 收到消息后进行解码（将消息对象反序列化）
5. Server Stub 根据解码结果调用本地的服务
6. 本地服务执行(对于服务端来说是本地执行)并将结果返回给 Server Stub
7. Server Stub 将返回结果打包成消息（将结果消息对象序列化）
8. 服务端通过 sockets 将消息发送到客户端
9. Client Stub 接收到结果消息，并进行解码（将结果消息发序列化）
10. 客户端得到最终结果。

### jsonRPC

JSON-RPC是一个无状态且轻量级的远程过程调用(RPC)协议。

我司之前用的大概就是 jsonRPC 改，并命名为 XX_RPC，（这玩意儿真的好用吗 - -），然后我还甚至能 fake Client Stub 和 Server Stub。

```Text
--> {"jsonrpc": "2.0", "method": "subtract", "params": [42, 23], "id": 1}
<-- {"jsonrpc": "2.0", "result": 19, "id": 1}
```
请求对象：
- jsonrpc

  指定JSON-RPC协议版本的字符串，必须准确写为“2.0”

- method

  为调用的方法名

- params

  传递的参数

- id	

  已建立客户端的唯一标识id

响应对象：
- jsonrpc

  指定JSON-RPC协议版本的字符串，必须准确写为“2.0”

- result

  该成员在成功时必须包含。
  服务端中的被调用方法决定了该成员的值。

- error

  该成员在失败是必须包含。

- id	

  已建立客户端的唯一标识id

### gRPC

gRPC 设计上是分层的，底层支持不同的协议。

- [gRPC-web](https://github.com/grpc/grpc/blob/master/doc/PROTOCOL-WEB.md)

- [gRPC over HTTP2](https://github.com/grpc/grpc/blob/master/doc/PROTOCOL-HTTP2.md)

gRPC 在后端之间调用往往采用 ** gRPC over HTTP2 **。

gRPC-web 多用于前端，实际上 gRPC-web 解决的是 REST 部分是 RPC 翻译器的问题。

![img](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/network/grpc-web.png)

[REST 的替代者：Envoy + gRPC-Web](https://juejin.im/post/5c4e791f6fb9a049ba41f6b0)

值得注意的是前后端交互需要 Envoy 来转换。而 Envoy 扮演的角色是：

![img](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/network/envoy.png)


# 部分参考文献

[全双工通信的 WebSocket](https://halfrost.com/websocket/#websocket)
[浅谈 RPC](https://dubbo.apache.org/zh-cn/blog/rpc-introduction.html)
[RPC和RESTful API入门篇](https://ddnd.cn/2018/12/19/rpc-and-restful/)
[思考gRPC:为什么是HTTP/2](http://hengyunabc.github.io/thinking-about-grpc-http2/)
[域名系统——wiki](https://zh.wikipedia.org/wiki/%E5%9F%9F%E5%90%8D%E7%B3%BB%E7%BB%9F#%E5%9F%9F%E5%90%8D%E8%A7%A3%E6%9E%90)