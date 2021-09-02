---
title: R语言-生存分析
author: 阿狸的Blog
date: '2021-07-29'
slug: survival analysis
categories:
  - r
tags:
  - 统计
---
## 生存分析基础
生存分析对应于一组统计方法，用于调查感兴趣的事件发生所需的时间。

生存分析用于各种领域，例如：
- 癌症研究用于患者生存时间分析，
- 社会学用于“事件-历史分析”，
- 工程学用于“失效-时间分析”。

在癌症研究中，典型的研究问题是：
- 某些临床特征对患者生存的影响是什么？
- 一个人存活3年的概率是多少？
- 不同患者组之间的存活率有差异吗？

### 目标
本章的目的是描述生存分析的基本概念。在癌症研究中，生存分析大多采用以下方法：
- Kaplan-Meier图可视化生存曲线，
- Log-ranch检验比较两组或多组生存曲线，
- Cox比例风险回归描述变量对生存的影响。

在这里，我们将首先解释生存分析的基本概念，包括：
- 如何生成和解释生存曲线，
- 以及如何量化和测试两组或多组患者之间的生存差异。

然后，我们将继续描述使用Cox比例风险模型进行的多变量分析。

### 基本概念
在这里，我们首先定义生存分析的基本术语，包括：
- 生存时间和事件
- 删失值
- 生存函数和危险函数

### 癌症研究中的生存时间和事件类型
有不同类型的事件，包括：
- 复发、
- 进展、
- 死亡

从“治疗反应”(完全缓解)到感兴趣事件发生的时间通常称为生存时间(或事件发生时间)。

癌症研究中最重要的两个衡量标准包括：i)**死亡时间**；ii)**无复发生存时间**，这与治疗反应和疾病复发之间的时间相对应。它也被称为**无病生存时间**和无事件生存时
间。

### 删失值
如上所述，生存分析的重点是发生感兴趣的事件(复发或死亡)之前的预期持续时间。然而，有些人在研究期间可能没有观察到这一事件，从而产生了所谓的经审查的观察结果。

审查可能以以下方式出现：
- 患者(尚未)在研究期间没有经历感兴趣的事件，如复发或死亡；
- 患者在研究期间失去随访；
- 患者经历不同的事件，使得进一步随访变得不可能。
这种类型的审查，称为正确审查，在生存分析中进行处理。

### 生存和危险函数
用两个相关的概率来描述生存数据：生存概率和危险概率。

生存概率，也称为生存函数S(T)，是个体从时间起点(例如癌症诊断)存活到指定未来时间t的概率。

危险概率, 用h(T)表示，是在时间t被观察的个体在该时间发生事件的概率。

**请注意**，与侧重于没有事件的幸存者功能不同，危险功能侧重于发生的事件。

