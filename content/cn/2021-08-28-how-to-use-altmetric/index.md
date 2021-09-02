---
title: 使用rAltmetric查询文献的Altmetric指标
author: 阿狸的Blog
date: '2021-08-28'
slug: how to use Altmetric
categories: []
tags: []
---
# 如何使用rAltmetric查询文献的Altmetric指标?

Altmetric是最近几年新兴的评价论文影响力的指标，我们可以利用Altmetric评价系统了解论文的关注度和分享情况。其官网的地址是：https://www.altmetric.com/  ，这里要注意的是，Altmetric只看一篇文章或博文被在线讨论的次数，而不考虑这些关注是正面或负面的，甚至阅读次数和下载量也不考虑。Altmetric评分主要从三个方面进行考量，分别是被引用量、引用源和引用作者。

![20210828095706](https://gitee.com/alingyisheng/tupian2/raw/master/20210828095706.png)

本文介绍R软件包rAltmetric的基本用法，此软件包提供了一种从altmetric.com以编程方式检索具有适当标识符的任何出版物的altmetric.com数据的方法。该包使用起来非常简单，只有两个主要函数：一个(altmetrics())用于下载指标，另一个(altmetrics_data())用于将数据提取到data.frame中。

## 安装R包

```{r}
#install.packages('rAltmetric')
```

我们这里就用稳定版的。

## 快速使用
### 获取metrics指标
这里以 Acuna等人的文章为例，其DOI: 10.1038/465860a。
```{r}
library(rAltmetric) 
acuna <- altmetrics(doi = "10.1038/465860a")
acuna
```

### 获取数据
要获得表格形式的指标以便进一步处理，可以通过altmetric_data()运行altmetric类的任何对象，以获得可以轻松地以电子表格形式写入磁盘的数据。
```{r}
altmetric_data(acuna) 
```

### 数据保存：
```{r}
acuna_data <- altmetric_data(acuna) 
write.csv(acuna_data, file = 'acuna_altmetrics.csv')
```

## 收集多个 DOI 的指标
在实际应用时，人们可能希望获得多篇文献的指标。假设我们已经收取了多个DOI信息。
### 载入R包并读入DOI数据

```{r}
library(rAltmetric)
library(magrittr)
library(purrr)

ids <- list(c(
  "10.1038/nature09210",
  "10.1126/science.1187820",
  "10.1016/j.tree.2011.01.009",
  "10.1086/664183"
))

alm <- function(x)  altmetrics(doi = x) %>% altmetric_data()

results <- pmap_df(ids, alm)
head(results)
# This results in a data.frame with one row per identifier.
```
这会产生一个 data.frame，每个标识符一行，我可可以保存数据。
```{r}
write.csv(results, file = "metric_data.csv")
```

