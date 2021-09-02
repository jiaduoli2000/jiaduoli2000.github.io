---
title: R语言-14-cox回归-列线图绘制
author: 阿狸的Blog
date: '2021-07-29'
slug: cox-nomogram
categories:
  - r
tags:
  - 统计
---
前面的视频我们了解了关于生存分析的[KM曲线和log-rank检验](https://www.bilibili.com/video/BV1L64y1b7YA)，[Cox回归的多因素生存分析](https://www.bilibili.com/video/BV1Q54y1J7o9/)，以及如何[评估Cox模型假设有效性](https://www.bilibili.com/video/BV1KP4y147Av/)。在建立了cox回归模型之后，如何把模型展示出来，这就需要用到“列线图”。列线图，也叫nomogram图，是一种直观有效地展示Cox回归结果的一种方法。我们今天就来了解一下列线图。

## 关于列线图（Nomogram）
### 1. 列线图长什么样子？
下面就是列线图的样子：
![20210720171837](https://gitee.com/alingyisheng/tupian/raw/master/img/20210720171837.png)
最左边的给出了一些变量名称，包括：points(评分)，age（年龄），sex（性别），ECG（心电图），Total Points（总分），Risk（风险）。每个变量名右侧都有一条标有数值的直线轴，代表不同的评分或概率。

### 2. 怎么看这个图？
就那上图来说。我们想知道年龄45岁 (age=45) 的女性（sex=1）的患病风险，只需要将age=45岁向“ points（评分）”轴投射，则：points=50；同理 sex=1 时，points≈37。两者相加则“ Total points=87”；将此数值在“ Total points ”轴上向“ Risk ”概率轴投射，则可知风险大概在0.4和0.5之间。（参见图中红线）


## 如何制作列线图
下面我们看看如何通过R语言来绘制列线图。
### 1. 载入R包
我们打开Rstudio后，首先载入要用到的R包，如果没有安装的话，记得先安装。
```
library(survival) 
library(survminer)
library(rms)  
library(Hmisc)
library(grid) 
library(lattice)
library(Formula)
library(ggplot2)  

```

### 2. 载入数据
今天我们用到的数据是survival程序包的lung数据：
```
data("lung")
head(lung)
```

载入后我们看一下这个数据集：
![20210720180408](https://gitee.com/alingyisheng/tupian/raw/master/img/20210720180408.png)

在这个书籍中我们可以添加变量标签以便后续说明
```
lung$sex <- factor(lung$sex,
                   levels = c(1,2),
                   labels = c("male", "female"))
```
这里，1 = male ，2 = female。


### 3. 数据打包
按照nomogrm（）函数的要求，需要先“打包”数据，这是绘制列线图的关键步骤。"打包"用到的是`datadist（）`函数, 该函数计算预测器的统计摘要，以自动估计和绘制效果。
用户通常将最终的数据框提供给`datadist（）`函数，并使用options函数设置数据分布。
注意，如果修改数据框中的数据，则需要使用`datadist（）`函数重置分布摘要。在R中输入:  ??datadist可以查看详细说明。
```
dd=datadist(lung)
options(datadist="dd")
```

### 4. 构建Cox模型
这里我们用 `cph()`函数来拟合Cox比例风险回归模型, 你也可以尝试使用 `coxph()`函数来拟合，自己可以尝试一下。
```
res.cox <- cph(Surv(time, status) ~ age + sex, data = lung)
```

#### 绘制森林图展示多分类变量

```
str(lung)#该数据将所有变量都转换为数值型
ggforest(res.cox, data = lung,  #数据集
         main = 'Hazard ratio',  #标题
         cpositions = c(0.05, 0.15, 0.35),  #前三列距离
         fontsize = 1, #字体大小
         noDigits = 3 #保留HR值以及95%CI的小数位数
) 
```

### 5. 构建生存函数

```
med <- Quantile(res.cox) # 计算中位生存时间
surv <- Survival(res.cox) # 构建生存概率函数

```

### 6. 绘图：预测中位生存时间
```
nom <- nomogram(res.cox, fun=function(x) med(lp=x),
                funlabel="Median Survival Time")
plot(nom)
```
生成的图像是这样的，注意图的最下一行是“ Median Survival Time（中位生存时间）”。

![20210720214511](https://gitee.com/alingyisheng/tupian/raw/master/img/20210720214511.png)

### 7. 绘图：预测生存概率
这里要注意的是，lung数据的“time”是以“天”为单位。
```
nom <- nomogram(res.cox, fun=list(function(x) surv(365, x),
                             function(x) surv(730, x)),
                funlabel=c("1-year Survival Probability",
                           "2-year Survival Probability"))
plot(nom, xfrac=.6)
```

生成的图像是这样的，注意图的最下一行是“ 1-year Survival Probability（1年生存率）”和“2-year Survival Probability（2年生存率）”。

![20210720215102](https://gitee.com/alingyisheng/tupian/raw/master/img/20210720215102.png)

## 评价COX回归的预测效果
我们主要计算“ C-index ”即C-指数和绘制矫正曲线，来对Cox回归的预测效果进行评价。
### 1. 计算C-指数
```
rcorrcens(Surv(time,status) ~ predict(res.cox), data =lung)
```

```
Somers' Rank Correlation for Censored Data    Response variable:Surv(time, status)

                     C    Dxy  aDxy    SD    Z     P   n
predict(res.cox) 0.397 -0.206 0.206 0.051 4.03 1e-04 228
```

### 2. 绘制校正曲线
这里对参数做一些说明：
- 绘制校正曲线前需要在模型函数中添加参数x=T, y=T，详细参考帮助
- u需要与之前模型中定义好的time.inc一致，即365或730；
- m要根据样本量来确定，由于标准曲线一般将所有样本分为3组（在图中显示3个点）
- m代表每组的样本量数，因此m*3应该等于或近似等于样本量；
- b代表最大再抽样的样本量

#### 重新调整模型函数`res.cox2`
这里是加上了`x=T, y=T，time.inc = 365`三个参数：
```
res.cox2 <- cph(Surv(time,status) ~ age+sex, data =lung, x=T, y=T, surv=TRUE, time.inc = 365)
```

#### 构建校正曲线
通过`??rms::calibrate`查看详细参数说明
```
cal1 <- calibrate(res.cox2, cmethod='KM', method="boot", u=365, m=76, B=228)
```

#### 绘制校正曲线
```
par(mar=c(8,5,3,2),cex = 1.0)
plot(cal1,lwd=2,lty=1,
     errbar.col=c(rgb(0,118,192,maxColorValue=255)),
     xlim=c(0.25,0.6),ylim=c(0.15,0.70),
     xlab="Nomogram-Predicted Probability of 1-Year DFS",
     ylab="Actual 1-Year DFS (proportion)",
     col=c(rgb(192,98,83,maxColorValue=255)))
```

生成的校准曲线图是这样的：
![20210720222646](https://gitee.com/alingyisheng/tupian/raw/master/img/20210720222646.png)


## 参考文献
[R绘制Nomogram图的学习笔记 - R语言论坛 - 经管之家(原人大经济论坛) (pinggu.org)](https://bbs.pinggu.org/thread-4115525-1-1.html)
[Introduction to the RMS Package | R-bloggers](https://www.r-bloggers.com/2016/07/introduction-to-the-rms-package/)
[Logistic、Cox回归之图形化呈现（R语言中绘制Nomogram） - 统计与作图 - 专业医生社区，医学、药学、生命科学、科研学术交流 (dxy.cn)](https://www.dxy.cn/bbs/newweb/pc/post/27318323)
[使用 R 进行生存分析 - 王诗翔 (shixiangwang.github.io)](https://shixiangwang.github.io/home/cn/post/r-survival/#fn7)
[从一篇预测模型文章学习nomogram列线图 (360doc.com)](http://www.360doc.com/content/19/0115/18/52645714_809076882.shtml)
[生存模型的calibration需要注意的一个问题_FanJin的博客-CSDN博客](https://blog.csdn.net/fjsd155/article/details/91354441)
[TCGA+biomarker——Cox回归森林图 - 简书 (jianshu.com)](https://www.jianshu.com/p/e511fc9c87d9)
[预测模型 | 7. 决策曲线分析（DCA）：基于ggDCA包 (qq.com)](https://mp.weixin.qq.com/s?__biz=Mzg2MjU2NDQwMg==&mid=100010922&idx=1&sn=eae80cc7ab9e3fd2d66864609520921b&chksm=4e0752f77970dbe170cf969ab9baaf1dbbca8953ff4c2502e54595db5cffec4dc17f76267226#rd)
[预测模型 | 5. 模型评估：校准曲线 (qq.com)](https://mp.weixin.qq.com/s?__biz=Mzg2MjU2NDQwMg==&mid=2247494524&idx=1&sn=10e25b1ca431b1cf5f74312afd9f8ad9&chksm=ce075221f970db37bd143ed3a3d924a47e411c2b05e61f51fa9543b887863ad11abe3c2dfc72&scene=21#wechat_redirect)


存在的疑问：
[R中RMS包中的psm和cph有什么区别 | 码农俱乐部 - Golang中国 - Go语言中文社区 (mlog.club)](https://mlog.club/article/4800376)
[用于计算Cox比例风险模型的coxph和cph函数有什么区别？ - Thinbug](https://www.thinbug.com/q/20742720)
