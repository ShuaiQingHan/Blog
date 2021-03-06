---
title: 如何理解TCPIP协议？
date: 2021-06-29 20:00
tags: 
		- 计算机网络
		- TCP/IP
---

{% asset_img 123.png This is an example image %}

## 一、是什么
&nbsp;&nbsp;&nbsp;&nbsp;从字面意义上讲，有人可能会认为 TCP/IP 是指 TCP 和 IP 两种协议。实际生活当中有时也确实就是指这两种协议。然而在很多情况下，它只是利用 IP 进行通信时所必须用到的协议群的统称。具体来说，IP 或 ICMP、TCP 或 UDP、TELNET 或 FTP、以及 HTTP 等都属于 TCP/IP 协议。他们与 TCP 或 IP 的关系紧密，是互联网必不可少的组成部分。TCP/IP 一词泛指这些协议，因此，有时也称 TCP/IP 为网际协议群。

&nbsp;&nbsp;&nbsp;&nbsp;互联网进行通信时，需要相应的网络协议，TCP/IP 原本就是为使用互联网而开发制定的协议族。因此，互联网的协议就是 TCP/IP，TCP/IP 就是互联网的协议。

![](https://files.mdnice.com/user/10342/3c26da6f-ae77-40f7-ad60-76ddbbe4a4fe.png)

- TCP（传输控制协议）

一种面向连接的、可靠的、基于字节流的传输层通信协
- IP（网际协议）

用于封包交换数据网络的协议

TCP/IP协议不仅仅指的是<font color=red>TCP</font>和IP两个协议，而是指一个由<font color=red>FTP、SMTP、TCP、UDP、IP</font>等协议构成的协议簇，

只是因为在<font color=#E21918>TCP/IP</font>协议中<font color=#E21018>TCP</font>协议和<font color=#E21918>IP</font>协议最具代表性，所以通称为TCP/IP协议族（英语：TCP/IP Protocol Suite，或TCP/IP Protocols）

<!-- more -->

## 二、划分
TCP/IP协议族按层次分别了五层体系或者四层体系

五层体系的协议结构是综合了 OSI 和 TCP/IP 优点的一种协议，包括应用层、传输层、网络层、数据链路层和物理层

五层协议的体系结构只是为介绍网络原理而设计的，实际应用还是 TCP/IP 四层体系结构，包括应用层、传输层、网络层（网际互联层）、网络接口层

如下图：

![](https://files.mdnice.com/user/10342/f602068b-09c6-4fcc-bc31-a6d3ff2bdd41.png)

## 五层体系
#### 应用层
- 应用层(application layer)：是体系结构中的最高。直接为用户的应用进程提供服务。
- 在因特网中的应用层协议很多，如支持万维网应用的HTTP协议，支持电子邮件的SMTP协议，支持文件传送的FTP协议等等。

如：<font color=red>FTP、Telnet、DNS、SMTP</font>等

#### 传输层
- 运输层(transport layer)：负责向两个主机中进程之间的通信提供服务。由于一个主机可同时运行多个进程，因此运输层有复用和分用的功能。
- 复用，就是多个应用层进程可同时使用下面运输层的服务。
- 分用，就是把收到的信息分别交付给上面应用层中相应的进程。
- 运输层主要使用以下两种协议：
  - (1) 传输控制协议TCP(Transmission Control Protocol)：面向连接的，数据传输的单位是报文段，能够提供可靠的交付。
  - (2) 用户数据包协议UDP(User Datagram Protocol)：无连接的，数据传输的单位是用户数据报，不保证提供可靠的交付，只能提供“尽最大努力交付”。

#### 网络层
#####  网络层(network layer)主要包括以下两个任务：
- 负责为分组交换网上的不同主机提供通信服务。在发送数据时，网络层把运输层残留的报文段或用户数据报封装成分组或包进行传送。在TCP/IP体系中，由于网络层使用IP协议，因此分组也叫做IP数据报，或简称为数据报。
- 选中合适的路由，使源主机运输层所传下来的分组，能够通过网络中的路由器找到目的主机。
#### 数据链路层
数据链路层(data link layer)：常简称为链路层，数据链路层在两个相邻节点传输数据时，将网络层交下来的IP数据报组装成帧，在两个相邻节点之间的链路上传送帧

#### 物理层
物理层(physical layer)：在物理层上所传数据的单位是比特。物理层的任务就是透明地传送比特流。

## 四层体系
TCP/IP 的四层结构则如下表所示：

![](https://files.mdnice.com/user/10342/06bbd8c5-fb4b-4086-90eb-c8141e5d7622.png)
## CP/IP的三次握手，四次分手
首先我们先来了解TCP报文段

![](https://files.mdnice.com/user/10342/c52598ca-f51c-4127-9538-69100e7fa93f.png)

重要的标志我在图中也有标记，重点了解标志位

ACK：确认序号有效

RST：重置连接

SYN：发起了一个新连接

FIN：释放一个连接

三次握手的过程（客户端我们用A表示，服务器端用B表示）

前提：A主动打开，B被动打开

![](https://files.mdnice.com/user/10342/a5dd41a2-d555-44e8-bb19-d9234cc9900d.png)

1、在建立连接之前，B先创建TCB（传输控制块），准备接受客户进程的连接请求，处于LISTEN（监听）状态

2、A首先创建TCB，然后向B发出连接请求，SYN置1，同时选择初始序号seq=x，进入SYN-SEND（同步已发送）状态

3、B收到连接请求后向A发送确认，SYN置1，ACK置1，同时产生一个确认序号ack=x+1。同时随机选择初始序号seq=y，进入SYN-RCVD（同步收到）状态

4、A收到确认连接请求后，ACK置1，确认号ack=y+1，seq=x+1，进入到ESTABLISHED（已建立连接）状态。向B发出确认连接，最后B也进入到ESTABLISHED（已建立连接）状态。

简单来说，就是

1、建立连接时，客户端发送SYN包（SYN=i）到服务器，并进入到SYN-SEND状态，等待服务器确认

2、服务器收到SYN包，必须确认客户的SYN（ack=i+1）,同时自己也发送一个SYN包（SYN=k）,即SYN+ACK包，此时服务器进入SYN-RECV状态

3、客户端收到服务器的SYN+ACK包，向服务器发送确认报ACK（ack=k+1）,此包发送完毕，客户端和服务器进入ESTABLISHED状态，完成三次握手


在此穿插一个知识点就是SYN攻击，那么什么是SYN攻击？发生的条件是什么？怎么避免？

&nbsp;&nbsp;&nbsp;&nbsp;在三次握手过程中，Server发送SYN-ACK之后，收到Client的ACK之前的TCP连接称为半连接（half-open connect），此时Server处于SYN_RCVD状态，当收到ACK后，Server转入ESTABLISHED状态。SYN攻击就是 Client在短时间内伪造大量不存在的IP地址，并向Server不断地发送SYN包，Server回复确认包，并等待Client的确认，由于源地址 是不存在的，因此，Server需要不断重发直至超时，这些伪造的SYN包将产时间占用未连接队列，导致正常的SYN请求因为队列满而被丢弃，从而引起网 络堵塞甚至系统瘫痪。SYN攻击时一种典型的DDOS攻击，检测SYN攻击的方式非常简单，即当Server上有大量半连接状态且源IP地址是随机的，则可以断定遭到SYN攻击了，使用如下命令可以让之现行：
```
  #netstat -nap | grep SYN_RECV
```
四次分手的过程（客户端我们用A表示，服务器端用B表示）

由于TCP连接时是全双工的，因此每个方向都必须单独进行关闭。这一原则是当一方完成数据发送任务后，发送一个FIN来终止这一方向的链接。收到一个FIN只是意味着这一方向上没有数据流动，既不会在收到数据，但是在这个TCP连接上仍然能够发送数据，知道这一方向也发送了FIN，首先进行关闭的一方将执行主动关闭，而另一方则执行被动关闭。

前提：A主动关闭，B被动关闭

![](https://files.mdnice.com/user/10342/5a75f6af-7a81-4a1e-8e94-07fc409a7454.png)


有人可能会问，为什么连接的时候是三次握手，而断开连接的时候需要四次挥手？

这是因为服务端在LISTEN状态下，收到建立连接请求的SYN报文后，把ACK和SYN放在一个报文里发送给客户端。而关闭连接时，当收到对方的FIN 报文时，仅仅表示对方不再发送数据了但是还能接收数据，己方也未必全部数据都发送给对方了，所以己方可以立即close，也可以发送一些数据给对方后，再 发送FIN报文给对方来表示同意现在关闭连接，因此，己方ACK和FIN一般都会分开发送。


  1、A发送一个FIN，用来关闭A到B的数据传送，A进入FIN_WAIT_1状态。
2、B收到FIN后，发送一个ACK给A，确认序号为收到序号+1（与SYN相同，一个FIN占用一个序号），B进入CLOSE_WAIT状态。
3、B发送一个FIN，用来关闭B到A的数据传送，B进入LAST_ACK状态。
4、A收到FIN后，A进入TIME_WAIT状态，接着发送一个ACK给B，确认序号为收到序号+1，B进入CLOSED状态，完成四次挥手。
#### 简单来说就是
1、客户端A发送一个FIN，用来关闭客户A到服务器B的数据传送（报文段4）。

2、服务器B收到这个FIN，它发回一个ACK，确认序号为收到的序号加1（报文段5）。和SYN一样，一个FIN将占用一个序号。

3、服务器B关闭与客户端A的连接，发送一个FIN给客户端A（报文段6）。

4、客户端A发回ACK报文确认，并将确认序号设置为收到序号加1（报文段7）。

#### A在进入到TIME-WAIT状态后，并不会马上释放TCP，必须经过时间等待计时器设置的时间2MSL（最长报文段寿命），A才进入到CLOSED状态。为什么？

1、为了保证A发送的最后一个ACK报文段能够到达B

2、防止“已失效的连接请求报文段”出现在本连接中
## 三、总结
OSI 参考模型与 TCP/IP 参考模型区别如下：

- 相同点：

  - OSI 参考模型与 TCP/IP 参考模型都采用了层次结构
  - 都能够提供面向连接和无连接两种通信服务机制
- 不同点：

  - OSI 采用的七层模型；TCP/IP 是四层或五层结构

  - TCP/IP 参考模型没有对网络接口层进行细分，只是一些概念性的描述；OSI 参考模型对服务和协议做了明确的区分

  - OSI 参考模型虽然网络划分为七层，但实现起来较困难。TCP/IP 参考模型作为一种简化的分层结构是可以的

  - TCP/IP协议去掉表示层和会话层的原因在于会话层、表示层、应用层都是在应用程序内部实现的，最终产出的是一个应用数据包，而应用程序之间是几乎无法实现代码的抽象共享的，这也就造成 OSI 设想中的应用程序维度的分层是无法实现的

三种模型对应关系如下图所示：


![](https://files.mdnice.com/user/10342/87ea878a-f4ed-4184-89ee-2b22ab7e125e.png)