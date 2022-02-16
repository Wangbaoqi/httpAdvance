# Web资源以及URI

web资源，也就是网络上的资源，这些资源包括了网页、HTML、CSS、视频、图片等等，只要是能够在互联网上存储的东西，都可以称之为资源。

而要访问到这些资源，则需要**URI（Uniform Resource Identifier）统一资源标识符，**有了这个规则，就可以准确的访问到互联网中任何一个资源。

### URI **Uniform Resource Identifier**

URI **（**统一资源标识符）是紧凑的字符序列，提供了一种简单可扩展的方式来表示抽象或者物资源。比如每一台web服务器中资源名称也被称为URI。

相比URI，我们更加熟悉`URL`，除此之外，还有类似的`URN`，而URI是他们的超集。

在URI规范[`RFC3986`](https://tools.ietf.org/html/rfc3986)中分别对`Uniform`、`Resource`和`Identifier`进行了定义。主要有以下三个特性：

**Uniform**

* 规定统一的格式（语法）处理不同类型的资源标识符。eg. 在HTML中图片请求和脚本的请求类型就完全不一致
* 允许引入新类型的资源标识符，不会干扰现有的资源类型。eg. video 和 audio
* 允许标识符在不同的上下文中重用

**Resource**

* 可以是图片、文档、温度等，也可以是抽象的概念，数字、类型等
* 一个资源可以有多个URI

**Identifier**

* 当前资源与其他资源区分开的名称

URI 用字符串标识互联网资源。也就是用某个协议表示的资源定位标识符，比如HTTP协议、FTP协议等。标准的[URL协议](https://www.iana.org/assignments/uri-schemes/uri-schemes.xhtml)有30多种。

常见的协议有以下几种:

```javascript
ftp://ftp.is.co.za/rfc/rfc1808.txt
http://www.ietf.org/rfc/rfc2396.txt
ldap://[2001:db8::7]/c=GB?objectClass?one
mailto:John.Doe@example.com
news:comp.infosystems.www.servers.unix
tel:+1-816-555-1212
telnet://192.0.2.16:80/
urn:oasis:names:specification:docbook:dtd:xml:4.1.2
```

### URI 语法

通用URI语法由组件的层次结构序列组成，包括**scheme**，**authority**，**path**，**query**以及**fragment**。

```
URI         = scheme ":" hier-part [ "?" query ] [ "#" fragment ]

hier-part   = "//" authority path-abempty
               / path-absolute
               / path-rootless
               / path-empty
```

**URI格式语法组成**，是遵循[`ABNF`](https://tools.ietf.org/html/rfc5234)产生式来定义的。

![](.gitbook/assets/uri\_component.png)

#### Scheme 方案

Scheme（方案），也就是使用什么协议来访问资源

每个URI均以Scheme名称开头，由一系列字符（`字母`，`数字`，`+`，`.`或者`-`）任意组成，规范格式为小写，接收与小写字母等效的大写字母(HTTP和http)，不过建议使用小写。

```
scheme = ALPHA  (ALPHA / DIGIT / " +" / "-"/ ".")
```

_例如_ `http`、`ftp`、`telnet`、`https`、`file`或者`mailto`

#### Authority 权限

授权验证前面有`//`，并且由下一个`/`、`?`或者数字符号`#`字符终止URI

```
authority = [ userinfo "@" ] host [":" port]
userinfo =  user: password 
port =  DIGIT
```

根据`ABNF`语法 _\[ userinfo "@" ]和\[":" port]_是可以忽略的，因此我们常见的URI为`google.com`

用户信息 代表用访问host是需要验证信息

端口号  HTTP默认端口为`80`，HTTPS默认端口为`433`

#### **Path 路径**

path一般包含通常以分层形式组织的数据以及非分层query数据，这些数据用于表示服务端中的资源。

```bash
path =  path-abempty: 以"/" 或者 ""开始
        / path-absolute 以"/"开始 不能是"//"
        / path-rootless 
        / path-empty
```

path 由一系列的path段组成，这些段由`/`分隔。

#### **Query 查询字符串**

query包含了非分层数据，以及路径组件中的数据。由第一个问号`?`字符开始，并由数字符号`#`字符或者URI末尾终止。

```bash
query = *(pchar /" /" /"? ")
```

#### Fragment 片段

fragment 的出现是为了展示大型资源中的某一片段。在客户端也可以用作锚点，展示对应的资源。

```bash
fragment = *(pchar /" /" /"? ")
```

### URL 方式

URL的使用方式有两种：**绝对URL**和**相对URL。**我们常用的是**绝对URL，相对URL**一般是在复杂项目中跳转不同的页面使用比较便捷。

### URL 编码机制
