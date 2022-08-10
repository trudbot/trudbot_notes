# 什么是网络编程？
网络编程：使用编程语言实现多台计算机的通信。

# 网络编程三大要素。
    1. IP地址：网络中每一台计算机的唯一标识，通过IP地址找到指定的计算机。
    
    2. 端口：用于标识进程的逻辑地址，通过端口找到指定进程。
    
    3. 协议：定义通信规则，符合协议则可以通信，不符合不能通信

## IP地址
**IP地址**：是网络中计算机的唯一标识，通过IP地址可以找到指定计算机。

　假如有一个192.168.26.254 的IP地址，它在网络中其实是这样用四个字节表示的：11000000 10101000 00011010 11111110，使用0、1表示，而且中间没有点，因为这种表示形式不容易记（还要计算二进制数），所以使用192.168.26.254的形式，这种形式叫做“点分十进制”。也因为一个字节最大值为255，所以组成点分十进制的四个数字每个都不能超过255。

## 端口
用于标识进程的逻辑地址，不同进程使用的端口是不同的，计算机通过端口找到指定进程，有效端口为0~6+5535，其中1~1024是系统使用的端口或保留端口。


## 协议

协议是定义的通信规则，一般有TCP协议和UDP协议。
（1）TCP协议是在通信的两台设备之间建立连接通道，对传输的数据大小没有限制，但是因为建立连接，可靠一些，但是速度会慢一些。TCP协议又称为三次握手协议，因为建立过程有三步，发送请求、获取反馈、建立连接。
通常使用的蓝牙、打电话都是TCP协议。

（2）UDP协议需要将数据打包，因为包有大小，所以对数据大小有限制，UDP是不用建立连接的，不保证待接收方一定会接收到消息，所以不可靠，但是因为不建立连接，速度要快一些。

#### InetAddress
InetAddress是Java中一个对ip地址进行抽象的类

InetAddress没有构造方法， 需通过静态方法获取对象

```
static InetAddress getByAddress(byte[] addr) 给定原始IP地址返回 InetAddress对象。  
static InetAddress getByAddress(String host, byte[] addr) 根据提供的主机名和IP地址创建InetAddress。  
```
常用方法
```
String getHostAddress() 返回文本表示中的IP地址字符串。  
String getHostName() 获取此IP地址的主机名。  
```
```java
public class NetWorkTest {
    public static void main(String[] args) throws UnknownHostException {
        InetAddress ip = InetAddress.getByName("DESKTOP-128NDKM");
        System.out.println(ip.getHostAddress());
        System.out.println(ip.getHostName());
    }
}
/*
192.168.137.1
DESKTOP-128NDKM

*/
```
#### 使用UDP协议发送和接收数据

##### 发送数据
1. 使用 DatagramSocket() 创建一个数据包套接字。
> 套接字（socket）为通信的端点，每个套接字由一个 IP 地址和一个端口号组成。通过网络通信的每对进程需要使用一对套接字，即每个进程各有一个。
2. 使用 DatagramPacket() 创建要发送的数据包。
3. 使用 DatagramSocket 类的 send() 方法发送数据包。
4. 关闭发送端

*创建发送端套接字*
使用java.net包下的DatagramSocket类创建套接字
常用构造方法
```
DatagramSocket() 构造一个数据报套接字并将其绑定到本地主机上的任何可用端口。  
DatagramSocket(int port) 构造一个数据报套接字并将其绑定到本地主机上的指定端口。  

```
*创建数据包*
使用类DatagramPacket创建数据报包
```
DatagramPacket(byte[] buf, int length, InetAddress address, int port) 构造一个数据报包，用于将长度为 length的数据包发送到指定主机上的指定端口号。  
```
数据包不仅要有要发送的数据信息, 还要有接收端套接字的信息
*发送数据包*
```
void send(DatagramPacket p) 从此套接字发送数据报包。  
```
*完整实现*
```java
import java.io.IOException;
import java.net.*;

public class NetWorkTest {
    public static void main(String[] args) throws IOException {
        InetAddress address = InetAddress.getByName("DESKTOP-128NDKM");
        DatagramSocket ds = new DatagramSocket();
        String data = "hello world";
        DatagramPacket dp = new DatagramPacket(data.getBytes(), data.length(), address, 10086);
        ds.send(dp);
        ds.close();
    }
}
```
**接收数据**
1. 使用 DatagramSocket 创建数据包套接字，并将其绑定到指定的端口。
2. 使用 DatagramPacket 创建字节数组来接收数据包。
3. 使用 DatagramPacket 类的 receive() 方法接收 UDP 包。
4. 解析数据
5. 关闭接收端

* 接收端的Socket应指定端口
* packet接收数据需要给定字节数组作为容器
* packet的getdata能获得接收到的数据, getLength获得数据的长度
```java
public class ReceiveTest {
    public static void main(String[] args) throws IOException {
        DatagramSocket ds = new DatagramSocket(10086);
        byte[] data = new byte[1024];
        DatagramPacket dp = new DatagramPacket(data, data.length);
        ds.receive(dp);
        System.out.println("接收到的数据为: " + new String(dp.getData(), 0, dp.getLength()));
    }
}
```

#### 使用TCP协议发送和接收数据

TCP 网络程序是指利用 Socket 编写的通信程序。利用 TCP 协议进行通信的两个应用程序是有主次之分的，一个是服务器程序，一个是客户端程序，两者的功能和编写方法不太一样。其中 ServerSocket 类表示 Socket 服务器端，Socket 类表示 Socket 客户端，两者之间的交互过程如下：
- 服务器端创建一个 ServerSocket（服务器端套接字），调用 accept() 方法等待客户端来连接。
- 客户端程序创建一个 Socket，请求与服务器建立连接。
- 服务器接收客户的连接请求，同时创建一个新的 Socket 与客户建立连接，服务器继续等待新的请求。

**创建客户端**
使用Socket类：该类实现客户端套接字（也称为“套接字”）。Socket 类表示通信双方中的客户端，用于呼叫远端机器上的一个端口，主动向服务器端发送数据（当连接建立后也能接收数据）。 

*构造方法*
- Socket()：无参构造方法。
- Socket(InetAddress address,int port)：创建一个流套接字并将其连接到指定 IP 地址的指定端口。
- Soclcet(InetAddress address,int port,InetAddress localAddr,int localPort)：创建一个套接字并将其连接到指定远程地址上的指定远程端口。
- Socket(String host,int port)：创建一个流套接字并将其连接到指定主机上的指定端口。
- Socket(String host,int port,InetAddress localAddr,int localPort)：创建一个套接字并将其连接到指定远程地址上的指定远程端口。Socket 会通过调用 bind() 函数来绑定提供的本地地址及端口。

*常用方法*
InputStream getInputStream()：返回此套接字的输入流。
OutputStream getOutputStream()：返回此套接字的输出流。
void close()：关闭此套接字。
void shutdownInput() 将此套接字的输入流放在“流结束”。  
void shutdownOutput() 禁用此套接字的输出流。  



