---
layout: post
title: '华为HCNA笔记-TO-BE-CONTINUED'
excerpt: 华为HCNA笔记,视频学习地址https://www.bilibili.com/video/av10177237
date: 2018-05-31
categories: 广电
tags: HCNA
---


# 第三讲 

## ICMP协议  因特网控制报文协议

### 数据包格式

以太网头-ip头-icmp-fcs
![](https://youyefu-1251686655.cos.ap-beijing.myqcloud.com/18-5-31/57706916.jpg)

```flow
Type表示消息类型
code表示同意消息类型的不同信息
Checksum检验和  检测报文是否被篡改
```

### 用途

1测试连通性
Ping：echo request  echo reply
![](https://youyefu-1251686655.cos.ap-beijing.myqcloud.com/18-5-31/45920494.jpg)
2错误报告
如上图，如不可达，会告诉你为什么不可达
网络部可达：路由器没有去向目地网络的
主机不可达：网络中找不到对应的主机
协议不可达：能找到主机，但没有找到四层的协议
端口不可达：以上都能识别，但端口对应的应用不可达

### Icmp重定向

![](https://youyefu-1251686655.cos.ap-beijing.myqcloud.com/18-5-31/36910573.jpg)

如果访问服务器A本来第一跳是RTB 但RTB会重定向让PCa的第一跳直接跳到RTA

源地址ping
R1-R2
1.1.1.1
2.2.2.2

在R1上ping
Cisco：ping 2.2.2.2 source 1.1.1.1
Huawei:ping -a 1.1.1.1 2.2.2.2
![](https://youyefu-1251686655.cos.ap-beijing.myqcloud.com/18-5-31/36118629.jpg)
-t默认是 2000 毫秒 内如果应答了 就是ping 成功了 

TraceRT 路由跟踪 比ping更好用更详细

### ARP协议

解决再以太网环境中 二三层映射问题 只能再ipv4环境下工作
![](https://youyefu-1251686655.cos.ap-beijing.myqcloud.com/18-5-31/72520255.jpg)
Operation code 请求是1 应答是2

### Arp代理

一般由路由器实现
有不同网关的情况下通过代理可以连通

原理是有路由器里的arp表回复给不同网段的arp请求
路由器会假装是被访问的pc 回复arp
![](https://youyefu-1251686655.cos.ap-beijing.myqcloud.com/18-5-31/92724397.jpg)
![](https://youyefu-1251686655.cos.ap-beijing.myqcloud.com/18-5-31/18363688.jpg)
功能：
1检测地址冲突
2 更新新ip地址arp映射

#### Arp攻击

用第二特性实现的，攻击者利用其特性
![](https://youyefu-1251686655.cos.ap-beijing.myqcloud.com/18-5-31/88314754.jpg)

### 传输协议TCP UDP

TCP面向连接的可靠协议 点到点协议 单播
UDP无连接 尽力而为的协议
![](https://youyefu-1251686655.cos.ap-beijing.myqcloud.com/18-5-31/21266680.jpg)
![](https://youyefu-1251686655.cos.ap-beijing.myqcloud.com/18-5-31/50957191.jpg)
![](https://youyefu-1251686655.cos.ap-beijing.myqcloud.com/18-5-31/54820194.jpg)
p.s. : Ddos 不断的更新ip后发送tcp 导致服务器内存满 
![](https://youyefu-1251686655.cos.ap-beijing.myqcloud.com/18-5-31/35540489.jpg)
Udp没有序列 所以要使用 rtp实时传输协议 12byte
比如voip就是用udp发送的，发送前经过四次封装
Layer|ip|UDP|rtp|Voip

## 第四讲

### Vrp基础

Vrp是华为的平台 类似cisico 的ios  都是基于unix
设备：
1层设备集线器：1信号放大 2数据泛洪 已经淘汰了
2层 交换机：2层
Mls3层
3层 路由器


广播域 是星型拓扑


路由器
直连路由：
1up up 物理层 数据链路层 
2接口要有正常的ip和子网掩码
非直连路由：
1静态路由
2动态路由选择协议 RIP EIGRP OSPF ISIS BGP	
![](https://youyefu-1251686655.cos.ap-beijing.myqcloud.com/18-5-31/51434180.jpg)
Vty线路接口 远程登录 只有五个  只能有五个管理员进行远程登录
user-interface vty 0 4 开启0-4 五个终端接口

基本查询命令：
Dir：查看flash里的文件
Mkdir 新建文件夹
Rmdir 删除文件夹
Copy move rename

Delete
Undelete
Reset recycle-bin
![](https://youyefu-1251686655.cos.ap-beijing.myqcloud.com/18-5-31/34961120.jpg)
![](https://youyefu-1251686655.cos.ap-beijing.myqcloud.com/18-5-31/88544074.jpg)
![](https://youyefu-1251686655.cos.ap-beijing.myqcloud.com/18-5-31/50441450.jpg)

### 设备升级

![](https://youyefu-1251686655.cos.ap-beijing.myqcloud.com/18-5-31/55741308.jpg)
Reboot后要n y


## 第五讲

### 交换机基础

内容可寻址存储系统 ：mac表

贯穿式转发：三层报头的目地ip地址 看二层帧头和三层报头 直接转发 效率高 但可能被篡改
无分片转发：成功率较低，保证数据完整
存储转发：查看帧的全部字段  ，存储后转发，对于qos支持好

![](https://youyefu-1251686655.cos.ap-beijing.myqcloud.com/18-5-31/25536444.jpg)
例子：
![](https://youyefu-1251686655.cos.ap-beijing.myqcloud.com/18-5-31/98221752.jpg)
Pc-a 要和pc-c通信 
a通过广播的形式到交换机接口，交换机学习到a的mac地址 所属vlan 
![](https://youyefu-1251686655.cos.ap-beijing.myqcloud.com/18-5-31/32989956.jpg)
![](https://youyefu-1251686655.cos.ap-beijing.myqcloud.com/18-5-31/69428282.jpg)
c接受到泛洪的数据 回复arp
![](https://youyefu-1251686655.cos.ap-beijing.myqcloud.com/18-5-31/86284366.jpg)
以下三个监听协议协助泛洪：增强转发组播效率
IGMP snooping
IGMP snooping proxy
CGMP

### STP原理与配置

[生成树协议动画](https://youyefu.github.io/2018/05/31/STP%E7%94%9F%E6%88%90%E6%A0%91%E5%8D%8F%E8%AE%AE%E5%8A%A8%E7%94%BB%E6%BC%94%E7%A4%BA.html)
![](https://youyefu-1251686655.cos.ap-beijing.myqcloud.com/18-5-31/35113339.jpg)

多条路径可走：如果两个交换机 连了两根线，其中没有配置stp 泛洪的流量会来回跑，形成环路，变成广播风暴
![](https://youyefu-1251686655.cos.ap-beijing.myqcloud.com/18-5-31/36290261.jpg)

 Ieee 控制层面协议
802.1d  stp 平时不用
802.1w rstp 快速生成树 收敛速度快
802.1s mstp/mist/mst 多进程生成树
产生的报文叫BPDU
![](https://youyefu-1251686655.cos.ap-beijing.myqcloud.com/18-5-31/90194617.jpg)
 
产生风暴最明显的特征是一个mac出现对应了多个端口
![](https://youyefu-1251686655.cos.ap-beijing.myqcloud.com/18-5-31/53015607.jpg)
```flow
生成树关注三点
1如何确保阻塞的是不重要的路径
2如何确保网络是通的
3如果之前的线路有问题，怎么高校的切换路径
```
![](https://youyefu-1251686655.cos.ap-beijing.myqcloud.com/18-5-31/11150174.jpg)

跟桥（根交换机）：树根只有一个
根与非根的路径是根端口
R根端口 Dp指定端口 NDP非指定端口
 
BPDU有两类
1配置BPDU
2tcn BPDU（特殊情况特殊需求下使用）
 
802.3|BPDU|

![](https://youyefu-1251686655.cos.ap-beijing.myqcloud.com/18-5-31/61054400.jpg)

Root id:根网桥的标识符
2byte优先级字段 0-35535
6byte mac地址
Cost of path 路径开销 描述路径好坏的参数
 
Stp过程
1 接口没有运行stp down状态
2 blocking 不能收发任何数据，接受BPDU 不能转发
3 listening 不能收发任何数据，可以接受和转发bPDU
4 learning 同上 且接收数据可以基于源mac地址进行mac地址表项的学习
5 forwarding 可以任意收发数据流量 bpdu mac表项

![](https://youyefu-1251686655.cos.ap-beijing.myqcloud.com/18-5-31/37797412.jpg)

1选跟桥 bid mac
2根端口 rid cop bid pid 自身pid
3指定端口 rid cop bid pid
 
RSTP 原理和配置
Stp是整体性收敛协议 RSTP两台交换机之间分段收敛 
非指定端口分为backup 和alternate 
RSTP边缘端口：
![](https://youyefu-1251686655.cos.ap-beijing.myqcloud.com/18-5-31/60335.jpg)
![](https://youyefu-1251686655.cos.ap-beijing.myqcloud.com/18-5-31/42773626.jpg)
![](https://youyefu-1251686655.cos.ap-beijing.myqcloud.com/18-5-31/3671235.jpg)
Stp root p设置主根桥
Stp root s 设置备份跟桥
Stp port p设置主根端口
Stp port s 设置备份根端口

## 第七讲：Ip路由基础

自治系统：autonomous system。在互联网中，一个自治系统(AS)是一个有权自主地决定在本系统中应采用何种路由协议的小型单位。这个网络单位可以是一个简单的网络也可以是一个由一个或多个普通的网络管理员来控制的网络群体，它是一个单独的可管理的网络单元（例如一所大学，一个企业或者一个公司个体）。一个自治系统有时也被称为是一个路由选择域（routing domain）。一个自治系统将会分配一个全局的唯一的16位号码，有时我们把这个号码叫做自治系统号（ASN） 

一个自治系统就是处于一个管理机构控制之下的路由器和网络群组。它可以是一个路由器直接连接到一个LAN上，同时也连到Internet上；它可以是一个由企业骨干网互连的多个局域网。在一个自治系统中的所有路由器必须相互连接，运行相同的路由协议，同时分配同一个自治系统编号。自治系统之间的链接使用外部路由协议，例如BGP.。

技术定义
互联网协议指南给自治系统提出了如上的的定义后，又提出了一个更具有技术性的定义如下：

一个自治系统即为由一个或多个网络运营商来运行一个或多个网络协议前缀的网络连接组合，这些运营商往往都具有单独的定义明确的路由策略

1-64511 公有
64512-65535私有
 
静态路由基础：
告诉指定地址该怎么走 不灵活