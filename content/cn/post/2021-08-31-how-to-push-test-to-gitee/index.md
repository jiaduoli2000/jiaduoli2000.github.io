---
title: 如何推送本地内容到码云（Gitee）？
author: 阿狸的Blog
date: '2021-08-31'
slug: how to push test to gitee
categories:
  - 效率工具
tags:
  - gitee
---

无奈于github推送的速度太慢，或者干脆无法推送。似乎推送本地内容到[码云Gitee](https://gitee.com/enterprises?utm_source=google&utm_medium=sem&utm_campaign=enterprise&utm_term=giteezsy&gclid=EAIaIQobChMIwe6k8IXa8gIVRVtgCh1IfgBCEAAYASAAEgKBH_D_BwE)是一个解决办法。为什么要推送到网络上，这里我是本着开源的思想，把一些资料上传到码云，以供大家学习。简单的说，就是把Gitee或Github当作是网络硬盘来用，同时可以对自己的资料做个备份。电脑、网盘都是不靠谱的，随时可能发生意外。下面记录一下相关方法：

## 直接用git-大多数程序员的选择
首先克隆`git clone url.git`，然后查看当前所有分支`git branch -a`，新建本地分支`git branch my_branch` ，然后切换到本地分支`git checkout my_branch`，  将我们的项目代码提交`git add .` ， `git commit -m "new add files"`，最后将本地分支推到远程分支`git push origin my_branch`，这是[简书](https://www.jianshu.com/p/11cbd8de7098)上一位网友的方法介绍。对于一个连git都不懂的人，这种方法好像不太适合我呀。看来还是要找到一种对菜鸟友好的方法。

## TortoiseGit-群众的选择
为什么要选择TortoiseGit，俩字“简单”，四个字“简单方便“。TortoiseGit是一个可视化管理软件，非命令行操作，支持简体中文等多种语言，适合我这种不懂代码的吃瓜群众。下面我们来了解一下如何使用。

### 安装git

当然，要使用 TortoiseGit，要先在电脑上[安装Git](https://www.runoob.com/git/git-install-setup.html)。

![20210831091243](https://gitee.com/alingyisheng/tupian2/raw/master/20210831091243.png)

安装完成后，在桌面上单击鼠标右键，可以看到`Git GUI Here`和`Git Bash Here`, 这应该是Git安装成功了吧。

### 安装TortoiseGit

下面我们来安装TortoiseGit。[软件下载](https://tortoisegit.org/download/)：https://tortoisegit.org/download/。

![20210831092744](https://gitee.com/alingyisheng/tupian2/raw/master/20210831092744.png)

官网的小乌龟还是挺可爱的。根据电脑配置选择下载的版本，这里我选择`for 64-bit windows`。安装过程不复杂，和其他软件一样，一直下一步到底就可以了。

![20210831093227](https://gitee.com/alingyisheng/tupian2/raw/master/20210831093227.png)

一直到这里，停顿一下。

![20210831093423](https://gitee.com/alingyisheng/tupian2/raw/master/20210831093423.png)

点击上图中的`download`, 在弹出的界面中选择`chines，simplified`，然后点击`Setup`安装。

![20210831093655](https://gitee.com/alingyisheng/tupian2/raw/master/20210831093655.png)

语言包安装完成后，选择下图中的`language`为中文简体，然后进入下一页。这里也可以存储这些设置。

![20210831094007](https://gitee.com/alingyisheng/tupian2/raw/master/20210831094007.png)

一直到这里，填入自己Gitee的用户名和邮箱，进入 下一页。

![20210831094324](https://gitee.com/alingyisheng/tupian2/raw/master/20210831094324.png)

到这里点击`生成PuTTY密钥对`,

![20210831094644](https://gitee.com/alingyisheng/tupian2/raw/master/20210831094644.png)

在弹出的对话框中，选择`Generate`,

![20210831094831](https://gitee.com/alingyisheng/tupian2/raw/master/20210831094831.png)

然后点击下图中的`Save private key`, 点击是，然后把**Putty密钥**保存到本地，到此安装完成。

![20210831095156](https://gitee.com/alingyisheng/tupian2/raw/master/20210831095156.png)

安装完成后，在桌面单击鼠标右键，可以看到下图。是不是有些变化？

![20210831095919](https://gitee.com/alingyisheng/tupian2/raw/master/20210831095919.png)

## 如何用TortoiseGit？

### 建立新仓库

假设我们已经注册了[码云](https://gitee.com/)，注册后根据需求新建一个仓库，界面如下：

![20210831101352](https://gitee.com/alingyisheng/tupian2/raw/master/20210831101352.png)

仓库建好之后，复制**仓库链接地址**备用。

![20210831102110](https://gitee.com/alingyisheng/tupian2/raw/master/20210831102110.png)

### 克隆仓库到本地
在桌面单击鼠标右键，选择”git克隆“。

![20210831095919](https://gitee.com/alingyisheng/tupian2/raw/master/20210831095919.png)

填入**仓库链接地址**，**存储位置**，以及**Putty密钥**。

![20210831102347](https://gitee.com/alingyisheng/tupian2/raw/master/20210831102347.png)

在弹出的对话框中，填入码云的用户名和密码。

![20210831102720](https://gitee.com/alingyisheng/tupian2/raw/master/20210831102720.png)

等待传输完成。这里我克隆到本地的文件夹名为`test`。

![20210831102908](https://gitee.com/alingyisheng/tupian2/raw/master/20210831102908.png)

### 文件推送到码云

在`test`文件夹中存入一个名为”新建文本文档“的文件。

![20210831103135](https://gitee.com/alingyisheng/tupian2/raw/master/20210831103135.png)

上传文件，分为两个操作，`提交`和`推送`。`提交`是将文件添加到本地版本控制里面，并没有提交到远程项目里。`推送`是提交到远程项目里。

![20210831103805](https://gitee.com/alingyisheng/tupian2/raw/master/20210831103805.png)

选中文件夹`test`, 右键选择`Git同步`或`Git提交`。

#### 点击Git同步

点击`推送`提交到远程项目里。点击`拉取`，我们就能从远程项目上拉取到新的文件。

![20210831104631](https://gitee.com/alingyisheng/tupian2/raw/master/20210831104631.png)

#### 点击Git提交

填写`日志信息`、`选中文件`，然后`提交`。

![20210831104306](https://gitee.com/alingyisheng/tupian2/raw/master/20210831104306.png)

#### 更多

我们也可以右键选中`TortoiseGit(T)`, 这里有更多的功能设置，有兴趣的小伙伴可以自己去发掘一下。

![20210831105139](https://gitee.com/alingyisheng/tupian2/raw/master/20210831105139.png)

## 小结

总体来说，设置不算复杂，很快就能完成，用起来确实是”简单方便“，大力推荐不懂代码的小伙伴尝试一下，而且Gitee的速度比起Github来说，那快的可不是一点半点。我本来想用码云的`Gitee Pages`来托管我的博客[阿狸的Blog (aliyisheng.cc)](https://www.aliyisheng.cc/)的，无奈技术不够，折腾了2天没有成功，美好的理想到此作罢。在这个过程中了解了TortoiseGit的用法，也算是一种收获吧，在此做个记录。这里是**阿狸的Blog**，再见。
