title: WebSocket 是 Socket 吗？
date: 2019-11-28 21:12:00
desc: 
tags: [network] 
index_img: https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/websocket.png
banner_img: https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/websocket.png
---

WebSocket 带上了个 socket，但是两者差别应该还是挺大的。

<!-- more -->

# 什么是 WebSocket

（黑马是马吗？蜗牛是牛吗？啤酒是酒吗？） 

WebSocket 其实是一个位于七层的协议。WebSocket 协议在 2011 年由 IETF 标准化为 RFC 6455，后由 RFC 7936 补充规范。Web IDL 中的 WebSocket API 由 W3C 标准化。

WebSocket 使得客户端和服务器之间的数据交换变得更加简单，允许服务端主动向客户端推送数据。在 WebSocket API 中，浏览器和服务器只需要完成一次握手，两者之间就可以创建持久性的连接，并进行双向数据传输。

## URL

统一资源定位符（英语：Uniform Resource Locator，缩写：URL；或称统一资源定位器、定位地址、URL地址，俗称网页地址或简称网址）是因特网上标准的资源的地址（Address），如同在网络上的门牌。它最初是由蒂姆·伯纳斯-李发明用来作为万维网的地址，现在它已经被万维网联盟编制为因特网标准RFC 1738。

统一资源定位符的标准格式如下：
```
[协议类型]://[服务器地址]:[端口号]/[资源层级UNIX文件路径][文件名]?[查询]#[片段ID]
```

统一资源定位符的完整格式如下：
```
[协议类型]://[访问资源需要的凭证信息]@[服务器地址]:[端口号]/[资源层级UNIX文件路径][文件名]?[查询]#[片段ID]
```

其中[访问凭证信息]、[端口号]、[查询]、[片段ID]都属于选填项。

从这里也可以印证出 WebSocket 是一个七层的协议。

WebSocket 使用 ws 或 wss 的统一资源标志符，类似于 HTTPS。其中 wss 表示使用了 TLS  的 WebSocket。如：
```
ws://example.com/wsapi
wss://secure.example.com/wsapi
```

# 为什么要 WebSocket

为了实现更加实时的通信。

## 短连接长连接

长连接是在 HTTP 1.1 之后默认使用的，但实际上是在用 TCP 的长连接短连接。关于长连接短连接的文章有很多，不再赘述。长连接省去了较多的 TCP 握手和关闭的时间。问题就在于如果较多长连接存在的时候，服务器需要采取一些措施来释放资源。

## 流（Streaming）

流常见的有 Iframe Streaming、XHR Streaming、Flash Streaming、Server-Sent Events。

其主要思想都是从服务器向客户端发送数据。

## 上述优缺点

短连接自然不用讲，每个文件的请求都需要建立一次连接。

长连接情况下，仍然需要与客户端保持连接，消耗大量资源。

到了流的方式，服务器往客户端推送，这个方向的流实时性比较好，服务器的请求压力就会减少很多，因为是服务器给用户推送信息，而不是长连接然后轮询。但是依旧是单向的，客户端请求服务器依然还需要一次 HTTP 请求。

流对浏览器支持要求也比较高。

## 解决

websocket 是独立在单个 TCP 连接上进行的全双工通讯，是个有状态的协议。

当然除此之外，他还有其他等等优点，还能支持二进制帧、扩展协议、部分自定义的子协议、压缩等特性。

# 题外话

之前在图森未来实习工作的时候，曾有幸担任几次面试官，我记得有一位不幸的朋友被我问了 WebSocket 是 Socket 吗。

（他最后居然一本正经地解释给我听不同 socket 的区别，给我整蒙了）

其实是因为当时我正做相关方面开发，也是想试一试他知不知道相关方面的知识。

但是后面回过头来看，这个问题不太行，问了没啥意义- -。。。

不过这都是题外话了
