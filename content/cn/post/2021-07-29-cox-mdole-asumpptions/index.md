---
title: R语言-Cox回归-评估Cox模型假设有效性
author: 阿狸的Blog
date: '2021-07-29'
slug: cox-mdole- asumpptions
categories:
  - r
tags:
  - 统计
---
# Cox模型假设
之前，我们描述了分析生存数据的基本方法，以及处理几个因素影响生存过程的情况的Cox比例风险方法。

在这篇文章中，我们继续描述评估Cox模型假设有效性的方法。

**请注意，如果使用不当，统计模型可能会产生误导性的结论。因此，检查给定的模型是否是数据的适当表示是很重要的。**


## Cox模型的诊断学
考克斯比例风险模型做了几个假设。因此，重要的是评估拟合的考克斯回归模型是否充分描述了数据。

在这里，我们将讨论考克斯模型的三种类型的对角线性:
- 测试比例危险假设。
- 检查有影响的观察结果(或异常值)。
- 检测对数风险和协变量之间关系的非线性。

为了检验这些模型假设，本文使用了残差法。Cox模型的常见残差包括：
-   _Schoenfeld residuals_ 检查比例危险假设
-   _Martingale residual_ 评估非线性
-   _Deviance residual_ (Martinguale残差的对称变换), 检查有影响力的观察结果

## R检验Cox模型的有效性
### 安装和加载所需的R包
我们将使用两个R包:
-   **survival** 计算生存分析
-   **survminer** 可视化生存分析结果
-   安装包
```
install.packages(c("survival", "survminer"))
```
-   载入包
```
library("survival") 
library("survminer")
```

### 计算一个Cox模型
我们将使用肺数据集和生存包中的coxph()函数。要计算考克斯模型，请键入以下内容:
```
library("survival") r
es.cox <- coxph(Surv(time, status) ~ age + sex + wt.loss, data = lung) res.cox
```

```
Call:
coxph(formula = Surv(time, status) ~ age + sex + wt.loss, data = lung)
            coef exp(coef) se(coef)     z      p
age      0.02009   1.02029  0.00966  2.08 0.0377
sex     -0.52103   0.59391  0.17435 -2.99 0.0028
wt.loss  0.00076   1.00076  0.00619  0.12 0.9024
Likelihood ratio test=14.7  on 3 df, p=0.00212
n= 214, number of events= 152 
   (14 observations deleted due to missingness)
```

### 测试比例危险假设
可以使用基于缩放的Schoenfeld残差的统计测试和图形诊断来检查比例风险（pH）假设。

**原则上，舍恩菲尔德残差与时间无关。显示出对时间的非随机模式的情节是违反PH假设的证据**。

函数cox.zph()(在生存包中)为检验Cox回归模型拟合中包含的每个协变量的比例风险假设提供了一个方便的解决方案。

对于每个协变量，函数cox.zph()将相应的缩放Schoenfeld残差集合与时间相关，以测试残差与时间之间的独立性。此外，它还对整个模型执行全局测试。

**比例风险假设被残差与时间之间不显著的关系所支持，并被显著的关系所驳斥。**

为了说明测试，我们首先使用肺数据集(在生存包中)计算Cox回归模型：
```
library("survival") 
res.cox <- coxph(Surv(time, status) ~ age + sex + wt.loss, data = lung) res.cox
```
```
Call:
coxph(formula = Surv(time, status) ~ age + sex + wt.loss, data = lung)
            coef exp(coef) se(coef)     z      p
age      0.02009   1.02029  0.00966  2.08 0.0377
sex     -0.52103   0.59391  0.17435 -2.99 0.0028
wt.loss  0.00076   1.00076  0.00619  0.12 0.9024
Likelihood ratio test=14.7  on 3 df, p=0.00212
n= 214, number of events= 152 
   (14 observations deleted due to missingness)
```
要测试比例危险(PH)假设，请键入以下命令：
```
test.ph <- cox.zph(res.cox) 
test.ph
```
```
            rho chisq     p
age     -0.0483 0.378 0.538
sex      0.1265 2.349 0.125
wt.loss  0.0126 0.024 0.877
GLOBAL       NA 2.846 0.416
```

**从上面的输出来看，检验对每个协变量都没有统计学意义，全局检验也没有统计学意义。因此，我们可以假设成比例的危险。**

可以使用函数ggcozph()[在survminer包中]进行图形诊断，该函数为每个协变量生成缩放的舍恩菲尔德残差相对于转换时间的图形。

