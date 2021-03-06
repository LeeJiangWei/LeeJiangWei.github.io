---
title: 阿里暑期实习后端面试记录
date: 2022-03-24 20:18:11
categories:
- 随笔
sticky: -1
---

# 阿里暑期实习后端面试记录

## 项目

+ 项目相关，难点，如何解决

## 操作系统

+ 进程和线程是什么，区别
+ 进程间通信有哪几种
+ 为什么操作系统要用用户态和内核态
    + 在内核态下，进程运行在内核地址空间中，此时 CPU 可以执行任何指令。运行的代码也不受任何的限制，可以自由地访问任何有效地址，也可以直接进行端口的访问。
    + 在用户态下，进程运行在用户地址空间中，被执行的代码要受到 CPU 的诸多检查，它们只能访问映射其地址空间的页表项中规定的在用户态下可访问页面的虚拟地址，且只能对任务状态段(TSS)中 I/O 许可位图(I/O Permission Bitmap)中规定的可访问端口进行直接访问
    + 通过区分内核空间和用户空间的设计，隔离了操作系统代码(操作系统的代码要比应用程序的代码健壮很多)与应用程序代码。即便是单个应用程序出现错误也不会影响到操作系统的稳定性，这样其它的程序还可以正常的运行
    + **区分内核空间和用户空间本质上是要提高操作系统的稳定性及可用性**

## 计算机网络

+ 三次握手过程，两次握手可以吗
+ HTTP 和 HTTPS 的区别

## 数据库

+ 介绍 B 树，B+ 树，B* 树
+ MySQL 有哪些索引
+ 对区分度不高的列（例如性别）可以建立索引吗，怎么建立索引
    + 不适合，区分度越低，索引效果越差

## Redis

+ 五种数据类型及底层的实现有了解吗
+ 为什么 ZSET 用跳跃表不用红黑树
+ 内存淘汰策略

## 设计模式

+ 单例模式等

## 场景题

+ 几十亿个无序正整数互不重复，储存在磁盘中，电脑内存不够大没有办法一次都进来，现在要查找几个数是否在这之中，有什么方法做到，复杂度 O(logn)
    + 利用二进制位建立类似二叉树结构（文件储存）
    + 布隆过滤器