---
title: Zotero和Scrivener管理参考文献
author: 阿狸的Blog
date: '2021-09-04'
slug: Zotero and Scrivener manage references
categories:
  - r
tags:
  - scrivener
---

这是一次糟糕的折腾过程，踩了很多坑，丢了很多文件，很沮丧。也明白了一些道理，有些坑，也许只有你自己会遇到。你遇到了，是因为你很久之前做的选择。那就记录一下这个过程。有人说，成功很美，说的很对。那如果失败了呢，还美吗，不美了，但可能会收获更多。

在使用Zotero的过程中，为了追求功能的极致或者说就是为了新鲜，我试用了zotero beta， beta版本自带一个内置的`pdf阅读器`，界面设计很优美的，笔记功能也是很不错的，但是和其他插件配合起来还存在缺陷。试用之后，一直在用zotero beta这个版本，当然没有用继续用它的`pdf阅读器`功能。

另外，为了实现远程同步，我尝试过一些方法。zotero官方建议使用`登陆账号`来进行同步，不过容量有限，只有300MB，超过的话，需要购买，下面这个价格表对于普通用户来说是接受不了的，当然也有人介绍同步到`坚果云`的方法，我也试用过，坚果云也对免费用户上传和下载的流量进行了限制。所以最终，我选择了一种官方不建议的方法，我用`群晖NAS`来同步我的台式机和笔记本中zotero内容，一直以来，虽然间断会报错，但还算能用。采用这种方法，不用登陆zotero账号，也就是不开启云服务。

