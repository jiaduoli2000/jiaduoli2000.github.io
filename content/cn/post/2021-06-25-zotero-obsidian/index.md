---
title: zotero 与 obsidian 配合提高阅读效率
author: 阿狸的Blog
date: '2021-06-25'
slug: zotero-obsidian
categories:
  - 效率工具
tags:
  - obsidian
---
[Zotero](https://www.zotero.org/)是一款不错的文献管理工具，开源，免费，功能强大。作为医学生，我们可以用它来管理文献。

[Obsidian](https://obsidian.md/)是一款强大的笔记软件，开源，支持双向链接，有利于我们进行知识循环。

如何把二者联合起来，以提高我们的阅读效率，今天我们来探讨一下这个话题。

## 我是如何做的？
假如我从[PubMed ](https://pubmed.ncbi.nlm.nih.gov/)或[中国知网](https://www.cnki.net/)下载了一些关于关键词“胸腺瘤”的文献，并存在了我的电脑桌面上，准备进行阅读。没错，就是下面这篇。

![20210712215325](https://gitee.com/alingyisheng/tupian/raw/master/img/20210712215325.png)

现在这篇文献的PDF格式文件我已经下载好了，我首先要做的是把这个文件导入到zotero中。我可以直接把这个文件拖动到zotero中，然后就是这个样子：

![20210712215930](https://gitee.com/alingyisheng/tupian/raw/master/img/20210712215930.png)

在这里，如果是英文文献，我可选中这篇文献后，点击鼠标右键，点击重新抓取pdf的元数据，然后这篇文章的元数据就有了。
![20210712220221](https://gitee.com/alingyisheng/tupian/raw/master/img/20210712220221.png)


### "坑一"-中国知网文献无法获取元数据怎么办？
从知网下载的中文文献的元数据获取不了。解决办法是安装“[jasminum: 茉莉花](https://github.com/l0o0/jasminum)插件。

>具体安装方法可参考：
[简单的Zotero CNKI 中文插件 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/159408394)

安装好茉莉花插件之后，我们选中这篇文献，点击鼠标右键，点击抓取知网元数据。

![20210712221542](https://gitee.com/alingyisheng/tupian/raw/master/img/20210712221542.png)

然后这篇文章的索引信息就有了。
![20210712222838](https://gitee.com/alingyisheng/tupian/raw/master/img/20210712222838.png)


### 开始文献阅读
在zotero中双击我刚才要阅读的那篇文献的pdf，它就会在默认的PDF阅读器中打开，这里我用的是"Adobe Acrobat Pro DC"，我会一边阅读，一边做一些标注。比如这样：

![20210712223302](https://gitee.com/alingyisheng/tupian/raw/master/img/20210712223302.png)

阅读完这篇文献之后，我会把pdf阅读器关掉，关掉之前会有弹出提示：要不要保存？这里一点不要忘了保存。

### 提取文献内容到Obsidian
#### 准备工作1：zotero安装插件
1. [ZotFile](http://zotfile.com/)插件
2. [Mdnotes for Zotero](https://github.com/argenos/zotero-mdnotes)插件
3. [Better BibTex for ZoteroI](https://retorque.re/zotero-better-bibtex/installation/)插件

安装方法比较简单，先下载，然后常规安装，这里就不赘述了。安装完成后是这个样子：

![20210712225020](https://gitee.com/alingyisheng/tupian/raw/master/img/20210712225020.png)

#### 准备工作2：Obsidian安装插件
1. [obsidian-citation-plugin](https://github.com/hans/obsidian-citation-plugin/releases/tag/0.4.3)插件

安装方法比较简单，先下载，然后常规安装，这里就不赘述了。安装完成后是这个样子：

![20210712225611](https://gitee.com/alingyisheng/tupian/raw/master/img/20210712225611.png)

>安装完成后需要进行一些设置，具体设置方法参考：
[zotero插件_ob和zotero连用（Citation插件介绍）](https://blog.csdn.net/weixin_39758618/article/details/113326410)


#### zotero中pdf注释提取
我们回到zotero，选中我刚才阅读完的那篇文献，点击右键，在弹出的选项中找到“Manage Attachments”，然后进一步选择“Extract Annotations”。

![20210713083931](https://gitee.com/alingyisheng/tupian2/raw/master/20210713083931.png)

然后就会提取出pdf注释，并生成一个新文件如下：

![20210713084904](https://gitee.com/alingyisheng/tupian2/raw/master/20210713084904.png)

我们可以点击这个文件看一下，可以看到最右侧就显示了我们之前在pdf阅读器中注释的内容。

#### 从zotero提取文献信息到obsidian
下面开始提取我们刚才阅读的那篇文献的信息到obsidian，我们选中文献，点击右键，在弹出的选项中找到“Mdnotes”，然后进一步选择“Create Mdnotes file”。（这里有三个选择，另外两个“Export to markdown”，“Batch export to markdown”，你可以自己尝试一下，看看会有什么效果。）

![20210713085456](https://gitee.com/alingyisheng/tupian2/raw/master/20210713085456.png)

我们把“Create Mdnotes file”建立的文件存储在一个文件夹中，这里我已经在obsidian文件夹的根目录建立一个文件夹，并命名文件夹名为“6 - References”。我就把新建立的markdown文件存在这里。

![20210713090544](https://gitee.com/alingyisheng/tupian2/raw/master/20210713090544.png)

点击"打开"，然后点击“保存”，然后我们在obsidian中来看一下新保存的这个文件。

![20210713091133](https://gitee.com/alingyisheng/tupian2/raw/master/20210713091133.png)

这个样子好像并不符合我可胃口，需要调整一下这个内容模板。

#### 调整保存到obsidian中的内容模板
我们希望从zotero提取到obsidian中的内容符合我们的阅读习惯，我们就要制作自己的模板。首先，在菜单栏选择"工具“, 然后选择”Mdnotes preferences“。

![20210713091854](https://gitee.com/alingyisheng/tupian2/raw/master/20210713091854.png)

点击之后，会弹出一个对话框，如下：

![20210713092141](https://gitee.com/alingyisheng/tupian2/raw/master/20210713092141.png)

我们在”Template folder“中选择”模板所在的文件夹“，我这里还是选择文件夹 ”6 - References“。因为，在这之前我已经把我做好的模板放在了这个文件夹中。

![20210713092657](https://gitee.com/alingyisheng/tupian2/raw/master/20210713092657.png)

这个模板也是一个markdown文件，我的这个模板的名称是”Mdnotes Default Template“样式是这样的：

![20210713092850](https://gitee.com/alingyisheng/tupian2/raw/master/20210713092850.png)

#### 再次从zotero提取文献信息到obsidian
设置好模板之后，我们把原先那个从zotero导入到obsidian的文件删掉，然后重新导入一次，看看会有什么变化。操作方法同前。

![20210713085456](https://gitee.com/alingyisheng/tupian2/raw/master/20210713085456.png)

然后我们看看应用了”模板“后，会是什么样子：

![20210713094123](https://gitee.com/alingyisheng/tupian2/raw/master/20210713094123.png)

是不是与没有应用模板的时候发生了很大的变化，我们看看这里都包含了哪些信息：

1. 标题：
![20210713094455](https://gitee.com/alingyisheng/tupian2/raw/master/20210713094455.png)

2. 作者：
![20210713094554](https://gitee.com/alingyisheng/tupian2/raw/master/20210713094554.png)

3. 发表时间：
![20210713094706](https://gitee.com/alingyisheng/tupian2/raw/master/20210713094706.png)

4. 标签：
![20210713094826](https://gitee.com/alingyisheng/tupian2/raw/master/20210713094826.png)

5. 文献的网页链接：
![20210713095015](https://gitee.com/alingyisheng/tupian2/raw/master/20210713095015.png)

6. 连接到zotero所在位置
![20210713095308](https://gitee.com/alingyisheng/tupian2/raw/master/20210713095308.png)

7. 本地PDF附件
![20210713095422](https://gitee.com/alingyisheng/tupian2/raw/master/20210713095422.png)

8. pdf中的注释内容
![20210713095541](https://gitee.com/alingyisheng/tupian2/raw/master/20210713095541.png)

好吧，就是这些内容，如果你还需要文献的其他信息，你可以自己编辑自己的模板。

## 小结
本文读起来可能有些复杂，主要是设置过程，安装许多插件，但一旦设置完成，用起来就会很方便。特别是obsidian强大的标签和链接功能，我们很容易找到我们之前阅读过的文献内容，而不至于读完某篇文献后，想用的时候就再也找不到了，然后就，没有然后了。所以，不要害怕这个设置过程，一步一步做下来，你会感觉也不是很复杂的。

如果按照这个教程没有设置成功的化，记得告诉我。我已经尽力写的明白，但能力有限，有些时候自己可能表达的不太清楚，如果不清楚的化可以给我留言，共同探讨解决。我的个人公众号及B站up都名为：阿狸的Blog，欢迎点赞关注。然后我会做一个同名的视频教程，可能会讲得清楚一些。好吧，我是阿狸，再见。
