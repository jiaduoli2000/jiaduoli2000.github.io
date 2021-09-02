---
title: Mimics-气管肺的重建
author: 阿狸的Blog
date: '2021-08-11'
slug: mimics-lung-seg
categories:
  - 效率工具
tags:
  - mimics
---

## 1. 导入数据

打开`mimics 21.0`,

![20210811164115](https://gitee.com/alingyisheng/tupian/raw/master/img/20210811164115.png)

选择`New Project`, 在弹出的对话框中选择数据，这里是`肺CT示例-1`，

![20210811164243](https://gitee.com/alingyisheng/tupian/raw/master/img/20210811164243.png)

数据导入完成并显示，

![20210811164441](https://gitee.com/alingyisheng/tupian/raw/master/img/20210811164441.png)

## 2. Segment airway 重建气道

选择最上方菜单栏`ADVANCED SEGMENT`, 然后选择`Segment airway`, → `start`		

![20210811164750](https://gitee.com/alingyisheng/tupian/raw/master/img/20210811164750.png)

用弹出的画笔在气管上标记两个点，

![20210811164946](https://gitee.com/alingyisheng/tupian/raw/master/img/20210811164946.png)

标记之后开始自动建立气道模型

![20210811165108](https://gitee.com/alingyisheng/tupian/raw/master/img/20210811165108.png)

这里了解一些操作方式：
- 光标放在工作区，点击空格键，可以在单个工作区和4个界面之间进行切换
- 鼠标右键按住后移动：调节CT灰度值（肺窗和纵隔窗之间切换）
- 鼠标`右键+Ctrl`: 放大或缩小CT图像
- 鼠标滚珠持续按住：可以平移图像。或者`shift+右键`。

![20210811165235](https://gitee.com/alingyisheng/tupian/raw/master/img/20210811165235.png)

然后点击`calculate part`,

![20210811170418](https://gitee.com/alingyisheng/tupian/raw/master/img/20210811170418.png)

选中重建好的`airway`, 点击右键，弹窗中可以选择`smooth`来调整模型光滑度，

![20210811170627](https://gitee.com/alingyisheng/tupian/raw/master/img/20210811170627.png)

也可以选择`properties`修改名字，或颜色。

![20210811170701](https://gitee.com/alingyisheng/tupian/raw/master/img/20210811170701.png)

## Centerline label 标记中心线

选择`New centerline label`, 选择`Smoothed_Aiway1`, 点击`next`,

![20210811172342](https://gitee.com/alingyisheng/tupian/raw/master/img/20210811172342.png)

在弹出的对话框中，根据医学知识检查软件标记的是否正确，错误的化可以重新标识和更改，然后点击`apply`。

![20210811172631](https://gitee.com/alingyisheng/tupian/raw/master/img/20210811172631.png)

## Segment lung and lobes 肺叶的重建和分割
点击`Segment lung and lobes`, 选择刚才标记的中心线`Centerline 1`，然后点击`next`,

![20210811173133](https://gitee.com/alingyisheng/tupian/raw/master/img/20210811173133.png)

重建完毕，肺叶及肺裂已经被分割出来了，

![20210811173521](https://gitee.com/alingyisheng/tupian/raw/master/img/20210811173521.png)

如果肺列识别的不好，可以点击上图中`Edit Fissures`，进行手动编辑。可以增加点，删除点等。

![20210811173829](https://gitee.com/alingyisheng/tupian/raw/master/img/20210811173829.png)

可以在CT肺窗中查看肺裂分割线，看软件分析的是否准确，不准确的化可以进行修正

![20210811174303](https://gitee.com/alingyisheng/tupian/raw/master/img/20210811174303.png)

编辑完成之后，选择`next`，肺叶的维重建就完成了。

![20210811181134](https://gitee.com/alingyisheng/tupian/raw/master/img/20210811181134.png)

## cut through points 分割肺叶
点击`cut through points`, 然后点击新建`new`，

![20210811181811](https://gitee.com/alingyisheng/tupian/raw/master/img/20210811181811.png)

新建了一个`CP4`，然后在肺窗中标记肺裂，然后选择要分割的肺叶，然后选择以`CP4`为界限分割,然后点击`ok`, 就可以分割了。

![20210811184146](https://gitee.com/alingyisheng/tupian/raw/master/img/20210811184146.png)

可以看到右下肺已经被分割成两部分了。这里主要学习这个功能，实际分割要在完成肺血管成像之后再进行，才会对临床有知道意义。

![20210811184314](https://gitee.com/alingyisheng/tupian/raw/master/img/20210811184314.png)

好吧，今天的内容就是这些，不足之处还请批评指正。本节涉及的主要模块是：
- Segment airway 重建气道
- Centerline label 标记中心线
- Segment lung and lobes 肺叶的重建和分割
- cut through points 分割肺叶
