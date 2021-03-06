# 网络

## 网络

### URL

URL全称Uniform Resource Locator（统一资源定位符）  
通过一个URL就能找到网络上唯一的一个资源  
URL就是资源的地址、位置，互联网上每个资源都有一个唯一的URL

**URL的基本格式** = 协议://主机地址/路径

* `协议`：不同的协议代表着不同的资源查找方式、资源传输方式。
* `主机地址`：存放资源的主机（服务器）IP地址（域名）
* `路径`：资源在主机（服务器）中的具体位置

#### URL中常见的协议

1、HTTP

```text
超文本传输协议，访问的是远程的网络资源
```

2、file

```text
    访问的是本地计算机上的资源
```

3、mailto

```text
    访问的是电子邮件地址
```

4、FTP

```text
    访问的是共享主机的文件资源
```

### HTTP协议

#### HTTP协议的作用

（1）规定客户端和服务端之间数据的传输格式  
（2）让客户端和服务端能够有效的进行数据沟通

#### HTTP的通信过程：请求和响应

**请求**

**请求行**：包含了请求方法、资源路径和HTTP协议版本  
GET /MJServer/resources/images/1.jpg HTTP/1.1

**请求头**:包含了对客户端环境的描述、客户端请求的主机地址等信息  
Host: 192.168.1.105:8080 // 客户端想访问的服务器主机地址  
User-Agent: Mozilla/5.0 \(Macintosh; Intel Mac OS X 10.9\) Firefox/30.0// 客户端的类型，客户端的软件环境  
Accept: text/html, _/_// 客户端所能接收的数据类型  
Accept-Language: zh-cn // 客户端的语言环境  
Accept-Encoding: gzip // 客户端支持的数据压缩格式

**请求体**：客户端发给服务器的具体数据，比如文件数据

**响应**

**状态行**：包含了HTTP协议版本、状态码、状态英文名称  
HTTP/1.1 200 OK

**响应头**：包含了对服务器的描述、对返回数据的描述

**实体内容**：服务器返回给客户端的具体数据，比如文件数据  
Server: Apache-Coyote/1.1 // 服务器的类型  
Content-Type: image/jpeg // 返回数据的类型  
Content-Length: 56811 // 返回数据的长度  
Date: Mon, 23 Jun 2014 12:54:52 GMT // 响应的时间

常见的**响应状态码**  
200 OK 请求成功  
400 Bad Request 客户端请求的语法错误，服务器无法解析  
404 Not Found 服务器无法根据客户端的请求找到资源  
500 Internal Server Error 服务器内部错误，无法完成请求

**8种HTTP请求方法**  
GET、POST、OPTIONS、HEAD、PUT、DELETE、TRACE、CONNECT、PATCH

### HTTPS

使用安全套接字层进行信息交换，简单来说它就是HTTP的安全版，使用TLS/SSL加密的HTTP协议

为什么要使用HTTPS？

* 因为HTTP采用明文传输信息，存在信息窃听、信息篡改和信息劫持的风险
* HTTPS具有身份验证、信息加密和完整校验的功能，可以避免此类问题

#### TLS/SSL

是介于HTTP和TCP之间的一层安全协议  
不影响原有的HTTP协议和TCP协议

**TLS/SSL工作原理**

TLS/SSL功能实现依赖于三类算法

* `非对称加密`：身份认证和对称秘钥协商
* `对称加密`：采用协商的对称秘钥对数据进行加密
* `散列算法`： 验证数据完整性

**非对称加密**

* 非对称加密算法：RSA、ECC、DH等
* 算法特点：由一对秘钥组成，俗称密钥对（`公钥`和`私钥`），公钥的加密信息只有私钥能解开，私钥的加密信息只有公钥能解开
* 通信方式1vn，服务器可以一对多的通信
* 缺点：算法的复杂度高，加密速度慢

**对称加密**

* 对称加密算法：AES、DES、3DES、IDEA、RC4等
* 同一个密钥可以用于信息的加密和解密

**散列算法**

* 散列算法：MD5、SHA1、SHA256
* 算法特点：单向不可逆、对输入非常敏感、输出长度固定
* 针对数据的任何修改都会改变散列算法的结果，可以验证数据的完整性
* 补充：SHA-1、SHA-224和SHA-256适用于长度不超过2\^64二进制位的消息，SHA-384和SHA-512适用于长度不超过2^128二进制位的消息

`RSA加密`：这个客户端里面有使用过，MOA里面的登录密码是`RSA`加密的，客户端代码里放了公钥，使用公钥加密密码，传给后台做登录使用。

`MD5`：这个也用过，用于请求的签名。

### DNS

DNS（Domain Name System，域名系统）是互联网的一项服务，提供了将人类易于理解的域名转换成计算机或网络可识别的数字地址的机制，能够使人更方便的访问互联网。

`DNS解析`：URL域名解析成IP地址的过程

**DNS劫持**  
由于DNS请求是明文，请求过程中可被攻击者监测，然后攻击者`伪装成DNS服务器`向主机发送带有假IP地址的响应报文，从而使得主机访问到假的服务器。

解决方案：

`LocalDNS`：本地解析IP地址

`HTTPDNS`：通过HTTP请求到后台拿域名对应的IP地址

## 网络优化

一直都是一个人独立开发的小型APP，APP的用户都不多，公司对这块要求也不高也没有资源，所以这一块基本没有过实践。

大型APP一般都需要做一些网络优化，包括：

1. **速度**：网络请求的速度怎样能进一步提升？
2. **弱网**：怎样在移动端弱网情况下最大限度最快的完成网络请求？
3. **安全**：怎样方式被第三方窃听/篡改和冒充，防止运营商劫持又不影响性能？

**速度**：HTTPDNS、连接多路复用、更好的数据压缩算法

参考文章：

[移动 APP 网络优化概述](https://blog.cnbang.net/tech/3531/)

### 网络安全

#### 中间人攻击

`中间人攻击`：攻击者与通信的两端分别建立独立的联系，并交换其所受到数据，使通信的两端认为他们正在通过一个私密的连接与对方直接通话，但实际上整个会话都会被攻击者控制。

#### 安全地传输用户密码

安全做法：非对称加密密码密文传输，服务器密文存储比对。即使用`非对称加密`算法加密密码，密文传输到后台，后台解密后加盐之后再多次求`MD5`，然后再和服务器之前采用同样方式存储的密码匹配，确认登录结果。

#### 通讯协议安全

`通讯协议`：是指通信双方对数据传送控制的一种约定。约定中包括对数据格式，同步方式，传送速度，传送步骤，纠错方式以及控制字符定义等问题做出统一规定，通信双方必须共同遵守。

参考文章：

[iOS应用安全开发概述](http://blog.devtang.com/2014/05/08/ios-security-dev-overview/)

