---
title: 在Zettlr(Markdown 编辑器)中插入参考文献
author: 阿狸的Blog
date: '2021-07-15'
slug: zettlr-markdown
categories:
  - 效率工具
tags:
  - zettlr
---
[Zettlr](https://www.zettlr.com/)，一种Markdown 编辑器，开源，是为非编码技术人员设计的，用作者的话说，是专门为社会科学、历史或政治学的学生打造的，因为作者本人是德国社会学家/政治理论家。在这里，对于跨专业人才，我是无比崇拜呀，因此今天我这个医学生，也来了解一下Zettler。

![20210715101237](https://gitee.com/alingyisheng/tupian2/raw/master/20210715101237.png)

## 1. 安装Zettlr
### 1.1 下载及安装
安装过程很简单，打开[Zettlr下载地址](https://www.zettlr.com/download/win32)，选择适合自己的操作系统版本，下载后直接安装就行了，和安装其他软件一样，直接点击下一步到安装完成。

### 1.2 设置中文界面
想让Zettlr 拥有中文界面，可以点击设置(齿轮图标)，打开“Preferences”，点击“Chinese(china)”，点击“Save”，重新启动Zettlr就可以了。

![20210715105019](https://gitee.com/alingyisheng/tupian2/raw/master/20210715105019.png)

重启后变成了这个样子：

![20210715104759](https://gitee.com/alingyisheng/tupian2/raw/master/20210715104759.png)

## 2. 相关软件安装

### 2.1 安装Pandoc
Pandoc是一个小程序，能够将文档文件从一种格式转换成另一种格式。它非常强大，有很多选择。为了使Zettlr能够导入和导出文件，需要在您的计算机上安装Pandoc。因为我的电脑是Windows系统，安装的话先[从官网下载安装程序](https://github.com/jgm/pandoc/releases/tag/2.14.0.3)，然后运行它。

![20210715123754](https://gitee.com/alingyisheng/tupian2/raw/master/20210715123754.png)

这里我下载的是“[pandoc-2.14.0.3-windows-x86_64.msi](https://github.com/jgm/pandoc/releases/download/2.14.0.3/pandoc-2.14.0.3-windows-x86_64.msi)”。

### 2.2 安装LaTeX
如果我们要导出PDF文件，Pandoc本身依赖于另一个免费的开源软件包:LaTeX。Pandoc可以将Markdown文件转换成LaTeX文件，但是为了创建PDF文件，我们需要安装LaTeX。这里我安装的是流行[MiKTeX](https://miktex.org/download)，点击下载后就可以安装了。安装好之后，我试着运行了一下导出PDF文件，可以导出，但是，有个问题，字体都显示的是方块：

![20210715131711](https://gitee.com/alingyisheng/tupian2/raw/master/20210715131711.png)

### 2.3 Zotero中安装BetterBibTex插件
如果你应用的文献管理工具是[Zotero](https://www.zotero.org/download/)，为了在写作的时候插入参考文献，需要安装一个插件：[Better BibTeX for Zotero 下载地址)](https://retorque.re/zotero-better-bibtex/)。

![20210715145505](https://gitee.com/alingyisheng/tupian2/raw/master/20210715145505.png)

安装好BetterBibTex后，需要导出文献库文件。在zotero菜单栏中选择“文件”
，点击“导出文件库”。

![20210715150228](https://gitee.com/alingyisheng/tupian2/raw/master/20210715150228.png)

在弹出的对话框中，格式选择“Better CSL JSON”, 在“Keep updated”前面的方框中划勾。然后点击“ok”，然后写一个名字，并保存就可以了。这里要记住文件存储路径。

![20210715150404](https://gitee.com/alingyisheng/tupian2/raw/master/20210715150404.png)

然后将刚才的库文件导入到Zettlr。我们打开zettlr的“设置”选项，转到“导出”选项卡，然后单击引文数据库输入字段右侧的小文件夹图标。将出现一个对话框，让您导航到您的数据库文件。选择它，保存首选项，Zettlr将自动加载数据库。现在你准备引用了！

![20210715152702](https://gitee.com/alingyisheng/tupian2/raw/master/20210715152702.png)

## 3. 开始写作
### 新建文档
下面我们打开zettlr软件，新建一个文档，然后给文档起个名字，比如我起的名字是“zettlr使用初探.md”，可以看出，这是一个Markdown文件。

### 开始引用参考文献
在Zettlr中引用非常容易。我可以简单地在文本中的某个地方写入一个标识符“@”，这样就会弹出文献库中的所有文献，像这样：

![20210715153454](https://gitee.com/alingyisheng/tupian2/raw/master/20210715153454.png)

你可以选择想要插入的文献，然后点击，文献就被插入了。我们可以在右侧的边栏中看到这篇餐卡文献的的详细信息，以及引用格式。当然，我也可以更改引用样式。[[如何更改引用样式]]，以后有时间的话我们再说。

![20210715154027](https://gitee.com/alingyisheng/tupian2/raw/master/20210715154027.png)


 更多内容，可以选择阅读[Zettlr使用教程](https://docs.zettlr.com/en/)。






## 参考文献
[Zettlr：适合写作者和研究人员的 Markdown 编辑器 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/67733927)
