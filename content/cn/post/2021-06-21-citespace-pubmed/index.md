---
title: 下载新版PubMed为xml格式文件并导入CiteSpace
author: 阿狸的Blog
date: '2021-06-21'
slug: citespace-pubmed
categories:
  - 效率工具
tags:
  - citspace
---


上一期我们学习了CiteSpace，也叫引文空间，是一个强大的文献可视化工具。作为一个医学生，我们经常要在[PubMed](https://baike.baidu.com/item/PubMed/3912197?fr=aladdin)来检索生物医学文献，本期主要讲解把Pubmed中检索的文献导入到Citespace进行可视化分析。关于citespace安装的问题，请参考我的上一期视频[[../../4-Note/Ⅰ-R统计与绘图/效率工具-初学CiteSpace]]。

## 1.xml格式文件下载

[[如何以XML文本文件格式从新的Pubmed中保存参考文献？]] ，这里我们需要用到PubMed2XL。PubMed2XL是一个免费的网络工具，它允许你以xml格式下载多个引文，可以在[https://pubmed2xl.com/xml/](https://pubmed2xl.com/xml/).上找到。只需在搜索框中输入PMID号，每行一个，然后单击**下载**按钮。
![[Pasted image 20210612181419.png]]

我们来演示一下。首先，我们把网址收藏在收藏夹中，打开[PubMed (nih.gov)](https://pubmed.ncbi.nlm.nih.gov/)。
![[Pasted image 20210612181609.png]]

我们来搜索“lung cancer”，肺癌，然后点击搜索，在搜索的结果中，点击我们想要可视化的文献，我们这里来选择10篇，选中后点击我们收藏家里的PubMed2XL，
![[Pasted image 20210612182243.png]]

点击download xml file，命名为“download_pubmed”保存下载的文件到桌面。

下载这一步就完成了。

## 2.导入CiteSpace

在导入Citespace软件之前，我们需要做一些准备工作。我们需要在桌面建一个文件夹，命名为pubmed，然后打开这个pubmed文件夹，在里面建立四个文件夹，分别命名为：input、output、data、project，建好之后，我们把刚才下载的“download_pubmed”复制到“input”文件夹。然后，打开Citespace软件，

![[Pasted image 20210612082758 1.png]]

点击菜单栏的data，选择import/export，选择pubmed，选择相应的input和output文件夹，然后选择pubmed（xml）→wos，需要运行一会，成功之后，
![[Pasted image 20210612193834.png]]
我们可以看到，在output文件夹里有了一个新文件，
![[Pasted image 20210612184540.png]]
我们把这个文件复制到data文件夹里

我们回到citespace的主界面，在new项目中，输入一个新项目的名字，选择project文件夹的位置，
![[Pasted image 20210612194100.png]]

然后设定一些参数，点击“go”，在弹出的对话框里选择“visualize”即可。
![[Pasted image 20210612194447.png]]

这样，我们导入的pub文献数据就形成了可视化，当然。我们选择的文献的数量较少，所以这个图比较简单，然后关于citespace的参数设置，我还不太了解，以后有机会的化我们再去了解吧。


## 3.参考文献
- [给CiteSpace初学者的学习指南 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/32695561)
- [如何用Citespace处理知网（CNKI）的数据？ - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/56096522)
- [科学网—ChaomeiChen的博客 - 陈超美 (sciencenet.cn)](http://blog.sciencenet.cn/home.php?mod=space&uid=496649)
- [CiteSpace 5.6.R3: Getting Started - YouTube](https://www.youtube.com/watch?v=zPZDu0rm9UM)
- [以中国知网为例的citespace实操（一）\_哔哩哔哩\_bilibili](https://www.bilibili.com/video/BV127411m7ub?from=search&seid=16002619813776693515)
- ![[引文空间分析原理与应用-CiteSpace实用指南 by 陈悦；陈超美；胡志刚；王贤文.pdf]]
