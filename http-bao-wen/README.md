# HTTP 报文

HTTP(HyperText Transfer Protocol) is a **stateless(无状态)** application-level **request/response** protocol that uses **extensible semantics(可扩展语义)** and **self-descriptive(自描述)** message payloads for flexible interaction with network-based **hypertext information** systems. - from **RTC7230**。

HTTP是一种能够获取HTML这样的网络资源的通讯协议。是web上进行数据交换的基础，是一种client-server协议。

HTTP是应用层的协议，通过TCP或者TLS(加密的TCP)连接来发送信息，不仅用来传输超文本文档，也可以传输图片、视频，也可以部分文档内容更新网页。

### 报文流

报文主要是在**客户端**和**服务端**之间进行流通。**Client**发送的报文称为**请求报文**，服务端返回给Client的称之为**响应报文。**

报文是数据传输的载体，互联网上所有展示的信息以及服务器流通的数据都是报文。

### 报文组成

Client发送一个HTTP请求向服务端，这个请求以一个请求行（request-line）开始，包含了Method、Path、Protocol Version；接下来是请求修饰符（request modifiers），包含了客户端信息以及表示元数据的头字段；最后就是包含有效负载的消息正文。

![from mdn](../.gitbook/assets/HTTPMsgStructure2.png)

#### 报文语法

```bash
HTTP-message = start-line
               *(header-field CRLF)
               CRLF
               [ message-body ]
```

### Reference

* [IETF RFC 7230 Message Syntax and Routing ](https://tools.ietf.org/html/rfc7230)

