# 状态码

### 状态码分类

### 100 - 199&#x20;

#### 100 - 199 信息提示 请求已接收，继续进程进程，已定义范围 100 - 101

| code | reason-phrase       | description                                                                                                                                                   |
| ---- | ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 100  | Continue            | 收到了请求的初始部分，请客户端继续。更多请看[\[RFC 7231 6.2.1\]](https://tools.ietf.org/html/rfc7231#section-6.2.1)                                                                 |
| 101  | Switching Protocols | 服务器根据客户端指定，将协议切换成Update首部所列协议更多请看[\[RFC 7231 6.2.](https://tools.ietf.org/html/rfc7231#section-6.2.2)[2\]](https://tools.ietf.org/html/rfc7231#section-6.2.2) |

### 200 - 299&#x20;

#### 200 - 299 成功 请求被成功接收、理解以及处理，已定义范围 200 - 206

| code  | reason-phrase                 | description          |
| ----- | ----------------------------- | -------------------- |
| 200   | OK                            | 请求无问题                |
| 201   | Create                        | 用户创建服务器对象的请求         |
| 202   | Accepted                      | 请求已被接受，但是还没有处理       |
| 203   | Non-Authoritative Information | 实体首部包含信息不是来源于源服务器    |
| 204   | No Content                    | 没有实体主体部分             |
| 205   | Reset Content                 | 另一个主要用于浏览器代码         |
| 206   | Partial Content               | 成功执行了一个部分或者range范围请求 |

### 300 - 399&#x20;

#### 300 - 399 重定向 需要进一步采取行动 以便完成请求，已定义范围 300 - 305

重定向一般是服务器告知客户端需要进一步去请求资源移动到新服务器。如果资源被移动了，服务器响应重定向状态码以及一个新的资源地址，一边客户端去请求所需资源信息。

重定向还可以识别资源是否被修改过。客户端请求头加了 **If-Modifier-Since，**如果在这个时间之后没有修改文档，则不会返回响应，直接返回状态码。

```http
// 请求报文
POST /test HTTP/1.1
Host: www.nate.com
If-Modifier-Since: Tue Dec 01 2010 16:27:22 GMT
// 响应报文
HTTP/1.1 304 Not Modifier
```

| code  | reason-phrase    | description                   |
| ----- | ---------------- | ----------------------------- |
| 300   | Multiple Choices | 客户端请求一个实际指向多个资源的URL会返回        |
| 301   | Move Permanently | 在请求的URL已被移除时使用                |
| 302   | Found            | 客户端使用Location首部给出的URL来定位资源    |
| 303   | See Other        | 告知客户端使用另一个URL获取资源             |
| 304   | Not Modified     | 告知客户端资源是否被修改过                 |
| 305   | Use Proxy        | 必须通过一个代理来访问资源，代理位置由Location给出 |

>

### 400 - 499&#x20;

#### 400 - 499  客户端错误 请求包含错误语法，已定义范围 400 - 415

客户端错误码也是常见的，比如常见的400、404

| code | reason-phrase                   | description                        |
| ---- | ------------------------------- | ---------------------------------- |
| 400  | Bad Request                     | 告知客户端发送了一个错误的请求                    |
| 401  | Unauthorized                    | 由于缺少有效的身份验证，必须传送WWW-Authenticate标头 |
| 402  | Payment Required                | 未使用                                |
| 403  | Forbidden                       | 请求被服务器拒绝了                          |
| 404  | Not Found                       | 请求URL未被服务器找到                       |
| 405  | Method Not Allowed              | 请求中方法服务器不支持                        |
| 406  | Not AcceptTable                 | 服务器没有匹配到客户端所要求类型的实体                |
| 407  | Proxy Unauthorized Required     | 用于对资源需要认证的代理服务器                    |
| 408  | Request Timeout                 | 客户端请求耗时太长                          |
| 409  | Conflict                        | 在资源上引发一些冲突                         |
| 410  | Gone                            | 类似404，服务器曾经拥有过资源                   |
| 411  | Length Required                 | 服务器要求请求报文中包含Content-Length头        |
| 412  | Precondition Failed             | 客户端发起的条件请求，其中一个失败了                 |
| 413  | Payload Too Large               | 客户端发起的请求实体主体比服务器所能处理还要大            |
| 414  | Request URL Too Long            | 请求URL太长了                           |
| 415  | Unsupported Media Type          | 服务器无法理解请求媒体类型                      |
| 416  | Requested Range Not Satisfiable | 请求报文所请求的是指定资源的范围                   |
| 417  | Expectation Failed              | 请求头Except包含了一个期望，服务器无法理解           |

### 500 - 599&#x20;

#### 500 - 599 服务器错误，服务器错误执行了请求，已定义范围 500 - 505&#x20;

| code | Reason Phrase              | Description                      |
| ---- | -------------------------- | -------------------------------- |
| 500  | Internal Server Error      | 服务器错误                            |
| 501  | Not Implemented            | 客户端发起的请求超出了服务器能力范围               |
| 502  | Bad Gateway                | 作为代理或网关使用的服务器从请求响应链的下一条链路上收到了伪响应 |
| 503  | Service Unavailable        | 服务器无法为请求提供服务                     |
| 504  | Gateway Timeout            | 响应来自网关或者代理，等待另一服务器请求超时了          |
| 505  | HTTP Version Not Supported | 服务器收到的请求使用其无法理解的协议版本             |

更多有关状态码的信息可以查询 [\[RFC7231\]](https://tools.ietf.org/html/rfc7231#section-6)规范