```
ggcoxzph(test.ph)
```
![20210710181054](https://gitee.com/alingyisheng/tupian/raw/master/img/20210710181054.png)
在上图中，实线是拟合到打印的平滑样条曲线，虚线表示拟合周围的+/-2标准误差带。

**请注意，系统偏离水平线表示非比例风险，因为比例风险假设估计值β1、β2、β3随时间变化不大。**

从图形检查来看，没有随时间变化的模式。比例风险的假设似乎支持协变量性别(回想一下，这是一个二级因素，解释了图表中的两个波段)、体重损失和年龄。

另一种检查比例风险的图形化方法是绘制log(-log(S(T)与t或log(T)的关系图，并寻找并行度。这只适用于分类协变量。

违反比例风险假设可通过以下方式解决：
-   添加协变量*时间交互
-   Stratification 成层

分层对于“讨厌的”混杂因素是有用的，在这种情况下，你不需要估计效果。你不能检查分层变量的影响(约翰福克斯&桑福德韦斯伯格)。

要了解更多关于如何应对非比例危险的信息，请阅读以下文章:
-   Jadwiga Borucka, PAREXEL, Warsaw, Poland. [Extensions of cox model for non-proportional hazards purpose](http://www.lexjansen.com/phuse/2013/sp/SP07.pdf). 2013.
-   John Fox & Sanford Weisberg. [Cox Proportional-Hazards Regression for Survival Data in R](https://socserv.socsci.mcmaster.ca/jfox/Books/Companion/appendix/Appendix-Cox-Regression.pdf).
-   Max Gordon. [Dealing with non-proportional hazards in R](https://www.r-bloggers.com/dealing-with-non-proportional-hazards-in-r/). March 29, 2016.






### 测试有影响力的观察结果
为了测试有影响的观测值或异常值，我们可以将以下两者之一可视化:
- 偏差残差或
- dfbeta值

[在survminer软件包中]函数ggcoxDiagnostics()为检查有影响力的观测提供了一个方便的解决方案。简化格式如下：
```
ggcoxdiagnostics(fit, type = , linear.predictions = TRUE)
```

>-   fit: 类的一个对象
>-   type: 要在Y轴上显示的残差类型。允许的值包括以下值之一:(“martingale”, “deviance”, “score”, “schoenfeld”, “dfbeta”, “dfbetas”, “scaledsch”, “partial”).
>-   linear.predictions: 一个逻辑值，指示是显示观测的线性预测(TRUE)还是仅显示X轴上的索引化观测(FALSE)。

指定参数type=“dfbeta”，将在依次删除每个观测值时绘制回归系数的估计变化；同样，type=“dfbetas”将生成系数除以其标准误差的估计变化。

例如：
```
ggcoxdiagnostics(res.cox, type = "dfbeta", linear.predictions = FALSE, ggtheme = theme_bw())
```

![20210710185330](https://gitee.com/alingyisheng/tupian/raw/master/img/20210710185330.png)
(死亡时间与年龄、性别和体重损失的Cox回归的dfbeta指数图)

上述指数图表明，将最大dfbeta值的大小与回归系数进行比较表明，即使年龄和体重损失的dfbeta值中的一些值与其他值相比较大，但没有一个观测结果对单个观测结果有很大影响。

还可以通过可视化偏差残差来检查异常值。偏差残差是鞅残差的归一化变换。这些残差应该大致对称地分布在零附近，标准差为1。
- 与预期存活时间相比，正值对应于“过早死亡”的个体。
- 负值对应于“活得太久”的个体。
- 很大或很小的值都是离群值，模型无法很好地预测这些值。

偏差残差示例:
```
ggcoxdiagnostics(res.cox, type = "deviance", linear.predictions = FALSE, ggtheme = theme_bw())
```

![20210710212754](https://gitee.com/alingyisheng/tupian/raw/master/img/20210710212754.png)

**该模式在0附近看起来相当对称。**




### 测试非线性
通常，我们假设连续协变量具有线性形式。然而，这个假设应该被检查。

绘制连续协变量的鞅残差图是检测非线性的常用方法，换句话说，是评估协变量的函数形式。对于给定的连续协变量，图中的模式可能表明变量不合适。

非线性不是分类变量的问题，所以我们只研究鞅残差和部分残差相对于连续变量的图。

鞅残差可以表示(-INF，+1)范围内的任何值:
- martinguale残差值接近1表示“过早死亡”的个体，
- 而大负值对应的是“活得太久”的个体。

为了评估Cox比例风险模型中连续变量的函数形式，我们将使用函数ggcoxfunctional()[在survminer R包中]。

函数ggcoxfunctional()显示零cox比例风险模型的连续协变量对鞅残差的图。这可能有助于正确选择考克斯模型中连续变量的函数形式。具有下限函数的拟合线应该是线性的，以满足考克斯比例风险模型的假设。

例如，要评估年龄的功能形式，请键入以下内容：
```
ggcoxfunctional(Surv(time, status) ~ age + log(age) + sqrt(age), data = lung)
```
![20210710213611](https://gitee.com/alingyisheng/tupian/raw/master/img/20210710213611.png)

看起来，这里有轻微的非线性。

### 小结
我们描述了如何使用生存包和Survminer包来评估Cox模型假设的有效性。
