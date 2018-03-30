1. NIO和BIO：NoneBlocking IO,Blocking IO

2. 传统发的HTTP服务器原理
    1. 创建一个ServerSocket,监听并绑定一个端口
    2. 一系列客户端来请求这个端口
    3. 服务器使用Accept,获得一个来自客户端的Socket连接对象
    4. 编码协议，将结果序列化字节流
    5. 写Socket，将字节流发给客户端
    循环循环....

3. HTTP服务器之所以称为HTTP服务器，是因为编码解码协议是HTTP协议。

4. Apache处理请求：传统的多线程服务器，过程如2所述

5. 高性能，事件驱动，异步
