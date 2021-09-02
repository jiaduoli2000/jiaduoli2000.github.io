---
title: Materialise Mimics-初识之安装
author: 阿狸的Blog
date: '2021-08-03'
slug: materialise-mimics-soft
categories:
  - 效率工具
tags:
  - mimics
---
# Materialise Mimics
## 初识
[Materialise Mimics](https://www.materialise.com/zh-hans/medical/software/mimics-innovation-suite/products-services/mimics)，用于医学影像处理。CT和MRI的断层图像都能进行三维重建，输出为通用的三维格式，然后进行三维打印、科研、医疗、有限元分析等应用。

 软件功能：  
 - 导入DICOM，JPEG，TIFF，BMP，X射线或原始图像数据
 - 创建3D模型  
 - 执行解剖分析
 - 几乎模拟手术导出的用于3D分析，FEA网格划分，设计或3D打印的3D模型  
 - 使用分析原理促进复杂的解剖学测量
 - 评估肿瘤的大小或肿瘤的复杂性  
 - 调查并跟踪手术的结果
 - 预测用于手术的板和螺钉的正确尺寸
 - 检查软骨的厚度
 - 测量和分析进一步统计分析 

## 安装
### 1. 安装过程
官网提供机构注册，申请试用1个月，对于大多数爱好者，都无法申请。所以，为了学习，只能在某宝想些别的办法，这个就不具体说了。[百度分享链接](https://pan.baidu.com/s/1CNL16JOOo2WXYYJda_-VtQ) [提取码](bfvy)。按照压缩包中的安装方法进行安装就好了。
![20210803131430](https://gitee.com/alingyisheng/tupian/raw/master/img/20210803131430.png)
有条件的化，还是最好支持正版，一般个人也是买不起。这里仅作学习交流用。由于目前这个版本较低，有些功能可能受到限制。解压到本地文件夹：
![20210803132051](https://gitee.com/alingyisheng/tupian/raw/master/img/20210803132051.png)
来看看文件夹中包含的内容:
![20210803132321](https://gitee.com/alingyisheng/tupian/raw/master/img/20210803132321.png)
我的电脑是64位，Windows10操作系统，以此为例进行安装。首先，打开文件夹`64位`，
![20210803132822](https://gitee.com/alingyisheng/tupian/raw/master/img/20210803132822.png)。
选择MIS的版本，`Medical`或`Research`，双击安装。这里选择`Medical`。下面开始提取文件（过程较慢）：
![20210803133208](https://gitee.com/alingyisheng/tupian/raw/master/img/20210803133208.png)
提取完成之后会弹出安装界面，点击`Next`，方框中划`√`，点击`Next`,
![20210803133504](https://gitee.com/alingyisheng/tupian/raw/master/img/20210803133504.png)
点击`Next`, 这里`CHoose location`选择了默认的`Europe - Africa`
![20210803133730](https://gitee.com/alingyisheng/tupian/raw/master/img/20210803133730.png)
这里安装类型选择`Complete`, 存储位置选择：`E:\mimics\`,点击`Next`,点击`Next`,点击`Install`。
![20210803134015](https://gitee.com/alingyisheng/tupian/raw/master/img/20210803134015.png)
正在安装，这个过程比较慢，大概10分钟时间，
![20210803134406](https://gitee.com/alingyisheng/tupian/raw/master/img/20210803134406.png)
点击`finish`完成安装。
![20210803135545](https://gitee.com/alingyisheng/tupian/raw/master/img/20210803135545.png)
查看桌面，可以看到下面两个快捷方式：
![20210803135707](https://gitee.com/alingyisheng/tupian/raw/master/img/20210803135707.png)
安装完毕后，进入刚才的安装路径，
![20210803140113](https://gitee.com/alingyisheng/tupian/raw/master/img/20210803140113.png)
如果发现里面没有MatConvert这个文件夹，检查一下C:\Program Files\Materialise（如果存在这个文件夹）里面有没有
![20210803140337](https://gitee.com/alingyisheng/tupian/raw/master/img/20210803140337.png)
如果两个地方都找不到MatConvert，再双击对应的MatConvert_xXX.msi安装，自动安装到C:\Program Files\Materialise 之中，然后最好重启一下计算机

### 2.破解过程
到cgp_mis17文件夹内根据自己安装的版本选择32位还是64位，我这里选择64位：
![20210803140555](https://gitee.com/alingyisheng/tupian/raw/master/img/20210803140555.png)
根据对应文件夹内的instruction.txt进行破解：
![20210803151411](https://gitee.com/alingyisheng/tupian/raw/master/img/20210803151411.png)
将`3-matic.research.9.0.0.231.xXX-patch.exe`复制到3-matic的安装目录中，
![20210803151702](https://gitee.com/alingyisheng/tupian/raw/master/img/20210803151702.png)
双击运行，（如果安装目录在C盘内，并且系统为Win7/8以上，需右键“以管理员身份运行”，下一条同理）
![20210803151845](https://gitee.com/alingyisheng/tupian/raw/master/img/20210803151845.png)
点击`patch`,
![20210803152205](https://gitee.com/alingyisheng/tupian/raw/master/img/20210803152205.png)
将`materialize.matconvert.7.0(xXX)-patch.exe`复制到`MatConvert`的安装目录中，
![20210803152527](https://gitee.com/alingyisheng/tupian/raw/master/img/20210803152527.png)
双击运行，点击`patch`,
![20210803152527](https://gitee.com/alingyisheng/tupian/raw/master/img/20210803152527.png)
至此，`3-matic`和`MatConvert`破解激活完毕。

### 3.启动过程
`Mimics17_start_xXX_(XX).exe`为`MIMICS`的启动器，每次需用它才能启动`MIMICS`。
![20210803153231](https://gitee.com/alingyisheng/tupian/raw/master/img/20210803153231.png)
将三个启动器复制到MIMICS的安装目录中，
![20210803153548](https://gitee.com/alingyisheng/tupian/raw/master/img/20210803153548.png)
按照括号内数字从小到大，逐一运行看看哪个能成功启动`MIMICS`,如果系统配置比较高，可能`50`就能够启动。我的选择`50`好像不行。
![20210803154730](https://gitee.com/alingyisheng/tupian/raw/master/img/20210803154730.png)
启动不了的话（会弹出一个CodeMeter之类的错误窗口），再试试150的启动器，看看能不能稳定启动，

![20210803154929](https://gitee.com/alingyisheng/tupian/raw/master/img/20210803154929.png)

这里我的可以了，打开后的界面是这样的：

![20210803155238](https://gitee.com/alingyisheng/tupian/raw/master/img/20210803155238.png)

下面说明书的内容我就看不懂了，但还是记录下来。再不行就试试255的。还不行的话……呃这系统配置略低了吧……自己找个十六进制编辑器比较一下这几个文件不同的地方（附带的`txt`文件里也可以找到），有个位置就是修改这个值的，目测是`32位int，little endian`，就这样选出一个能稳定启动MIMICS的启动器保留下来，删掉其他的。另外，桌面快捷方式似乎修改不了。
