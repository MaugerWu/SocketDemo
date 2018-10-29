# SocketDemo

## 1、Socket 编程

### 1.1 Server 的生命周期：

1. 创建socket
2. 绑定（bind）地址端口
3. 监听网络连接
4. 接受连接
5. 关闭连接

### 1.2 Clinet 的生命周期：

1. 创建socket
2. 绑定地址
3. 发起连接
4. 关闭连接

### 1.3 常用协议默认端口号

|应用程序|FTP|TFTP|TELNET|SMTP|DNS|HTTP|SSH|MYSQL|SQL Server|Oracle|
|:---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|默认端口|20,21|69|23|25|53|80|22|3306|1433|1521|
|传输层协议|TCP|UDP|TCP|TCP|UDP|TCP|||

## 2、Socket 通信 TCP 三次握手

1. 客户端发送一个握手包(SYN Seq)，第一次握手，客户端连接状态为 SYS_SEND
2. 服务端有响应，并发送一个 (SYN, ACK) 的应答包， 第二次握手 客户端的状态都变成 ESTABLISHED 表示可以发送数据了
3. 客户端再向服务端发送 （ACK） 应答包，第三次握手，建立 TCP 连接，服务端也可以发送数据。
4. 客户端发送一个 [FIN, ACK] 的包，表示关闭连接。
5. 服务端发送一个 [ACK] 包表示确定关闭客户端到服务端的连接。客户端到服务端的连接断了。服务端到客户端的连接还保持

## 3、Socket 通信 TCP 四次挥手

1. 客户端发送[FIN]包，表示要断开 clinet->server 的连接。
2. 服务端收到[FIN]之后，发送一个[ACK]包表示确定断开连接啦。
3. 同时服务端也会向客户端再发一个[FIN]包，表示也想断开 server->clinet 的连接。
4. 客户端收到服务端的[ACK]包，确定了 clinet->server 的连接的断开，该连接将不会发送数据啦。由于客户端也会收到服务端的[FIN]包，因此也要为断开 server->clinet 的连接发送[ACK]给服务端确定。至此，四次挥手完成。

## 4、InetAddress 类

&emsp;&emsp;在 Java 应用中 JVM 也会缓存 DNS 的解析结果，这个缓存是在`InetAddress`类中完成的，而且这个缓存时间还比较特殊，它有两种缓存策略：一种是正确解析结果缓存，另一种是失败的解析结果缓存。这两个缓存时间由两个配置项控制，配置项是在`%JAVA_HOME%\lib\security\java.security`文件中配置的。两个配置项分别是：`networkaddress.cache.ttl`和`networkaddress.cache.negative.ttl`，它们的默认值分别是 -1（永不失效）和 10（缓存 10 秒）。

&emsp;&emsp;可以直接修改`java.security`文件中的默认值在 Java 的启动参数中增加`-Dsun.net.inetaddr.ttl=xxx`来修改默认值、通过`InetAddress`类动态修改。

&emsp;&emsp;这里要特别强调一下，如果需要用 InetAddress 类解析域名，必须是单例模式，不然会有严重的性能问题，如果每次都创建 InetAddress 实例，则每次都要进行一次完整的域名解析，非常耗时。

## 5、参考

- [socket.io](https://github.com/TooTallNate/Java-WebSocket)
- [socket](https://www.cnblogs.com/wangcq/p/3520400.html)

