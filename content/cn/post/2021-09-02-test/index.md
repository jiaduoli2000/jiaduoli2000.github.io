---
title: Bookdown制作图书+GiteePages展示
author: '阿狸的Blog'
date: '2021-09-02'
slug: [-]
categories: [r]
tags: [bookdown]
---

在读书时常常看到一些纸质书的前言介绍里会提供图书的`网页电子版本`，这个表达有一些拗口，暂且这样叫吧。比如说，这一本[《 用bookdown制作图书》](https://www.math.pku.edu.cn/teachers/lidf/docs/Rbook/html/_Rbook/bookdown.html)。

这些`网页电子版本`的图书还会定期更新。这让我不禁感叹，这些书籍的作者真是细心。这种方法好像是把一本书赋予了生命，书中的内容会随着时间不断的修正成长。网页电子书的更新很便捷，耗时很短。不像是纸质书，比如说外科学名著《黄家驷外科学》那样，更新一次要耗时几年。所以，我有了奇怪的想法，如果有一天我也写一本书的话（可能性极小），我一定写成`网页电子书`。

虽然写书的愿望实现还很遥远，但现实中学习一下这种`网页电子书`的制作过程还是可以的。R语言有一个叫Bookdown的包，能够让我们制作网页电子图书，类似于gitbook，差别是在R软件中进行实现。当我们写好后可以直接通过git推送到github或gitee仓库。前几日我逐步了解了一些GiteePages的相关知识。今天，我把二者结合起来，所以今天的主题是：用Bookdown制作图书+用GiteePages展示。好吧，话不多说，开干：


## 准备
这些软件是我已经安装好的，[ R软件](https://cran.r-project.org/)，[RStudio](https://www.rstudio.com/),[Git](https://git-scm.com/)，然后打开`RStudio`安装`R bookdown`包：

```text
# you can either use the CRAN version
install.packages('bookdown')

# or the development version on Github
remotes::install_github('rstudio/bookdown')
```

## 制作
在`RStudio`的菜单栏，点击`File`-`New Project`-`New Directory`，然后点击`book project using bookdown` ：

![20210901172152](https://gitee.com/alingyisheng/tupian2/raw/master/20210901172152.png)

设置文件名和路径，点击创建：

![20210901172625](https://gitee.com/alingyisheng/tupian2/raw/master/20210901172625.png)

创建好了之后，出现的页面：

![20210901172747](https://gitee.com/alingyisheng/tupian2/raw/master/20210901172747.png)

## 启动git

在面板中找到下图中的`Terminal`，

![20210901183004](https://gitee.com/alingyisheng/tupian2/raw/master/20210901183004.png)

然后在命令行输入：`git init`,

![20210901183434](https://gitee.com/alingyisheng/tupian2/raw/master/20210901183434.png)

然后在命令行输入：`git add .`, 这里注意在`" ."`前面有一个`空格`,

![20210901183655](https://gitee.com/alingyisheng/tupian2/raw/master/20210901183655.png)

然后在命令行输入：`git commit -m "initial bookdown template"`,

![20210901184219](https://gitee.com/alingyisheng/tupian2/raw/master/20210901184219.png)

然后在命令行输入：`git status `, 可以看到所有更改都已提交。

![20210901184436](https://gitee.com/alingyisheng/tupian2/raw/master/20210901184436.png)

## 调整模板设置

我们对bookdown包中自带的模板进行一些设置，这里我们要导出的格式是`html`，所以可以删除`pdf`等格式。

![20210901185101](https://gitee.com/alingyisheng/tupian2/raw/master/20210901185101.png)

在上图中找到`_output.yml`, 单击打开文件，删除**带有阴影**的部分，然后**保存**。

![20210901185323](https://gitee.com/alingyisheng/tupian2/raw/master/20210901185323.png)

同法打开文件：`_bookdown.yml`, 在其中指定输出文件夹，增加一行内容：`output_dir: "docs"`,  然后**保存**，一定记得保存。

![20210901190050](https://gitee.com/alingyisheng/tupian2/raw/master/20210901190050.png)

修改了这两个文件后，我们在`git`里查看一下，输入：`git status`, 这里显示：changes not staged  for commit，

![20210901190701](https://gitee.com/alingyisheng/tupian2/raw/master/20210901190701.png)

Terminal中输入：

```
git add _output.yml 
git add _bookdown.yml
git commit -m "chang bookdown output default"
```

![20210901191631](https://gitee.com/alingyisheng/tupian2/raw/master/20210901191631.png)

## 构建图书

下面我们来构建电子书，来到下面这个界面，找到`build`，然后点击`build book`，

![20210901192136](https://gitee.com/alingyisheng/tupian2/raw/master/20210901192136.png)

在弹出的对话框中我们可以看到，电子书已经构建好了，这个**网页电子书**左侧有大纲，还具有**搜索**和**下载**的功能。

![20210901192336](https://gitee.com/alingyisheng/tupian2/raw/master/20210901192336.png)

构建完成后，我们再查看文件目录，会看到生成了两个文件夹，再`_bookdown_files`文件夹中存储的是R中生成的图片文件，`docs`文件夹我们用来部署GiteePages。

![20210901192929](https:/gitee.com/alingyisheng/tupian2/raw/master/20210901192929.png)

我们可以通过设置来忽略`_bookdown_files`，具体方法是打开`.gitignore`文件后，添加:`_bookdown_files`, 然后输入:


```
git add .gitignore
git commit -m "ignore bookdown files created on build"
```

我这里就略过了。有点啰嗦了，谁让我是个小白呢，

## 主角上场

该看一看我们的主角`docs`文件夹了，里面主要是一些`.html`文件。这些是构建我们`网页电子书`的主要成分。

![20210901195054](https://gitee.com/alingyisheng/tupian2/raw/master/20210901195054.png)

把`docs`文件夹提交到**git**，输入以下命令：

```
git add docs/
git commit -m "bulid initial websit"
```

![20210901200048](https://gitee.com/alingyisheng/tupian2/raw/master/20210901200048.png)

![20210901200200](https://gitee.com/alingyisheng/tupian2/raw/master/20210901200200.png)

到此，在**R studio** 中的操作暂停一下。

## 建立仓库

我们来到[码云Gitee- Gitee.com](https://gitee.com)，新建一个仓库：

![20210901201149](https://gitee.com/alingyisheng/tupian2/raw/master/20210901201149.png)

复制仓库地址：

![20210901201341](https://gitee.com/alingyisheng/tupian2/raw/master/20210901201341.png)

## 回到R
在**R studio**中，输入代码：

```
git remote add origin https://gitee.com/alingyisheng/book-of-alee.git
git push -u origin master
```

![20210901202100](https://gitee.com/alingyisheng/tupian2/raw/master/20210901202100.png)

![20210901202226](https://gitee.com/alingyisheng/tupian2/raw/master/20210901202226.png)

这里报错了，为什么呢，研究了半天，最终是因为我设置了私钥，所以我用TortoiseGit来加入私钥，保存就可以了。关于TortoiseGit的简单用法，我之前介绍过[不懂代码，如何推送本地内容到码云（Gitee）？](https://zhuanlan.zhihu.com/p/405321511)

![20210901204650](https://gitee.com/alingyisheng/tupian2/raw/master/20210901204650.png)

好吧，再来一次，这回输入的代码做了个调整，注意这里把`origin`改成了`alee`，到现在这个小白才明白**`origin`**是啥意思了，原来是远端的名称，是可以更改的呀。

```
git remote add alee https://gitee.com/alingyisheng/book-of-alee.git
git push -u alee master
```

但是，仍然报错了。原因不清，若你知道的话，可以留言告诉我。

![20210901210205](https://gitee.com/alingyisheng/tupian2/raw/master/20210901210205.png)

有些问题如果找不到解决方法，就会不了了之，因而就不会有这篇博文，或者永远不会分享给你。好在，我在**TortoiseGit**软件中发现了这个选项功能，俩字”**强制**“，点击之后推送成功。哈哈，这种喜悦之情又消耗了多少我的多巴胺。自己挖坑，掉坑，填坑，然后跳出来笑，还洋洋得意，人生中的多少事似乎都是这样，难道人生就是挖坑，填坑的过程？等到挖不动、填不动了，就躺平，等待后人来挖来填！我 是不是就在享受这个挖坑过程？不得而知。

![20210901210111](https://gitee.com/alingyisheng/tupian2/raw/master/20210901210111.png)

## 展示结果
回到Gitee里新建的仓库，刷新一下网页，然后再查看，`docs`文件夹已经被上传到了仓库里。

![](../z%20-%20Attachments%20I%20附件/Pasted%20image%2020210901212300.png)

然后在**服务**里找到`Gitee Pages`，点击进入。

![20210901212347](https://gitee.com/alingyisheng/tupian2/raw/master/20210901212347.png)

安装下面图片中选择后**启动**，等待部署完成，完成后会给出一个网址。

![20210901212647](https://gitee.com/alingyisheng/tupian2/raw/master/20210901212647.png)

就是这个网址：[https://alingyisheng.gitee.io/book-of-alee](https://alingyisheng.gitee.io/book-of-alee)，点进去悄悄吧。

![20210901212921](https://gitee.com/alingyisheng/tupian2/raw/master/20210901212921.png)

在浏览器里悄悄吧，这里的内容是原模板的，我一点也没有修改。

![20210901213102](https://gitee.com/alingyisheng/tupian2/raw/master/20210901213102.png)

## 大结局

这次折腾结束了，我尽量记录的详细，为什么呢？一是因为随着年龄的增长，我的记忆力开始衰退了，脑袋记不住，只能记在本本上了，应了那句我妈从小就教导我的”好记性不如烂笔头“。二是我认识到，我早晚还会掉入同一个坑，这么多年，所有的事都是这样，虽然每个坑都不一样，但掉坑的原理从来没变。也许我也是个被别人编程好的机器人，走固定的路，掉同样的坑。
