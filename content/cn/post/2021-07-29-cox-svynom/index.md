---
title: R语言-加权COX回归-列线图绘制
author: 阿狸的Blog
date: '2021-07-29'
slug: cox-svynom
categories:
  - r
tags:
  - 统计
---
前面的视频我们介绍了cox回归模型，今天的内容是绘制cox回归列线图。什么是列线图，来看看他的样子：

![20210717132142](https://gitee.com/alingyisheng/tupian/raw/master/img/20210717132142.png)

好像有点复杂，对了，列线图还有一个名字叫诺莫图（Nomogram），这图到底是干啥用的咧？列线图已经成为临床医生非常有用的工具，因为它们可以根据患者的特征提供个性化的”预测“。呃，知道了，列线图原来是用来预测的，听起来有点像算卦。而且有人认为，列线图比传统的TNM分期系统更有优势。那么，问题又来了，列线图能预测啥呢？简单说：概率。复杂说：基于多个变量的值预测一定的临床结局或者某类事件发生的概率。

好吧，那我们今天就用R包SvyNom中的胃癌数据集，来了解一下列线图的绘制过程。其实，我们不能只了解列线图的绘制方法。当我们绘制好一个列线图之后，还要评估它的表现。如何评估？根据两个方面，一是辨别能力；二是校准。辨别能力，通过计算C指数评估。校准，通过校准曲线图评估。

## 绘制列线图
好，让我们开始吧，我们打开RStudio，我安装的R版本是4.1，然后加载数据包：
```
library("rms")
library("survival")
library("survey")
library("SvyNom")
```

然后进行导入数据, 在此示例数据集中，缺失值的观测值被排除在外。
```
data("noNA", package = "SvyNom")
```

### 数据集介绍:[noNA: 胃癌病例对照研究](https://cran.r-project.org/web/packages/SvyNom/SvyNom.pdf)
![20210717150707](https://gitee.com/alingyisheng/tupian/raw/master/img/20210717150707.png)
这项研究包括1999年1月至2007年7月在纪念斯隆-凯特琳癌症中心接受化疗的所有转移性胃/胃食管交界处(GEJ)腺癌患者。大多数转移性胃癌患者在确诊后一年内死亡，只有不到15%的患者存活两年或更长时间。这项研究的目的是为了更好地描述这些具有特殊存活率的患者的特征。由於要取得所有这些病人所需的资料，需要翻查他们的医疗纪录，而这会耗费太多时间，因此，会随机抽取样本。为了最大限度地扩大感兴趣的人群，在符合资格标准的患者队列中(总共985名患者)，所有存活2年或更长时间的患者(总计132名患者，记为≥24组)都被纳入进行详细分析，大约30%的存活不足2年的患者被随机挑选(在剩余的853名患者中)，总共253名患者(记为&lt;24组)。所有患者都有至少2年的随访。


这个数据集里包含了384个观察对象，18个变量，其中“surv_cens”是“随访结局”，“survival”是“生存时间”。我们选择其中8个作为“协变量”：ECOG + liver_only + Alb + Hb + Age + Differentiation + Gt_1_m1site + lymph_only。


### 利用svydesign函数进行分层
对于调查数据，在检验调查加权Cox模型并建立诺模图之前，必须首先使用调查设计的svydesign函数指定调查的抽样设计。
```
dstr2 <- svydesign(id = ~1, strata = ~group, prob = ~inv_weight,
                   fpc = ~ssize, data = noNA)
```
- id = ~1, 表示不存在群集
- strata = ~group, 指定不同的分层
- prob = ~inv_weight, 提供抽样概率。
- fpc = ~ssize，指定在每个分层中的总样本量


### 建立加权COX回归方程
这类似于设置常规的Cox模型，不同之处在于现在调查设计是通过`design = dstr2`选项来考虑的。
```
svy.cox.fit <- svycoxph(Surv(survival, surv_cens) ~ ECOG + liver_only + Alb + Hb + Age + Differentiation + Gt_1_m1site + lymph_only, x = TRUE, design = dstr2)
```

下面列出了估计的模型参数及其显著性水平。
```
                        coef exp(coef)  se(coef) robust se      z        p
ECOG                0.960653  2.613404  0.133775  0.087134 11.025  < 2e-16
liver_only          0.327080  1.386913  0.195464  0.111001  2.947  0.00321
Alb                -0.318351  0.727347  0.166377  0.167557 -1.900  0.05744
Hb                 -0.195250  0.822629  0.056105  0.043763 -4.462 8.14e-06
Age                 0.007059  1.007084  0.004464  0.003389  2.083  0.03724
Differentiation2-3 -0.458017  0.632537  0.143651  0.109397 -4.187 2.83e-05
Gt_1_m1site         0.055396  1.056960  0.152256  0.101114  0.548  0.58379
lymph_only         -0.252121  0.777151  0.189292  0.144305 -1.747  0.08061
```

### 从模型中得到相应的线性预测值
```
pred_lp_cox <- predict(svy.cox.fit)
```

我们还将每个患者的预计生存时间存储为:
```
pred_survey_cox <- predict(svy.cox.fit, type = "curve", newdata = noNA)
```

### 使用ols函数近似模型
由于调查包中的svycoxph函数与rms包中的诺模图函数之间没有链接，因此我们必须使用rms包中的函数ols创建此链接。这通过设置普通最小二乘来回归用于检验调查加权Cox模型的相同预测值上的线性预测值来近似模型。请注意，包含参数sigma=1是为了防止因均方误差为零而导致的数值问题：
```
f <- ols(pred_lp_cox ~ ECOG + liver_only + Alb + Hb + Age +
Differentiation + Gt_1_m1site + lymph_only, sigma = 1,
x = TRUE, y = TRUE, data = noNA)
```


### 构建列线图
#### 方法一
在本例中选择为2年的所需时间点，在为建立我们的诺模图做准备的过程中:
```
dd <- datadist(noNA)
options(datadist = "dd")
ss3 <- c(0.05, 0.2, 0.4, 0.6, 0.7, 0.8, 0.9, 0.95, 0.99)
```

以及在构建诺模图时要使用的基线生存和生存函数:
```
twoyears <- with(pred_survey_cox[[1]], time[which(time > 24)[1] - 1])
baseline <- exp(log(pred_survey_cox[[1]]$surv[names(twoyears)]) /
exp(svy.cox.fit$linear.predictors[1]))
surv2y <- function(x) baseline[[1]]^exp(x)
```

请注意，在Surv2y的定义中，索引1可以由1到length(Pred_Survey_Cox)之间的任何数字替换，因为surv2y对于任何患者都是相同的。
最后，两年存活率的诺模图被构建为:
```
nom <- nomogram(f, fun = surv2y, funlabel = "Prob of 2 year OS",
fun.at = ss3, lp = TRUE, vnames = "labels")
plot(nom)
```

#### 方法二
或者，可以使用SvyNom包中的svycox.norgram构建两年存活率的诺模图：
```
mynom <- svycox.nomogram(.design = dstr2, .model =
Surv(survival, surv_cens) ~ ECOG + liver_only + Alb + Hb + Age +
Differentiation + Gt_1_m1site + lymph_only, .data = noNA, pred.at = 24,
fun.lab = "Prob of 2 Yr OS")
plot(mynom$nomog)
```


## 列线图的验证
对于每个Bootstrap样本(由原始数据的抽样和替换构成)，我们按照上面概述的步骤测试调查加权Cox模型。我们基于基于Bootstrap数据的模型的归一化线性预测因子来计算Harrell‘s c指数，并通过减去观测数据的c指数得到偏差。

原始数据的Harrell‘s c指数是在对建立诺模图的调查加权Cox模型的线性预测因子进行归一化后得到的：
```
lp_normalized <- svy.cox.fit$x %*% as.matrix(svy.cox.fit$coefficients) -
mean(svy.cox.fit$x %*% as.matrix(svy.cox.fit$coefficients))

cindex.orig <- with(noNA, 1 - rcorr.cens(lp_normalized,
Surv(survival, surv_cens))[[1]])

cindex.orig
[1] 0.7575879
```

我们使用200个引导数据集执行引导验证，这些数据集是通过对原始数据进行采样和替换而构建的，但是以这样的方式保持长期存活者相对于存活少于2年的患者数量的比率相同(分层引导)。更准确地说，在长期存活者中，我们用置换抽样的长期幸存者与观察数据中的数目(132)一样多，同样，我们用置换抽样了253名存活不到2年的患者中的253名患者；这两组人一起构成了自举样本。然后我们重复这个过程200次。可以使用执行以下步骤的svycox.valify来完成：
```
bootit <- 200
for (i in 1:bootit) {
case <- noNA[noNA$group == "long", ]
control <- noNA[noNA$group == "<24", ]
bootindex.case <- sample(1:nrow(case), replace = TRUE)
boot.case.data <- case[bootindex.case, ]
bootindex.control <- sample(1:nrow(control), replace = TRUE)
boot.control.data <- control[bootindex.control, ]
boot.data <- rbind(boot.case.data, boot.control.data)
}
```

对于每个Bootstrap数据集，详细说明了分层独立抽样设计:
```
dstr.boot <- svydesign(id = ~1, strata = ~group, prob = ~inv_weight,
fpc = ~ssize, data = boot.data)
```

将调查加权Cox模型应用于Bootstrap数据:
```
boot.fit <- svycoxph(Surv(survival, surv_cens) ~ ECOG + liver_only +
Alb + Hb + Age + Differentiation + Gt_1_m1site + lymph_only,
x = TRUE, design = dstr.boot)
```

在对来自调查加权Cox模型的线性预测因子进行归一化之后，对引导数据(lp.boot)进行了测试，并对原始数据(lp.test)进行了评估:
```
lp.boot <- boot.fit$x %*% as.matrix(boot.fit$coefficients) -
mean(boot.fit$x %*% as.matrix(boot.fit$coefficients))

lp.test <- svy.cox.fit$ x%*% as.matrix(boot.fit$coefficients) -
mean(svy.cox.fit$x %*% as.matrix(boot.fit$coefficients))
```

对于Bootstrap样本和原始数据，都会计算Harrell的c指数:
```
cindex.train <- 1 - rcorr.cens(lp.boot,
Surv(boot.data$survival, boot.data$surv_cens))[[1]]

cindex.test <- 1 - rcorr.cens(lp.test,
Surv(noNA$survival, noNA$surv_cens))[[1]]
```

这两个指数之间的区别是乐观的。在重复这个过程200次之后，最终的乐观估计是由相应的200个不同结果的平均值来估计的。
```
bias <- rep(1, bootit)
bias[i] <- abs(cindex.train - cindex.test)
```

然后通过从原始数据的一致性概率中减去乐观估计来获得一致性概率的无偏度量。
```
print(mean(bias))
[1] 0.01045796

print(paste("Adjusted C-index=", round(cindex.orig - mean(bias),
digits = 5), sep = " "))

[1] "Adjusted C-index= 0.74713"
```

或者，可以使用 SvyNom 包中的 , 函数 svycox.validate 进行验证:
```
cases <- which(noNA$group == "long")
controls <- which(noNA$group == "<24")
boot.index <- matrix(NA, nrow(noNA), bootit)
for (i in 1:bootit)
boot.index[, i] <- c(sample(cases, replace = TRUE),
sample(controls, replace = TRUE))
myval <- svycox.validate(boot.index, mynom, noNA)
```

## 列线图的校准
一旦两年的预测生存概率被排序，它们可以被分组为特定数量的组(通常为4或5组)，然后计算每个组的两年预测生存概率的中位数。校准曲线图将这些中位数估计值与两年调查加权Kaplan-Meier估计值(使用调查包中的svykm函数获得)进行对比。接近对角线的点表示良好的校准。

svycox.calibrate函数是实现诺模图校准的主要工具。一旦调用，它将通过以下步骤生成校准图。首先，数据被分成5组(注意组的数量是由用户选择的)。
```
.loc <- max(which(pred_survey_cox[[1]]$time <= 24))
pred_2years <- sapply(pred_survey_cox, function(x) x$surv[.loc])
grouped_pred_2years <- cut(pred_2years, quantile(pred_2years,
seq(0, 1, 0.2)), include.lowest = TRUE, labels = 1:5)
```

然后计算5组中每一组的2年预测生存概率的中位数:
```
median_pred_2years_1 <- median(pred_2years[grouped_pred_2years == 1])
median_pred_2years_2 <- median(pred_2years[grouped_pred_2years == 2])
median_pred_2years_3 <- median(pred_2years[grouped_pred_2years == 3])
median_pred_2years_4 <- median(pred_2years[grouped_pred_2years == 4])
median_pred_2years_5 <- median(pred_2years[grouped_pred_2years == 5])
median_pred_2years <- cbind(median_pred_2years_1, median_pred_2years_2,
median_pred_2years_3, median_pred_2years_4, median_pred_2years_5)
```

**下面提供了计算中值的简化代码:**
```
median_pred_2years <- as.vector(by(pred_2years, grouped_pred_2years,
median))
```

接下来，调查加权的Kaplan-Meier两年生存概率被估计在5组中的每一组中。
```
km_1 <- svykm(Surv(survival, surv_cens) ~ 1,
design = subset(dstr2, grouped_pred_2years == 1), se = TRUE)
km_2 <- svykm(Surv(survival, surv_cens) ~ 1,
design = subset(dstr2, grouped_pred_2years == 2), se = TRUE)
km_3 <- svykm(Surv(survival, surv_cens) ~ 1,
design = subset(dstr2, grouped_pred_2years == 3), se = TRUE)
km_4 <- svykm(Surv(survival, surv_cens) ~ 1,
design = subset(dstr2, grouped_pred_2years == 4), se = TRUE)
km_5 <- svykm(Surv(survival, surv_cens) ~ 1,
design = subset(dstr2, grouped_pred_2years == 5), se = TRUE)
km1_2years <- km_1[[2]][which(km_1[[1]] > 24)[1] - 1]
km2_2years <- km_2[[2]][which(km_2[[1]] > 24)[1] - 1]
km3_2years <- km_3[[2]][which(km_3[[1]] > 24)[1] - 1]
km4_2years <- km_4[[2]][which(km_4[[1]] > 24)[1] - 1]
km5_2years <- km_5[[2]][which(km_5[[1]] > 24)[1] - 1]
km_observed_2years <- cbind(km1_2years, km2_2years, km3_2years,
km4_2years, km5_2years)
```

连同它们在对数刻度上的对应方差:
```
varlog1_2years <- km_1[[3]][which(km_1[[1]] > 24)[1] - 1]
varlog2_2years <- km_2[[3]][which(km_2[[1]] > 24)[1] - 1]
varlog3_2years <- km_3[[3]][which(km_3[[1]] > 24)[1] - 1]
varlog4_2years <- km_4[[3]][which(km_4[[1]] > 24)[1] - 1]
varlog5_2years <- km_5[[3]][which(km_5[[1]] > 24)[1] - 1]
```

然后，在假设生存函数的对数为正态近似的情况下，估计95%概率区间的下界和上界：
```
ll1_2years <- exp(log(km1_2years) - 1.96 * sqrt(varlog1_2years))
ll2_2years <- exp(log(km2_2years) - 1.96 * sqrt(varlog2_2years))
ll3_2years <- exp(log(km3_2years) - 1.96 * sqrt(varlog3_2years))
ll4_2years <- exp(log(km4_2years) - 1.96 * sqrt(varlog4_2years))
ll5_2years <- exp(log(km5_2years) - 1.96 * sqrt(varlog5_2years))
ul1_2years <- exp(log(km1_2years) + 1.96 * sqrt(varlog1_2years))
ul2_2years <- exp(log(km2_2years) + 1.96 * sqrt(varlog2_2years))
ul3_2years <- exp(log(km3_2years) + 1.96 * sqrt(varlog3_2years))
ul4_2years <- exp(log(km4_2years) + 1.96 * sqrt(varlog4_2years))
ul5_2years <- exp(log(km5_2years) + 1.96 * sqrt(varlog5_2years))
```

最后，通过绘制模型估计的两年预测生存概率与调查加权Kaplan-Meier两年生存概率的中位数，得到校准图:
```
plot(median_pred_2years, km_observed_2years, xlim = 0:1, ylim = 0:1)
lines(x = rep(median_pred_2years_1, 2), y = c(ll1_2years, ul1_2years))
lines(x = rep(median_pred_2years_2, 2), y = c(ll2_2years, ul2_2years))
lines(x = rep(median_pred_2years_3, 2), y = c(ll3_2years, ul3_2years))
lines(x = rep(median_pred_2years_4, 2), y = c(ll4_2years, ul4_2years))
lines(x = rep(median_pred_2years_5, 2), y = c(ll5_2years, ul5_2years))
abline(0, 1, lty = 2)
lines(median_pred_2years, km_observed_2years)
```

下图所示，
![20210717144833](https://gitee.com/alingyisheng/tupian/raw/master/img/20210717144833.png)

也可以使用SvyNom包中的函数svycox.calbrate获得：
```
svycox.calibrate(mynom)
```
