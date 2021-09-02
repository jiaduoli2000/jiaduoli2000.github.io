---
title: FydeOS折腾记录
author: 阿狸的Blog
date: '2021-08-26'
slug: FydeOS
categories:
  - 效率工具
tags:
  - FydeOS
---


最近爱折腾的老毛病又犯了，看着家里那台龟速的旧笔记本，折腾之心再起。以前已经重装过N次系统，包括windows，也包括linux，都不太理想。自己毕竟不是程序员，不需要开发程序，也不会变成，用linux的感觉终究还是不习惯，不过运行速度倒是挺快的。最近又接触了Chrome OS系统，折腾了一下，但是安装成功后无法登录谷歌账号，无奈还是放弃了。又听说国内基于Chrome OS系统二次开发的[FydeOS - 面向未来的操作系统 | 为中国用户打造的 Chrome OS](https://fydeos.com/)，尝试了一下，在这里做个记录。

## 安装过程
步骤1. 下载镜像文件：[FydeOS - 下载](https://fydeos.com/download)
![20210826155230](https://gitee.com/alingyisheng/tupian/raw/master/img/20210826155230.png)
这里我选择的是**镜像2**，下载后不用解压，保留待用
![20210826160306](https://gitee.com/alingyisheng/tupian/raw/master/img/20210826160306.png)

步骤2. 下载[Rufus](https://rufus.ie/zh/)： 用来创建USB启动盘
![20210826155915](https://gitee.com/alingyisheng/tupian/raw/master/img/20210826155915.png)
这里我选了**第一个Rufus 3.15（1.1MB）**，下载完成后直接打开。
![20210826160349](https://gitee.com/alingyisheng/tupian/raw/master/img/20210826160349.png)

步骤3. 打开Rufus，制作usb启动盘，电脑插入一个8G优盘，选择**步骤1**下载好的镜像文件。然后安心图中选择分区类型，点击开始，等着制作完成。
![20210826160905](https://gitee.com/alingyisheng/tupian/raw/master/img/20210826160905.png)

步骤4. 把制作好的启动盘插入旧电脑，开机，按住F12（我的电脑是Dell inspiron 14-3421）进入安装界面，然后等待进入安装界面，这里不多做介绍，我这里是在首次启动 FydeOS 的第一个画面里呼出「FydeOS Installer」，然后根据屏幕的提示将 FydeOS 安装到设备的硬盘里的。

详细可看官网的[安装说明 ](https://faq.fydeos.com//#how-to-install-fydeos-to-the-hard-disk)。也可[使用命令行将 FydeOS for PC 安装进硬盘](https://faq.fydeos.com/getting-started/install-fydeos-to-hdd-using-cli/)。


## 使用体验
1. 运行速度：还可以，比window要快，偶尔会有卡顿。这台电脑我主要用来浏览网页，或看一些视频用，所以对浏览器![](../../z%20-%20Attachments%20I%20附件/Screenshot%202021-08-26%2016.48.04.png)的依赖很大，而系统自带的**chrome浏览器**正好适合。


2. 界面还是比较简洁，美观的，易上手。

3. 局域网传送文件，可以用燧石传输
![20210826175011](https://gitee.com/alingyisheng/tupian/raw/master/img/20210826175011.png)
4. 可以安装word等基本的在线办公工具。
![20210826174917](https://gitee.com/alingyisheng/tupian/raw/master/img/20210826174917.png)
5. 可以安装安卓应用，比如说**哔哩哔哩**，运行过程会卡顿，体验不流畅。
![Screenshot 2021-08-26 16.46.43](https://gitee.com/alingyisheng/tupian/raw/master/img/Screenshot%202021-08-26%2016.46.43.png)
6. 可以运行linux，但对我来说用处不大。
![Screenshot 2021-08-26 16.51.17](https://gitee.com/alingyisheng/tupian/raw/master/img/Screenshot%202021-08-26%2016.51.17.png)

## 总体评价
还不错，至少安慰了我的这颗爱折腾的心，让它暂时平静了下来，所以我会给个好评，推荐有破旧笔记本的小伙伴，在无所事事，百无聊赖的时候可以折腾一下。阿狸的Blog，赶紧平静下来吧。
