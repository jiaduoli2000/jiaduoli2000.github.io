---
title: TCIA数据库获取影像DICM文件
author: 阿狸的Blog
date: '2021-08-07'
slug: tcia-dicm
categories:
  - 效率工具
tags:
  - tcia
  - mimics
---

大家好，我是阿狸，这里是阿狸笔记，今天的内容是我自学Mimics软件的第二集。上一节，我学会了[如何安装Mimics](https://www.bilibili.com/video/BV1cy4y177im/)。软件安装好了之后，要进一步的学习，就需要影像数据。但是，由于涉及到隐私，影像数据是很难获得了。那怎么办呢，那就要利用一些公开的影像数据库，比如说`TCIA`。所以，我们今天学习的内容就是——如何从TCIA数据库获取影像DICM文件？下面我们就开始吧。
## 简介
**The Cancer Imaging Archive (TCIA)**是癌症研究的医学图像的开放获取数据库。该网站由国家癌症研究所（NCI）癌症影像计划资助，合同由阿肯色大学医学科学院管理。存档内的数据被组织成通常共享癌症类型和/或解剖部位的“集合”。 通常是由常见疾病（例如肺癌），图像形态（MRI，CT等）或研究焦点相关的患者。 DICOM是TCIA用于图像存储的主要文件格式。如果可用，还提供与图像相关的支持数据，如患者结果，治疗细节，基因组学，病理学和专家分析。大多数数据包括以DICOM格式存储的CT，MRI和核医学（例如PET）图像，但也提供或链接许多其他类型的支持数据，以增强研究效用。  

![](app://local/E%3A%5CSynologyDrive%5Cobsidian%5Cz%20-%20Attachments%20I%20%E9%99%84%E4%BB%B6%5CPasted%20image%2020210804223903.png?1628087943000)

  
**TCIA资源旨在支持：**

-   计算机辅助诊断方法的开发（定量成像）
-   通过可接受的标准统计方法评估无偏见的科学重现性
-   临床诊断医学图像与数字显微组织学图像的相关性研究
-   成像的关键因素的探索性生物标志物研究
-   跨学科研究者之间的协作，其中成像对于研究：肿瘤异质性 - 患者和肿瘤内部至关重要;组织时间反应跟踪 - 肿瘤进展的客观测量;成像基因组学和大数据联系和分析（临床，组织病理学，基因组学）。

![](app://local/E%3A%5CSynologyDrive%5Cobsidian%5Cz%20-%20Attachments%20I%20%E9%99%84%E4%BB%B6%5CPasted%20image%2020210804223921.png?1628087961000)

## 操作步骤
1. 打开官网[The Cancer Imaging Archive (TCIA)](https://www.cancerimagingarchive.net/)：

![20210807192531](https://gitee.com/alingyisheng/tupian/raw/master/img/20210807192531.png)

2. 点击上图中`Access the Data`，然后点击`Search Radiology`,

![20210807192712](https://gitee.com/alingyisheng/tupian/raw/master/img/20210807192712.png)

3. 然后点击`Search Radiology`, 显示初始化，等待一会儿

![20210807192837](https://gitee.com/alingyisheng/tupian/raw/master/img/20210807192837.png)

4. 初始化完毕后，进入条件搜索界面，

![20210807192959](https://gitee.com/alingyisheng/tupian/raw/master/img/20210807192959.png)

5. 这里以选择胸部CT为例，勾选`CHEST`,`CT`前面的方框，右侧视窗会显示出搜到的数据，

![20210807193412](https://gitee.com/alingyisheng/tupian/raw/master/img/20210807193412.png)

6. 点击一条数据前面的`购物车`图标, 图标变成绿色之后，然后点击最上方菜单栏的`Download`，

![20210807194243](https://gitee.com/alingyisheng/tupian/raw/master/img/20210807194243.png)

7. 在弹出的对话框中选择`Get NBIA Data Retriever`,

![20210807194411](https://gitee.com/alingyisheng/tupian/raw/master/img/20210807194411.png)

8. 在弹出的界面中，选择左侧视窗中的`NBIA Data Retriever 4.1 Installation Files`,

![20210807194636](https://gitee.com/alingyisheng/tupian/raw/master/img/20210807194636.png)

9. 然后选择自己电脑的系统，我这里选择`Windows`，

![20210807194828](https://gitee.com/alingyisheng/tupian/raw/master/img/20210807194828.png)

10. 在弹出的对话框中，下载安装包并安装。

![20210807194946](https://gitee.com/alingyisheng/tupian/raw/master/img/20210807194946.png)

11. 安装过程同其他windows软件，直接下一步就安装好了。

![20210807195208](https://gitee.com/alingyisheng/tupian/raw/master/img/20210807195208.png)

12. 安装好了之后，桌面会有一个这样的图标：

![20210807195358](https://gitee.com/alingyisheng/tupian/raw/master/img/20210807195358.png)

13. 然后我们回到搜索界面，点击`Download`,

![20210807195505](https://gitee.com/alingyisheng/tupian/raw/master/img/20210807195505.png)

14. 在弹出的对话框中，选择`打开`或`另存为`, 这里我另存到桌面，

![20210807195559](https://gitee.com/alingyisheng/tupian/raw/master/img/20210807195559.png)

15. 这就是下载到桌面的这个文件：

![20210807195751](https://gitee.com/alingyisheng/tupian/raw/master/img/20210807195751.png)

16. 直接双击打开，在弹出的对话框中，选择`Start`，当然，下载过程中也可以暂停，点`Pause`键就好了。

![20210807195929](https://gitee.com/alingyisheng/tupian/raw/master/img/20210807195929.png)

17. 下载开始后，会在桌面生成一个`同名`文件夹，就是下载的影像数据存储的地方，这个数据下载的速度可能会很慢（受到你的网速限制），不要着急，要有耐心，我验证了是可以下载成功的。

![20210807200241](https://gitee.com/alingyisheng/tupian/raw/master/img/20210807200241.png)

18. 下载成功后的数据展示，让我们看看文件夹里面的DICM影响文件数据是这样的，而且是按编号排列的：

![20210807200748](https://gitee.com/alingyisheng/tupian/raw/master/img/20210807200748.png)
## 验证是否能导入Mimics
1. 我把这些文件拷贝到一个叫`test`的文件夹里，

![20210807201032](https://gitee.com/alingyisheng/tupian/raw/master/img/20210807201032.png)

2. 打开`Mimics`，点击菜单栏中的`File`，点击`New project wizard`,

![20210807201544](https://gitee.com/alingyisheng/tupian/raw/master/img/20210807201544.png)

3. 在弹出的对话框中，选择桌面的`test`文件，然后点击`next`,

![20210807201849](https://gitee.com/alingyisheng/tupian/raw/master/img/20210807201849.png)

4. 文件开始导入，

![20210807202033](https://gitee.com/alingyisheng/tupian/raw/master/img/20210807202033.png)

5. 导入成功后，我们可以查看图像的一些信息，也能够预览图像，

![20210807202238](https://gitee.com/alingyisheng/tupian/raw/master/img/20210807202238.png)

6. 然后点击`Convert`,  在弹出的对话框中确认图像的方向，没有错误的化，就选择`ok`。

![20210807202421](https://gitee.com/alingyisheng/tupian/raw/master/img/20210807202421.png)

7. 成功了，我们可以在`Mimcs`中查看这个肺CT的影像数据了，再也不用担心没有影像数据了，可以进一步学习`mimics`的用法了。世界真美好！

![20210807202704](https://gitee.com/alingyisheng/tupian/raw/master/img/20210807202704.png)

好吧，你学会了么？找到这个网站的时候我十分兴奋，如果没有影像数据，真的没法继续学习这个软件了。既然炊具和食材都有了，那我们赶紧研究菜谱吧，下一期视频我将从今天下载的肺CT数据开始，了解一下Mimics中肺CT的应用。如果你感兴趣的化，记得关注呃。今天的内容就是这些，我是阿狸，再见。
