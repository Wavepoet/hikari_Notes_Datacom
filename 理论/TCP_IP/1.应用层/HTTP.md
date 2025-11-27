# **HTTP：超文本传输协议**

它是基于**TCP协议**的**应用层传输协议**，简单来说就是**客户端和服务端进行数据传输的一种规则**。请求和响应消息的头以[ASCII](https://baike.baidu.com/item/ASCII/309296?fromModule=lemma_inlink)形式给出；而消息内容则具有一个类似[MIME](https://baike.baidu.com/item/MIME/2900607?fromModule=lemma_inlink)的格式。

> 特点

- 帮助客户**访问万维网**
- 网页浏览器通过翻译**HTML**（超文本标识语言）文件表现文本，图像，音乐，动画及视频等对象
- 支持**客户/服务器**模式。
- **灵活**：HTTP允许传输任意类型的数据对象
- **无连接**：无连接的含义是限制每次连接只处理一个请求
- **无状态**：HTTP协议是无状态协议。无状态是指协议对于事务处理没有记忆能力。
- **简单快速**：客户向服务器请求服务时，只需传送请求方法和路径。

**太多，推荐查询[HTTP_百度百科 (baidu.com)](https://baike.baidu.com/item/http/243074)

## **URL：统一资源定位符**

URL是对可以从互联网上得到的资源的位置和访问方法的一种简洁的表示，互联网上的每个文件都有一个唯一的URL，它包含的信息指出文件的位置以及浏览器应该怎处理它。**URL是web页的地址。**
|ヾ(≧▽≦*)o就是这个
v
![](HTTP_image/image3.png)

URL由3个主要的部分构成：**协议**，**服务器地址**和**具体地址**

- **协议**是告诉我们自己面对的是何种类型的Internet资源。
- 存有该资源所在的**服务器的名称**或**IP地址**(包括端口号);
- 主机资源的**具体地址**

### 格式：

```

scheme://host[:port#]/path/…/[;url-params][?query-string][#anchor]
```


| **scheme(协议)**         | 有我们很熟悉的http，https，ftp以及ed2k，迅雷的thunder等。                |
| ------------------------------ | ------------------------------------------------------------------------ |
| **host(主机名)**         | http服务器的ip地址或域名                                                 |
| **port(端口)**           | http的默认端口是80，这种情况下端口号可以省略。如果使用其他端口必须指明。 |
| **path(路径)**           | 访问资源的路径                                                           |
| **url-params(查询参数)** | 所带参数                                                                 |
| **query-string**         | 发给http服务器的数据                                                     |
| **Franchor(锚点)**       | 锚点定位                                                                 |

![](HTTP_image/image2.jpeg)

### **URI（统一资源标识符）与URN(统一资源名称)**

Web上可用的每种资源都由一个通用资源标识符（URI）进行定位。URI可以分为URL,URN（统一资源名称）。**URN**确定了**东西的身份**，**URL**提供了**找到它的方式**。

因此，三者之间的关系是：**URL 一定是 URI，URN + URL 就是 URI。**

例如：

[http://www.baidu.com](https://link.zhihu.com/?target=http%3A//www.baidu.com)是URL.http://www.baidu.com/index.html 是URL 同时也是URI。

所以，URL 就是 URI 的 定位。

## **REQUEST：请求**

客户端发送一个HTTP请求到服务器的请求消息包括以下格式：**请求行、请求头部、空行和请求数据**四个部分组成，下图给出了请求报文的一般格式

![](HTTP_image/image1.png)

### **请求行**

包含三个信息：**请求方式、URI、HTTP 协议版本。**

### **请求方式**

| **get**      | 请求**获取**Request-URI所标识的资源                        |
| ------------------ | ---------------------------------------------------------------- |
| **post**     | 在Request-URI所标识的资源后**增加新的数据**                |
| **head**     | 请求获取由Request-URI所标识的资源的响应消息报头                  |
| **put**      | 请求服务器**存储或修改一个资源**，并用Request-UR作为其标识 |
| **delete**   | 请求服务器**删除**Request-UR所标识的资源                   |
| **trace**    | 请求服务器**回复收到的请求信息**，主要用于测试             |
| **connect**  | 保留将来使用                                                     |
| **opptions** | 请求查询服务器的性能，或者查询与资源相关的选项和需求             |

### **请求头 Header**

包含一些对消息的描述信息，格式是**`<field>`:`<value>`**。具体地，各种消息头又被分为四大类：**通用头、请求头、响应头**（用于响应消息）和**实体头**。

[鲜为人知的HTTP协议头字段详解大全 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/34908942)

[HTTP头部详解-CSDN博客](https://blog.csdn.net/sinat_34166518/article/details/83584910)

[HTTP请求头和响应头详解 - 简书 (jianshu.com)](https://www.jianshu.com/p/9a68281a3c84)

不想写啦！(╥﹏╥)

## **RESPONSE :响应**

**HTTP响应**

也由四个部分组成，分别是：

**状态行、消息报头、空行和响应正文**

```bash
#状态行

HTTP/1.1 200 0K
#消息头部
Date: Sat, 31 Dec 2005 23:59:59 GMT
Content-Type: text/html;charset=ISO-8859-1
Content-Length: 122
#空行

#响应正文
<!html>
<head>
<title>Wrox Homepage</title>
</head>
<body>
<!-- body goes here -->
</body>
</html>
```

**HTTP状态码:**

| 状态码  | 含义                                                                 |
| ------- | -------------------------------------------------------------------- |
| 100~199 | 表示成功接收请求，要求客户端继续提交下一次请求才能完成整个处理过程   |
| 200~299 | 表示成功接收请求并已完成整个处理过程                                 |
| 300~399 | 为完成请求，客户需进一步细化请求。例如，请求的资源已经移动一个新地址 |
| 400~499 | 客户端的请求有错误                                                   |
| 500~599 | 服务器端出现错误                                                     |

[**HTTP 状态码 | 菜鸟教程 (runoob.com)**](https://www.runoob.com/http/http-status-codes.html)
