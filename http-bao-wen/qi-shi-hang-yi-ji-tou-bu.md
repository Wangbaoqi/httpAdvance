# 起始行以及头部

起始行（start-line）包含了请求行（request-line）和响应行（status-line）。

起始行包含了客户端请求的一些方法，也就是Methods。

| Method  | description              | 是否包含主体 |
| ------- | ------------------------ | ------ |
| GET     | 从服务器获取一份文档               | no     |
| HEAD    | 只从服务器获取文档的首部             | no     |
| POST    | 向服务器发送要处理的数据             | yes    |
| PUT     | 将请求的主体部分存储在服务器上          | yes    |
| DELETE  | 从服务器上删除一份文档              | no     |
| OPTIONS | 决定在服务器上可以执行哪些方法          | no     |
| TRACE   | 对可能经过代理服务器传送到服务器上的报文进行追踪 | no     |

响应行也就是服务端反馈给客户端状态信息，也就是状态码以及响应短语。

### 首部和方法

[Header Field](https://tools.ietf.org/html/rfc7230#section-3.2) **** 包含了一个**不区分大小写**的 **Field Name，**后面跟 **":"**以及**Field Value。**

所有的消息头都在[IANA注册表](https://www.iana.org/assignments/message-headers/message-headers.xhtml)中列出，原始内容在[ RFC4229](https://tools.ietf.org/html/rfc4229) 定义。

```http
Header-field = field-name ":" OWS field-value OWS
OWS = Optional whiteSpace 
```

首部和方法共同决定了客户端和服务器要做什么。首部主要分为五个类型。

### 通用首部

通用首部是客户端和服务器都可以使用的，提供了与报文相关的基础功能。在客户端和服务器都提供一些通用的功能，比如 **Date，每一端都可以用它来构建报文的时间。**通用首部只能在请求头部或者响应头部，不能在实体头部。

| header            | description                                                    |
| ----------------- | -------------------------------------------------------------- |
| Connection        | 允许客户端和服务器指定请求或者响应是否连接选项                                        |
| Date              | 报文创建的时间                                                        |
| Cache-Control     | 随报文传递是否缓存指示                                                    |
| Transfer-Encoding | 告知接收端为了传输安全，报文采用什么编码方式                                         |
| Trailer           | 实现报文主体后记录哪些首部字段，该首部字段可以使用在HTTP/1.1版本分块传输编码时。 Trailer: Expiress |
| Upgrade           | 要求服务器升级到一个高版本协议                                                |
| Via               | 告诉服务器，这个请求是哪些代理发出去的                                            |

#### Connection&#x20;

Connection header 决定当前事务（请求/响应）结束后，是否关闭网络连接。如果其值是**Keep-alive**，网络连接就是持久性的。这样同一个服务器上的请求都可以在这个连接上完成。

```http
Connection: keep-alive // 持久连接 http/1.1 的默认值
Connection: close // 关闭网络连接 http/1.0 的默认值
```

#### Date

Date 包含了报文创建的时间和日期

```http
Date: <day-name>, <day> <month> <year> <hour>:<minute>:<second> GMT
// GMT 格林尼治时间 不是本地时间
// Date: Wed, 21 Oct 2020 08:29:33
```

#### Cache-Control

Cache-Control 被用于请求和响应中，通过指定来实现缓存机制。缓存是单向的，请求中设置了，只在请求中有效。

缓存指令

```http
// 客户端缓存指令
Cache-Control: max-age=<second> // 设置缓存的最大周期，单位S
Cache-Control: max-stale[=<second>] // 客户端可以接受过期的资源
Cache-Control: no-cache // 发布缓存副本之前，强制要求把请求交给原始服务器进行验证（协商缓存)
Cache-Control: no-store // 不使用任何缓存，缓存不应该存储有关客户端或者服务器响应的任何内容
Cache-Control: no-transform // 不得对资源进行转换或者转变

// 服务器缓存指令
Cache-Control: public // 响应可以被任何对象缓存
Cache-Control: private // 响应只能被单个用户缓存
```

有关Cache-Control的其他指令，可以查询[\[RFC7234\]](https://tools.ietf.org/html/rfc7234#section-5.2) 或者[ \[MDN Cache-Control\]](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Cache-Control)

#### Transfer-Encoding

Transfer-Encoding 指明将消息实体传递给用户所采用的的编码方式。一般出现在响应头部。仅用于两个节点之间消息传输，如果是端到端之间的传输，采用**Content-Encoding**

```http
Transfer-Encoding: chunked // 数据以分块的方式发送
Transfer-Encoding: compress // 采用Lempel-Ziv-Weich压缩算法
Transfer-Encoding: gzip // 采用Lempel-Ziv coding 压缩算法
// e.g
Transfer-Encoding: gzip, chunked
```

有关Transfer-Encoding 其他的描述以及指令，可以查询[\[RFC7230\]](https://tools.ietf.org/html/rfc7230#section-3.3.1) 或者 [\[MDN Transfer-Encoding\]](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Transfer-Encoding)

#### Trailer



### 请求首部

请求首部主要是针对请求报文中有意义的首部。服务器可以根据客户端请求报文中提供的首部进行更好的响应。

请求首部根据不同功能也分为以下类型

#### 信息型首部

信息型首部主要是提供的当前请求报文的载体（客户端）的信息

| Header     | description                                |
| ---------- | ------------------------------------------ |
| Client-IP  | 客户端机器的IP地址                                 |
| From       | 提供了客户端中用户的E-Mail地址                         |
| Host       | 提供了请求服务器的主机地址以及端口号(无 默认 HTTPS 443 HTTP 80) |
| Referer    | 包含了当前请求URL的来源页面的地址                         |
| User-Agent | 将发起请求的客户端的名称告知服务器 用户代理                     |

#### Referer 首部

此请求头表示了该页面是从来源页面的链接进入的，因此，使用Referer头可以记录到用户浏览信息，可以用来统计分析、日志分析以及缓存优化等。

下面两种情况 referer 是不会发送的

* 来源页面采用的协议表示本地的 “file” 或者 “data" URL
* 当前请求页面采用的是HTTP，来源页面采用的是安全协议

#### Accept 类型首部

Accept header 主要是告知服务器 客户端可以处理什么类型的内容。内容类型用[**MIME类型（媒体类型）**](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Basics\_of\_HTTP/MIME\_types)表示。服务器在响应头 **Content-type** 应答客户端。

| Header          | Description    |
| --------------- | -------------- |
| Accept          | 告知服务器可以接受的媒体类型 |
| Accept-Charset  | 告知服务器可以处理的字符集  |
| Accept-Encoding | 告知服务器能够发送哪些编码  |
| Accept-Language | 告知服务器能够发送哪些语言  |

客户端为请求加上某些限制时，使用条件型首部。

| Header              | Description              |
| ------------------- | ------------------------ |
| Expect              | 允许客户端列出某请求的所要求的服务器行为     |
| If-Match            | 实体标记和文档当前的实体标记相匹配，获取文档   |
| If-None-Match       | 实体标记和文档当前的实体标记不相匹配，获取文档  |
| If-Modified-Since   | 某个资源在指定日期之后修改过，则返回对应资源   |
| If-Unmodified-Since | 某个资源在指定日期之后没有修改过，则返回对应资源 |
| If-Range            | 允许对文档的某个范围内进行请求          |

#### 安全型首部

在客户端获取特定的响应资源时，会先对自身进行验证。这个也叫HTTP一种安全机制 **质询/响应认证**

| **Header**    | Description        |
| ------------- | ------------------ |
| Authorization | 客户端提供给服务端的自身数据进行验证 |
| Cookie        | 客户端向服务器提供一个令牌      |

#### Cookie Header





#### 代理型首部

代理型的首部目前有 Proxy-Authenticate、Proxy-Authentication-Info、Proxy-Authorization、Proxy-Features、Proxy-Connection。

### 响应首部

响应首部也有其对应的功能，比如谁在发送请求，发送给客户端的信息应该如何处理。

#### 信息型首部

| Header | Description      |
| ------ | ---------------- |
| Age    | 最初创建开始 响应持续的时间   |
| Server | 服务器应用程序的软件的名称和版本 |

#### 协商首部

对资源有多种的表示方法。

协商首部有  `Accept-Ranges` 、 `Vary` ，后面对协商首部会有详述。

#### 安全首部    &#x20;

安全首部跟请求首部类似          &#x20;

### 实体首部

实体首部提供了大量跟消息和其内容有关的信息。告知报文的接收者对消息进行什么操作。

#### 信息首部

| Header   | Description                   |
| -------- | ----------------------------- |
| Allow    | 可以对实体执行的请求方法                  |
| Location | 告知客户端实体实际的位置，将接收端定位到定向到资源的URL |

#### 内容首部

该首部提供了与实体内容有关的信息

| Header           | Description        |
| ---------------- | ------------------ |
| Content-Encoding | 对主体内容执行的编码方式       |
| Content-Language | 主体内容使用的语言          |
| Content-Length   | 主体内容的长度            |
| Content-Location | 主体内容的实际位置          |
| Content-MD5      | 主体内容的MD5校验         |
| Content-Range    | 整个资源中该主体内容的表示的字节范围 |
| Content-Type     | 主体的媒体类型            |

#### 缓存首部

通用的缓存首部说明如何、什么时候缓存。实体首部缓存提供了与被缓存实体有关的信息。

| Header        | Description   |
| ------------- | ------------- |
| ETag          | 与当前实体有关的标记    |
| Expires       | 实体不再有效        |
| Last-Modified | 当前实体最后一次修改的时间 |
