# SocketDemo

## 1、Socket 编程

### 1.1 Server 的生命周期大致如下：

1. 创建socket
2. 绑定（bind）地址端口
3. 监听网络连接
4. 接受连接
5. 关闭连接

### 1.2 Clinet 的生命周期则稍微简单点：

1. 创建socket
2. 绑定地址
3. 发起连接
4. 关闭连接

## 2、Socket 通信 TCP 三次握手

1. 客户端发送一个握手包(SYN Seq)，第一次握手，客户端连接状态为 SYS_SEND
2. 服务端端有响应，并发送一个(SYN, ACK)的应答包， 第二次握手 客户端的状态都变成ESTABLISHED表示可以发送数据了
3. 客户端再向服务端发送（ACK）应答包，第三次握手，建立TCP连接，服务端也可以发送数据。
4. 客户端发送一个[FIN, ACK]的包，表示关闭连接。
5. 服务端发送一个[ACK]包表示确定关闭客户端到服务端的连接。客户端到服务端的连接断了。服务端到客户端的连接还保持
