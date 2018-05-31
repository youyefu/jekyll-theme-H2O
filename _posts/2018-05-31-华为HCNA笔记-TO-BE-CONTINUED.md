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
![](http://p94dvrayw.bkt.clouddn.com/18-5-31/57706916.jpg)

```flow
Type表示消息类型
code表示同意消息类型的不同信息
Checksum检验和  检测报文是否被篡改
```

### 用途

1测试连通性
Ping：echo request  echo reply
![](http://p94dvrayw.bkt.clouddn.com/18-5-31/45920494.jpg)
2错误报告
如上图，如不可达，会告诉你为什么不可达
网络部可达：路由器没有去向目地网络的
主机不可达：网络中找不到对应的主机
协议不可达：能找到主机，但没有找到四层的协议
端口不可达：以上都能识别，但端口对应的应用不可达

### Icmp重定向

![](http://p94dvrayw.bkt.clouddn.com/18-5-31/36910573.jpg)

如果访问服务器A本来第一跳是RTB 但RTB会重定向让PCa的第一跳直接跳到RTA

源地址ping
R1-R2
1.1.1.1
2.2.2.2

在R1上ping
Cisco：ping 2.2.2.2 source 1.1.1.1
Huawei:ping -a 1.1.1.1 2.2.2.2
![](http://p94dvrayw.bkt.clouddn.com/18-5-31/36118629.jpg)
-t默认是 2000 毫秒 内如果应答了 就是ping 成功了 

TraceRT 路由跟踪 比ping更好用更详细

### ARP协议

解决再以太网环境中 二三层映射问题 只能再ipv4环境下工作
![](http://p94dvrayw.bkt.clouddn.com/18-5-31/72520255.jpg)
Operation code 请求是1 应答是2

### Arp代理

一般由路由器实现
有不同网关的情况下通过代理可以连通

原理是有路由器里的arp表回复给不同网段的arp请求
路由器会假装是被访问的pc 回复arp
![](http://p94dvrayw.bkt.clouddn.com/18-5-31/92724397.jpg)
![](http://p94dvrayw.bkt.clouddn.com/18-5-31/18363688.jpg)
功能：
1检测地址冲突
2 更新新ip地址arp映射

#### Arp攻击

用第二特性实现的，攻击者利用其特性
![](http://p94dvrayw.bkt.clouddn.com/18-5-31/88314754.jpg)

### 传输协议TCP UDP

TCP面向连接的可靠协议 点到点协议 单播
UDP无连接 尽力而为的协议
![](http://p94dvrayw.bkt.clouddn.com/18-5-31/21266680.jpg)
![](http://p94dvrayw.bkt.clouddn.com/18-5-31/50957191.jpg)
![](http://p94dvrayw.bkt.clouddn.com/18-5-31/54820194.jpg)
p.s. : Ddos 不断的更新ip后发送tcp 导致服务器内存满 
![](http://p94dvrayw.bkt.clouddn.com/18-5-31/35540489.jpg)
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
![](http://p94dvrayw.bkt.clouddn.com/18-5-31/51434180.jpg)
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
![](http://p94dvrayw.bkt.clouddn.com/18-5-31/34961120.jpg)
![](http://p94dvrayw.bkt.clouddn.com/18-5-31/88544074.jpg)
![](http://p94dvrayw.bkt.clouddn.com/18-5-31/50441450.jpg)

### 设备升级

![](http://p94dvrayw.bkt.clouddn.com/18-5-31/55741308.jpg)
Reboot后要n y


## 第五讲

### 交换机基础

内容可寻址存储系统 ：mac表

贯穿式转发：三层报头的目地ip地址 看二层帧头和三层报头 直接转发 效率高 但可能被篡改
无分片转发：成功率较低，保证数据完整
存储转发：查看帧的全部字段  ，存储后转发，对于qos支持好

