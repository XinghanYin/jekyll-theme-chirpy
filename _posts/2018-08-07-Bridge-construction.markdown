---
title: "大桥施工笔记"
author: xy
date: 2018-08-07 00:00:00 +0800
categories: [Archive]
tags: [Codes]
img_path: /images/Archive
---

鉴于某些不可描述的原因，科学上网的路越来越窄，笔者不得不自己搭桥。

为了以防记忆丧失，无法正确使用大桥，便写下这篇笔记。

 ---

已于2019年8月23日更新
SSR部署脚本（CentOS6/Debian6/Ubuntu14 ）：
```
yum -y install wget

wget –no-check-certificate https://freed.ga/github/shadowsocksR.sh; bash shadowsocksR.sh
```
SSR管理界面命令：
```
bash ssr.sh
```
锐速安装
（只支持 CentOS6 x64 及 CentOS7 x64 系统，不支持任何 Debian & Ubuntu 系统）

用Xshell连接服务器后，执行下面命令。
uname -r
回车后输出当前系统内核版本。主要分三种情况：

1、结果以 2 开头，例如 2.6.32-696.18.7.el6.x86_64。

这种输出结果说明我们的服务器为 CentOS6 x64 系统，大家直接查看第三步进行锐速安装即可。

2、结果以 3 开头，例如 3.10.0-693.11.6.el7.x86_64。

这种输出结果说明我们的服务器为 CentOS7 x64 系统，大家直接查看第四步进行锐速安装即可。

3、结果以 4 开头，例如 4.12.10-1.el7.elrepo.x86_64。

这种输出结果说明我们的服务器已经安装 Google BBR 拥塞控制算法，此时已经无法继续安装锐速。

CentOS6 x64 系统安装锐速
若确定服务器为 CentOS6 x64 系统则看这一步。

按照下图提示，我们继续复制下列命令：
```
wget --no-check-certificate -O appex.sh
https://raw.githubusercontent.com/hombo125/doubi/master/appex.sh
&& bash appex.sh install '2.6.32-642.el6.x86_64'
 ```
CentOS7 x64 系统安装锐速
若确定服务器为 CentOS7 x64 系统则看这一步。

按照下图提示，我们继续复制下列命令：
```
wget --no-check-certificate -O rskernel.sh
https://raw.githubusercontent.com/hombo125/doubi/master/rskernel.sh
&& bash rskernel.sh
```
等待内核更换完毕后系统会自动重启并断开连接。然后重新连接，执行下面命令。
```
yum install net-tools -y && wget -- no-check-certificate -O appex.sh
https://raw.githubusercontent.com/0oVicero0/serverSpeeder_Install/master/appex.sh
&& bash appex.sh install
```

若系统选择是CentOS6 x64，不需要更换内核，直接执行下列安装命令

```
wget -- no-check-certificate -O appex.sh https://raw.githubusercontent.com/0oVicero0/serverSpeeder_Install/master/appex.sh
&& bash appex.sh install '2.6.32-642.el6.x86_64'
```
安装步骤一路回车就行了。