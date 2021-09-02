---
title: R语言-bibliometrix包-文献可视化工具
author: 阿狸的Blog
date: '2021-07-25'
slug: r-bibliometrix
categories:
  - 效率工具
tags:
  - citspace
---
## bibliometrix包安装与调用
bibliometrix，是一款R包，Bibliometix这款R包，是基于【**文献计量学**】开发的。通过文献计量学分析相关文献，能够帮助我们快速了解相关方向的经典文献，领域内的领军人物以及分析未来的发展趋势。它能帮助我们整理本领域内的相关文献，并对结果进行可视化。

下面是如何安装并调用：
```
rm(list= ls())
#install.packages("bibliometrix")
library(bibliometrix)
biblioshiny()
```
调用后再浏览器中会弹出一个页面，证明调用成功，页面如下：

![](https://gitee.com/alingyisheng/tupian2/raw/master/Pasted%20image%2020210629104700.png)

## 准备工作：文献下载
在这里我们以“胸腺瘤”，英文“thymoma”为例。检索的scopus数据库，搜索关键词“thymoma”（下图中黄色标记）。检索结果可见16275篇文献。

![Pasted image 20210628154933](https://gitee.com/alingyisheng/tupian2/raw/master/Pasted%20image%2020210628154933.png)

我们选择前2000篇文献导出，方法如下：

![Pasted image 20210628155209](https://gitee.com/alingyisheng/tupian2/raw/master/Pasted%20image%2020210628155209.png)

![Pasted image 20210628155321](https://gitee.com/alingyisheng/tupian2/raw/master/Pasted%20image%2020210628155321.png)
点击导出，保存到桌面就可，注意：这个文件的格式是"**.bib**"。

## 文献导入
在下图菜单栏中中，选择“data”下面的“import or load files”，

![Pasted image 20210628160623](https://gitee.com/alingyisheng/tupian2/raw/master/Pasted%20image%2020210628160623.png)

按下面1-4的顺序，选择并导入上一步下载好的".bib”格式的文件，点击“start”，右边会出现引文，作者等各种信息。

![Pasted image 20210628160910](https://gitee.com/alingyisheng/tupian2/raw/master/Pasted%20image%2020210628160910.png)

可以用菜单栏的"filter"筛选你需要的文章，比如按类型，论著，综述，以及发表年份，被引数等。

![Pasted image 20210628161150](https://gitee.com/alingyisheng/tupian2/raw/master/Pasted%20image%2020210628161150.png)

## 文献可视化分析
### 每年发表胸腺瘤相关文章的趋势
![Pasted image 20210628161537](https://gitee.com/alingyisheng/tupian2/raw/master/Pasted%20image%2020210628161537.png)

可以看出，胸腺瘤研究在2017-2020是逐渐增多的，2021年下降。

### 哪些杂志发表胸腺瘤文章最多？
![Pasted image 20210628161911](https://gitee.com/alingyisheng/tupian2/raw/master/Pasted%20image%2020210628161911.png)

可以看出，journal of thoracic disease 这个期刊发表的最多，这是个什么样的杂志，请自己百度一下。

### 胸腺瘤研究领域有哪些大牛？
![Pasted image 20210628162949](https://gitee.com/alingyisheng/tupian2/raw/master/Pasted%20image%2020210628162949.png)

看来以国人发表的研究最多。

### 还能获得什么信息？
![Pasted image 20210628163706](https://gitee.com/alingyisheng/tupian2/raw/master/Pasted%20image%2020210628163706.png)


**词云图**，展示最常出现的词汇。
**网络图**，展示各文章之间的相互引用。
**世界地图**，展示各个文章之间的合作国家关系。

另外还有许多其他的分析以及各种漂亮的可视化图形，如果你觉得在线的绘制不满意，还可以把数据导出，自己用ggplot2或其他R包进行可视化。由于可分析的内容非常多，在这里就不跟大家一一展示了。
