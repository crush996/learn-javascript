# 输入 URL 到页面呈现

## 整体过程

1. `DNS`解析
2. `TCP`连接
3. `HTTP`请求
4. 服务器响应
5. 浏览器解析渲染页面

## DNS 解析

`DNS`解析过程就是通过网络查找哪台机器有你需要的资源的过程。  
互联网上每一台计算机的唯一标识是它的 IP 地址，但是 IP 地址并不方便记忆，所以互联网设计者为了方便，设计出了域名。

-   **DNS 解析过程**

1. 查询`www.baidu.com`
2. 访问客户端 DNS 缓存：**浏览器缓存 -> 系统缓存(host) -> 路由器缓存**
3. 访问\_\_ISP DNS 服务器(ISP,互联网服务提供商)，如果本地服务器有，则直接返回；如果没有，让本地 DNS 服务器去咨询查找
4. 本地去咨询 **DNS 根服务器** ，DNS 根服务器发现是`.com区域`管理的，告诉本地去咨询它
5. 本地去咨询 **.com 顶级域名服务器** ，.com 顶级域名服务器不太清楚，告诉本地去咨询 `baidu.com 主区域` 的服务器。
6. 本地去咨询 **baidu.com 主域名服务器** ，baidu.com 域服务器查找到对应的 IP 地址，返回给本地
7. 本地服务器通知用户，`baidu.com`对应的 IP 地址，同时缓存这个 IP

## TCP 连接

-   建立连接阶段：3 次握手。建立客户端和服务器之间的连接
-   传输数据阶段
-   断开连接阶段：4 次握手。断开客户端和服务器之间的连接

## 发送 HTTP 请求

发送`HTTP`请求的过程就是构建`HTTP`请求报文，并通过`TCP`协议发送到服务器指定端口(`HTTP`协议默认端口`80/8080`，`HTTPS`协议默认端口`443`)

`HTTP`请求报文由 3 部分组成：**请求行、请求报文和请求正文** 。

-   **请求行**：常用的方法有：GET、POST、PUT、DELETE、OPTIONS、HEAD
-   **请求报头**：允许客户端向服务器传递请求的附加信息和客户端自身的信息
-   **请求正文**：通过 POST、PUT 等方法时，通常需要客户端向服务器传递数据，这些数据就储存在请求正文中

> 当然，`HTTP`请求需要注意是否跨域。

## 服务器响应

服务器处理请求完毕后，会返回`HTTP`报文。  
`HTTP`响应报文也是由 3 部分组成：**状态码、响应报头和响应报文**。

-   **状态码：** `1xx`指示信息——表示请求已接收；`2xx`请求成功——表示请求成功接收并解析；`3xx`重定向——表示要完成请求需要更进一步操作；
    `4xx`客户端错误——请求有语法错误或者无法实现；`5xx`服务器端错误。
    -   常见的状态码：200（成功）、304（请求内容有缓存，不需要更新）、404（网页或者文件找不到）、500（服务器-后端处理错误）
-   **响应报头：** 常见的响应报头字段`Server`、`Connection`等
-   **响应报文：** 服务器返回给浏览器的文本信息，通常 HTML、CSS、JS、图片等文件就放在这一部分

## 浏览器解析渲染页面

-   解析 HTML 构建 DOM(DOM 树)，并行请求 css/image/js
-   CSS 文件下载完成，开始构建 CSSOM(CSS 树)
-   CSS 树构建完成后和 DOM 树一起生成 Render Tree(渲染树)
-   布局(Layout)：计算出每个节点在屏幕中的位置
-   显示(Painting)：通过显卡把页面画到屏幕上