### Kaplan-Meier生存估计
Kaplan-Meier(KM)方法是一种非参数方法，用于根据观察到的生存时间估计生存概率(Kaplan and Meier，1958)。
时间ti时的存活概率S(Ti)计算如下：
![20210702165204](https://gitee.com/alingyisheng/tupian/raw/master/img/20210702165204.png)
估计概率(S(T))是仅在每个事件发生时改变值的阶跃函数。也可以计算生存概率的置信区间。
KM生存曲线是KM生存概率与时间的关系图，它提供了一个有用的数据汇总，可用于估计中位生存时间等度量。

### R中的生存分析
#### 安装和加载所需的R包
我们将使用两个R包：
-   _survival_ 计算生存分析
-   _survminer_ 生存分析结果的汇总和可视化
    
```
install.packages(c("survival", "survminer"))
library("survival")
library("survminer")

```

#### 示例数据集
我们将使用生存包中提供的肺癌数据。
```
data("lung") 
head(lung)

```
```
  inst time status age sex ph.ecog ph.karno pat.karno meal.cal wt.loss
1    3  306      2  74   1       1       90       100     1175      NA
2    3  455      2  68   1       0       90        90     1225      15
3    3 1010      1  56   1       0       90        90       NA      15
4    5  210      2  57   1       1       90        60     1150      11
5    1  883      2  60   1       0      100        90       NA       0
6   12 1022      1  74   1       1       50        80      513       0
```
-   inst: 机构代码
-   time: 存活时间(以天为单位)
-   status: 审查状态1=已审查，2=无效
-   age: 年龄(以年为单位)
-   sex: 男性=1 女性=2
-   ph.ecog: ECOG性能得分(0=良好，5=无效)
-   ph.karno: 卡诺夫斯基表现得分(差=0-好=100)由医生评定
-   pat.karno: 由患者评定的卡诺夫斯基表现评分
-   meal.cal: 用餐时摄入的卡路里
-   wt.loss: 最近六个月的减肥情况

#### 计算生存曲线：survfit()
我们想通过**性别**来计算生存概率。
[_survival_包]中的Survfit()函数可用于计算Kaplan-Meier生存估计。其主要论点包括：
- 使用函数surv()创建的生存对象
- 和包含变量的数据集。

若要计算生存曲线，请键入以下内容：
```
fit <- survfit(Surv(time, status) ~ sex, data = lung) 
print(fit)
```

```
Call: survfit(formula = Surv(time, status) ~ sex, data = lung)
        n events median 0.95LCL 0.95UCL
sex=1 138    112    270     212     310
sex=2  90     53    426     348     550
```

默认情况下，函数print()显示生存曲线的简短摘要。它打印观察次数、事件次数、中位数存活率和中位数的置信度。

如果要显示更完整的生存曲线摘要，请键入以下内容：
```
# Summary of survival curves 
summary(fit) 
# Access to the sort summary table 
summary(fit)$table
```

#### 访问survfit()返回的值
函数survfit()返回变量列表，包括以下组件：
-   n: 每条曲线上的受试者总数。
-   time: 曲线上的时间点。
-   n.risk: 在时间t处于危险状态的受试者数量
-   n.event: 在时间t发生的事件数。
-   n.censor: 在时间t无事件情况下退出风险集的被审查对象的数量。
-   lower,upper: 曲线的下限和上限。
-   strata: 表示曲线估计的分层。如果层不为空，则结果中有多条曲线。地层级别(因子)是曲线的标签。

可以按如下方式访问组件：
```
d <- data.frame(time = fit$time, n.risk = fit$n.risk, n.event = fit$n.event, n.censor = fit$n.censor, surv = fit$surv, upper = fit$upper, lower = fit$lower ) 
head(d)
```
```
  time n.risk n.event n.censor      surv     upper     lower
1   11    138       3        0 0.9782609 1.0000000 0.9542301
2   12    135       1        0 0.9710145 0.9994124 0.9434235
3   13    134       2        0 0.9565217 0.9911586 0.9230952
4   15    132       1        0 0.9492754 0.9866017 0.9133612
5   26    131       1        0 0.9420290 0.9818365 0.9038355
6   30    130       1        0 0.9347826 0.9768989 0.8944820
```

#### 可视化生存曲线
- 我们将使用函数ggsurvlot()[在Survminer R包中]来生成两组受试者的生存曲线。
- 还可以显示：
- 使用参数conf.int=true的幸存者函数的95%置信极限。
- 使用选项Risk.table按时间划分的风险个人数量和/或百分比。Risk.table的允许值包括：
       - TRUE或FALSE，指定是否显示Risk表。默认值为False。
        - “绝对”或“百分比”：按时间分别显示处于危险状态的对象的绝对数量和百分比。使用“abs_pct”可以显示绝对数字和百分比。
- 使用pval=true比较组的Log-Rank测试的p值。
- 使用参数surv.median.line计算中位数存活率的水平/垂直线。允许的值包括c(“None”、“hv”、“h”、“v”)之一。V：垂直，h：水平。

```
# Change color, linetype by strata, risk.table color by strata ggsurvplot(fit, pval = TRUE, conf.int = TRUE, risk.table = TRUE, # Add risk table risk.table.col = "strata", # Change risk table color by groups linetype = "strata", # Change line type by groups surv.median.line = "hv", # Specify median survival ggtheme = theme_bw(), # Change ggplot2 theme palette = c("#E7B800", "#2E9FDF"))
```
![20210702173809](https://gitee.com/alingyisheng/tupian/raw/master/img/20210702173809.png)

可以使用以下参数进一步自定义绘图：
-   _conf.int.style = “step”_ 更改置信区间波段的样式
-   _xlab_ 更改x轴标签
-   _break.time.by = 200_ 将x轴在时间间隔中中断by200
-   _risk.table = “abs_pct”_显示处于危险状态的个人的绝对数量和百分比
-   _risk.table.y.text.col = TRUE_ 和 _risk.table.y.text = FALSE_ 在风险表图例的文本注释中提供条形图而不是名称。
-   _ncensor.plot = TRUE_ to 画出在时间t处被审查的对象的数量。正如[马尔辛·科辛斯基](https://github.com/kassambara/survminer/issues/18)所建议的那样, 这是对生存曲线的一个很好的补充反馈，这样人们就可以意识到：生存曲线是什么样子的，风险集的数量是多少，风险集变小的原因是什么：是由事件造成的，还是由审查事件造成的？
-   _legend.labs_ 若要更改图例标签。
```
ggsurvplot( fit, # survfit object with calculated statistics. 
pval = TRUE, # show p-value of log-rank test. 
conf.int = TRUE, # show confidence intervals for # point estimaes of survival curves. conf.int.style = "step", # customize style of confidence intervals xlab = "Time in days", # customize X axis label. 
break.time.by = 200, # break X axis in time intervals by 200. 
ggtheme = theme_light(), # customize plot and risk table with a theme. risk.table = "abs_pct", # absolute number and percentage at risk. risk.table.y.text.col = T,# colour risk table text annotations. risk.table.y.text = FALSE,# show bars instead of names in text annotations # in legend of risk table. 
ncensor.plot = TRUE, # plot the number of censored subjects at time t surv.median.line = "hv", # add the median survival pointer. 
legend.labs = c("Male", "Female"), # change legend labels. 
palette = c("#E7B800", "#2E9FDF") # custom color palettes. 
)

```
![20210702203605](https://gitee.com/alingyisheng/tupian/raw/master/img/20210702203605.png)

Kaplan-Meier Plot可以解释如下：

>横轴(x轴)表示时间(以天为单位)，纵轴(y轴)表示存活的概率或存活人数的比例。这两条线代表了两组人的生存曲线。曲线上的垂直下落表示事件。曲线上的垂直刻度线意味着患者在这个时候被审查了。
   - 在时间零时，存活概率为1.0(或100%的参与者还活着)。
   - 在时间250，性别=1的生存概率约为0.55(或55%)，性别=2的生存概率约为0.75(或75%)。
   - 性别=1的中位生存期约为270天，性别=2的中位生存期约为426天，这表明与性别=1相比，性别=2的中位生存期较好


使用下面的代码可以获得每组的中位生存时间:
```
summary(fit)$table
```

```
      records n.max n.start events   *rmean *se(rmean) median 0.95LCL 0.95UCL
sex=1     138   138     138    112 325.0663   22.59845    270     212     310
sex=2      90    90      90     53 458.2757   33.78530    426     348     550
```

**每组的中位生存时间代表生存概率为0.5的时间。**

性别=1(男性组)的中位生存时间为270天，而性别=2(女性组)的中位生存时间为426天。与男性相比，女性肺癌患者似乎有生存优势。然而，要评估这种差异是否具有统计学意义，需要进行正式的统计测试，这一主题将在接下来的章节中讨论。

请注意，曲线尾部的置信范围很宽，很难做出有意义的解释。这可以用这样一个事实来解释，在实践中，通常会有患者在随访结束时失去随访或活着。因此，在对x轴的追踪结束之前缩短地块可能是明智的(Pocock等人，2002年)。

**使用参数xlim可以缩短生存曲线，如下所示：**
```
ggsurvplot(fit, 
conf.int = TRUE, 
risk.table.col = "strata", # Change risk table color by groups 
ggtheme = theme_bw(), # Change ggplot2 theme 
palette = c("#E7B800", "#2E9FDF"), 
xlim = c(0, 600))
```
![20210702205519](https://gitee.com/alingyisheng/tupian/raw/master/img/20210702205519.png)

请注意，可以使用参数FUN指定三种常用的转换：
-   “log”: 残存函数的对数变换，
-   “event”: 绘制累积事件 (f(y) = 1-y). 它也被称为累积发病率
-   “cumhaz” 绘制累积危险函数 (f(y) = -log(y))

**例如，要绘制累积事件，请键入以下内容:**
```
ggsurvplot(fit, 
conf.int = TRUE, risk.table.col = "strata", # Change risk table color by groups ggtheme = theme_bw(), # Change ggplot2 theme 
palette = c("#E7B800", "#2E9FDF"), 
fun = "event")
```
![20210702210107](https://gitee.com/alingyisheng/tupian/raw/master/img/20210702210107.png)
累积风险通常用于估计风险概率。它被定义为H(t)=对数(生存函数)=对数(S(t))。累积危害(H(t))可以解释为死亡率的累积力。换句话说，如果事件是一个可重复的过程，它对应于每个人在时间t之前预期的事件数量。

**要绘制累积危险，请键入以下内容:**
```
ggsurvplot(fit, 
conf.int = TRUE, 
risk.table.col = "strata", # Change risk table color by groups 
ggtheme = theme_bw(), # Change ggplot2 theme 
palette = c("#E7B800", "#2E9FDF"), 
fun = "cumhaz")
```
![20210702210424](https://gitee.com/alingyisheng/tupian/raw/master/img/20210702210424.png)




#### Kaplan-Meier生命表：生存曲线总结
如上所述，您可以使用函数SUMMARY()来获得生存曲线的完整摘要：

```
summary(fit)
```
还可以使用函数surv_Summary()[在survminer包中]来获取生存曲线的摘要。与默认的Summary()函数相比，surv_Summary()创建了一个数据框，其中包含来自survfit结果的精美摘要。

```
res.sum <- surv_summary(fit) 
head(res.sum)
```
```
  time n.risk n.event n.censor      surv    std.err     upper     lower strata sex
1   11    138       3        0 0.9782609 0.01268978 1.0000000 0.9542301  sex=1   1
2   12    135       1        0 0.9710145 0.01470747 0.9994124 0.9434235  sex=1   1
3   13    134       2        0 0.9565217 0.01814885 0.9911586 0.9230952  sex=1   1
4   15    132       1        0 0.9492754 0.01967768 0.9866017 0.9133612  sex=1   1
5   26    131       1        0 0.9420290 0.02111708 0.9818365 0.9038355  sex=1   1
6   30    130       1        0 0.9347826 0.02248469 0.9768989 0.8944820  sex=1   1
```

函数surv_summary()返回一个包含以下列的数据框:
-   time: 曲线具有阶跃的时间点。
-   n.risk: 在时间点处于危险状态的受试者数量。
-   n.event: 在时间t发生的事件数。
-   n.censor: 审查事件的数量。
-   surv: 生存概率的估计。
-   std.err: 生存标准误差。
-   upper: 置信区间的上限
-   lower: 置信区间的下限
-   strata: 表示曲线估计的分层。地层级别(因子)是曲线的标签。

在生存曲线已经用一个或多个变量拟合的情况下，surv_summary对象包含表示变量的额外列。这使得按地层或某些因素的组合来划分地质调查图的输出成为可能。

Surv_Summary对象还有一个名为‘table’的属性，其中包含有关生存曲线的信息，包括带有置信区间的生存中位数，以及每条曲线中的受试者总数和事件数。要访问属性‘table’，请键入以下内容：

```
attr(res.sum, "table")
```

#### 比较生存曲线的对数秩检验：Survdiff()
对数秩检验是比较两条或两条以上生存曲线最常用的方法。零假设是两组患者的存活率没有差异。对数秩检验是一种非参数检验，对生存分布没有任何假设。本质上，对数秩检验将每组中观察到的事件数量与如果零假设为真(即，如果生存曲线相同)的预期数量进行比较。对数秩统计量近似分布为卡方检验统计量。

[生存包]中的函数survdiff()可用于计算比较两条或多条生存曲线的对数秩检验。

Survdiff()的用法如下：
```
surv_diff <- survdiff(Surv(time, status) ~ sex, data = lung) 
surv_diff
```
```
Call:
survdiff(formula = Surv(time, status) ~ sex, data = lung)
        N Observed Expected (O-E)^2/E (O-E)^2/V
sex=1 138      112     91.6      4.55      10.3
sex=2  90       53     73.4      5.68      10.3
 Chisq= 10.3  on 1 degrees of freedom, p= 0.00131 
```

该函数返回组件列表，包括:
-   n: 每组中受试者的数量。
-   obs: 每组中观察到的加权事件数。
-   exp: 每组事件的加权预期数量。
-   chisq: 检验平等的chisquare统计量。平等性检验的平方统计量。
-   strata: 可选地，每个层中包含的受试者的数量。

>生存差异的对数秩检验p值为p=0.0013，表明不同性别群体的生存有显著差异。

#### 拟合复杂生存曲线
在本节中，我们将使用多种因素的组合来计算生存曲线。接下来，我们将通过一些因素的组合来划分ggsurvplot()的输出

1. 使用结肠数据集拟合(复杂)生存曲线
```
require("survival") 
fit2 <- survfit( Surv(time, status) ~ sex + rx + adhere, data = colon )
```

2. 使用survminer可视化输出。下图显示了根据rx &粘附值按性别变量分面的生存曲线。
```
# Plot survival curves by sex and facet by rx and adhere 
ggsurv <- ggsurvplot(fit2, fun = "event", conf.int = TRUE, 
ggtheme = theme_bw()) 

ggsurv$plot +theme_bw() + theme (legend.position = "right")+ facet_grid(rx ~ adhere)
```
![20210702213656](https://gitee.com/alingyisheng/tupian/raw/master/img/20210702213656.png)

### 小结
生存分析是一套用于数据分析的统计方法，其中感兴趣的结果变量是事件发生之前的时间。

生存数据通常根据两个相关函数进行描述和建模：
- 生存函数表示个体从起源时间存活到时间t之后某个时间的概率。它通常用卡普兰-迈耶方法来估计。对数秩检验可用于检验各组生存曲线之间的差异，如治疗组。
- 危险函数给出了某一时刻发生某一事件的瞬时可能性，给出了该时刻的存活率。它主要用作诊断工具或指定生存分析的数学模型。

在本文中，我们展示了如何使用两个R包装的组合来表现和可视化生存分析：生存（用于分析）和Survminer（用于可视化）。

### 参考文献
-   Clark TG, Bradburn MJ, Love SB and Altman DG. Survival Analysis Part I: Basic concepts and first analyses. British Journal of Cancer (2003) 89, 232 – 238
-   Kaplan EL, Meier P (1958) Nonparametric estimation from incomplete observations. J Am Stat Assoc 53: 457–481.
-   Pocock S, Clayton TC, Altman DG (2002) Survival plots of time-to-event outcomes in clinical trials: good practice and pitfalls. Lancet 359: 1686– 1689