![20210904105320](https://gitee.com/alingyisheng/tupian/raw/master/img/20210904105320.png)

就是在`zotero beta+NAS同步`的前提下，我今天掉进了一个大坑。掉坑的结果“`丢了`”很多文件，不，是全部文件。为什么要加引号，因为这些文献其实并没有丢失，还在`storage`这个文件夹里。只不过zotero和storage之间的联系不见了。

![20210904110602](https://gitee.com/alingyisheng/tupian/raw/master/img/20210904110602.png)

好吧，我的zotero又回到了它刚出生时的样子，没有插件，没有文献，没有分类文件夹，没有标签，哈哈，这才是真实的世界，走一段路，就回归一次原点。会悔恨么，会为自己瞎折腾自责么，没有必要，“大不了从头再来”。耳边又听见朋友那句“电脑就是用来玩的，光看个片叫玩电脑么？”。软件也一样。别的呢？

![20210904111424](https://gitee.com/alingyisheng/tupian/raw/master/img/20210904111424.png)

那就从新开始吧，我还没有告诉大家我这次折腾的目的：在上一期[如何使用Zotero和Scrivener进行配合写作?](https://www.bilibili.com/video/BV1xv411P7vM?spm_id_from=333.999.0.0)，我曾说过，在完成初稿之前，最好不要太留意排版的事情。但一旦初稿完成，排版又成了必然问题。我们使用文件管理软件，无论是`zotero`还是`endnote`，抑或是我认为的独立王国的王者`citavi`，都是为了一个功能，`插入`和`编辑`参考文献。所以，这次的主题是：如何使用Zotero和Scrivener高效管理参考文献?。

## 安装

>1. [Zotero 下载：https://www.zotero.org/download/](https://www.zotero.org/download/)，老老实实安回稳定版本。

![20210904113525](https://gitee.com/alingyisheng/tupian/raw/master/img/20210904113525.png)

>2. [LibreOffice  下载：https://www.libreoffice.org/download/download/](https://www.libreoffice.org/download/download/)，一个类似于微软office的软件，但是是开源免费的，可用于Windows、Mac和Linux。

![20210902203015](https://gitee.com/alingyisheng/tupian/raw/master/img/20210902203015.png)

>3. 在Zotero中安装`LibreOffice插件`。当您安装Zotero并重新启动（或启动）LibreOffice时，会弹出一个安装插件的对话框，直接安装就可以了。安装完成之后可以查看一下。

![20210902212920](https://gitee.com/alingyisheng/tupian/raw/master/img/20210902212920.png)

![20210902213155](https://gitee.com/alingyisheng/tupian/raw/master/img/20210902213155.png)

>4. 安装[Java runtime:](https://www.oracle.com/java/technologies/javase-jre8-downloads.html)。这里我就不安装了，我在这期视频中[效率工具-Citespace-我是如何安装这款引文可视化工具的？](https://www.bilibili.com/video/BV1AB4y1M7bT/)已经安装过了。

>5. 在Zotero中安装`RTF/ODF-Scan插件`。[RTF/ODF-Scan for Zotero：https://zotero-odf-scan.github.io/zotero-odf-scan/](https://zotero-odf-scan.github.io/zotero-odf-scan/)。

![20210902214203](https://gitee.com/alingyisheng/tupian/raw/master/img/20210902214203.png)

安装成功后在`zotero-工具-插件`，查看一下插件。

![20210902214436](https://gitee.com/alingyisheng/tupian/raw/master/img/20210902214436.png)

查看：zotero-工具，看到`ODF Scan`，证明安装成功。

![20210902214802](https://gitee.com/alingyisheng/tupian/raw/master/img/20210902214802.png)

>6. 安装Scannable Cite.js，如果没有自动安装，就进行手动安装。先进入[这个网址：Scannable cite... - Zotero Forums](https://forums.zotero.org/discussion/80689/scannable-cite)，按下图示找到标红线的链接，千万不要找错了，右键单击此链接，然后选择“**将链接另存为**”，不要单击该链接将其打开。将Scanable Cite.js文件保存在Zotero Translators文件夹中，该文件夹位于Users/Your Username/Zotero/Translators下。重新启动Zotero，然后再次检查快速复制下拉菜单。选择Scanable Cite(现在应该在那里)，您就可以开始下一步了。

![20210903145750](https://gitee.com/alingyisheng/tupian/raw/master/img/20210903145750.png)

![20210903145932](https://gitee.com/alingyisheng/tupian/raw/master/img/20210903145932.png)

到此，安装结束，最关键的第6步，不要找错。

## 使用
### 初稿完成

在zotero中增加 2 篇文献。
![20210904121135](https://gitee.com/alingyisheng/tupian/raw/master/img/20210904121135.png)

新建scrivener文稿。从上到下依此点击下图“`红线`”标记处，点击完成后可见`“脚注”`。

![20210904121536](https://gitee.com/alingyisheng/tupian/raw/master/img/20210904121536.png)

选中一段文字，把zotero中的文献直接拖动到scrivener文稿的`脚注`中，

![20210904121929](https://gitee.com/alingyisheng/tupian/raw/master/img/20210904121929.png)

看看有什么变化：

![20210904122224](https://gitee.com/alingyisheng/tupian/raw/master/img/20210904122224.png)

在`scrivener-文件-编译`，选择`open office (.odt)`, 点击`compile`，保存。我这里存在桌面，命名为`test`。

![20210904122453](https://gitee.com/alingyisheng/tupian/raw/master/img/20210904122453.png)

### 格式转换

来到`zotero-工具-ODF Scan`，

![20210904123221](https://gitee.com/alingyisheng/tupian/raw/master/img/20210904123221.png)

依此从上到下按图示选择，然后`next-finish`，我这里存在桌面，命名为`test（citations）`。

![20210904123603](https://gitee.com/alingyisheng/tupian/raw/master/img/20210904123603.png)

用**LibreOffice**打开文件`test（citations）`，可以看`脚注`，以及`编号`，

![20210904124108](https://gitee.com/alingyisheng/tupian/raw/master/img/20210904124108.png)

点击带个z的小齿轮，可以设置参考文献的样式：

![20210904124428](https://gitee.com/alingyisheng/tupian/raw/master/img/20210904124428.png)

点击带个z的小书标，生成参考文献：

![20210904124922](https://gitee.com/alingyisheng/tupian/raw/master/img/20210904124922.png)

这样，参看文献就插入完成了，如果你在zotero中对参考文献的内容进行了更改，那么这个文档里的参考文献内容也会随之更改，这就形成了一种联动。

好吧，就到这里吧，有点累了。休息一会儿，还得去打捞我以前的文献。希望今天的内容对你的写作有所帮助，我是阿狸，再见。
