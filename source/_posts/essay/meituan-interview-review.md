---
title: 美团暑期实习后端面试记录
date: 2022-03-23 16:18:11
categories:
- 随笔
sticky: -1
---

# 美团暑期实习后端面试记录

寄了，太紧张了，很多基础八股文没想起来。

## 项目

+ 项目相关，难点，如何解决

## 编程题

+ 二叉树层序遍历打印
+ 反转链表一个区间

## 操作系统

+ 什么是临界区
    + 临界资源：同一时间只允许一个进程使用的共享资源
    + 对临界资源进行访问的那段代码称为临界区。为了互斥访问临界资源，每个进程在进入临界区之前，需要先进行检查
    + 使用临界区时，一般不允许其运行时间过长，只要运行在临界区的线程还没有离开，其他所有进入此临界区的线程都会被挂起而进入等待状态
+ 进程间通信有哪些
    + 管道：只能在父子进程或者兄弟进程中使用
    + 命名管道（FIFO）：去除了管道只能在父子进程中使用的限制
    + 消息队列
        + 可以独立于读写进程存在
        + 避免了 FIFO 的同步阻塞问题，即进程把消息放入队列就能继续运行
        + 读进程可以根据消息类型有选择地接收消息
    + 信号量 / 互斥量：信号量等于 0 时休眠，为多个进程提供对共享数据对象的访问
    + 共享储存
        + 允许多个进程共享一个给定的存储区
        + 需要用信号量同步
        + 多个进程可以使用同一个文件的方式实现共享内存
    + 套接字：可以用于不同机器的通信
+ 死锁的四个必要条件
    + 互斥：资源不能共享
    + 不可抢占：已经分配的资源不能被抢占
    + 占用并等待：已经得到资源的进程可以继续申请新的资源
    + 环路等待：系统中若干进程组成环路，该环路中每个进程都在等待相邻进程正占用的资源
+ 满足了这四个条件就一定会发生死锁吗：不一定
+ 怎么避免死锁
    + 在程序运行时对即将进入的状态判断，拒绝进入不安全的状态
    + 安全状态：如果没有死锁发生，并且即使所有进程突然请求对资源的最大需求，也仍然存在某种调度次序能够使得每一个进程运行完毕，则称该状态是安全的
+ 怎么预防死锁
    + 破坏四个必要条件之一
+ 为什么要加锁
    + 使共享资源同一时间只能由一个进程访问，避免出错

## 计算机网络

+ TCP 是怎么保证可靠传输的
    + 超时重传-确认机制：保证包不会丢失
    + 首部校验和：保证包不会传输出错
    + 流量控制：接收方告诉发送方发送窗口的大小，避免接收方因缓存不足而丢包
    + 拥塞控制：降低整个网络的拥挤程度
+ 浏览器输入网址后发生了什么
+ 数据是如何根据 IP 地址发送到目标主机的
+ 怎么追踪分组到目的地经过了多少跳：traceroute
    + 发送无法交付的 UDP 
    + 从 TLL = 1 开始依次增加 TTL，如果超时就增加 TTL
    + 直到返回 ICMP 终点不可达差错报文

## MySQL

+ MySQL 用的什么索引：B+ 树
+ 为什么要用 B+ 树，不用普通的二叉树红黑树哈希索引
    + 二叉树、红黑树都是二叉树，相同的数据树的高度会更高，磁盘 IO 次数更多，B+ 树是多路树
    + 哈希索引是无序的，不能部分查找或范围查找，无法用于排序与分组
+ 为什么不用 B 树
    + 磁盘一次会读入一整个块，树的每个节点都会使用一整个块的内存，**B+ 树的内部节点只储存索引，不储存值**，同样的内存空间大小下能储存更多的索引，树高更低
    + B+ 树叶子节点是有序链表且包含了父节点，区间查找更加方便（B 树的父节点在内部节点中，查找一个区间需要中序遍历）
    + B+ 树查询时间稳定，因为数据都只储存在叶节点中
