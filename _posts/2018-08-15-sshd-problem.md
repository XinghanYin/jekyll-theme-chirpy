---
title: "sshd连接修复笔记"
author: xy
date: 2018-08-15 18:00:00 +0800
categories: [Archive]
tags: [Codes]
img_path: /images/Archive
---

前言：阿毛这个博客服务器的sshd从几个月前就出现问题，命令只能通过管理控制台自带的SVN去执行，并且是osx自带的ssh和windows的xshell都连不上。这就让人很难受了。

查了很多资料，但是鄙人实在是太菜了，一直没找到是哪里出的问题，重启也重启了，补包也补包了，重装也重装了，甚至还自己写了几个脚本想强行启动，但始终是不行。

所以阿毛就需要找一个解决方案，因为本身就是一个linux小白，加上懒，所以一开始是想通过提交工单解决这个问题的，但是体验很一般（手动掰掰），搁置了很长时间，直到今天才修复。

![sshd_problem](/sshd_problem1.png)

首先，我的ssh包是在的。

![sshd_problem](/sshd_problem2.png)

其次，我的端口也是打开的。

![sshd_problem](/sshd_problem3.png)

但是我试着重启sshd的时候，总会出现这行代码。

```
Job for sshd .service failed because the control process exited with error code. See "systemctl status sshd .service" and " journctl -xe" for details.
```
一开始我并没在意这行信息的主要内容，我在意是为什么会出现这行信息，于是我又花费了很长时间去找包含这行信息的文件。直到今天，我才发现人就让我输入这俩代码自检一下，真是蠢到家了。于是我试着打出了
```journctl -xe
```
和
```systemctl status sshd .service
```
这两行代码，眼前一下就明了了。

![sshd_problem](/sshd_problem4.png)

这样的code大概有三批。这时候我才知道：权限好像放的太开了。。。

于是乎chmod600一下，再重新启动sshd.service。用xshell试一试。

哦，连上了。

![sshd_problem](/sshd_problem5.png)

呵呵。


