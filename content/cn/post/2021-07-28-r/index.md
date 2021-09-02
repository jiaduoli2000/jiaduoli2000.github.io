---
title: Blogdown+Hugo+Netlify搭建个人博客
author: 阿狸的Blog
date: '2021-07-28'
slug: r
categories:
  - r
tags:
  - writing
---

大家好，我是阿狸，这里是阿狸笔记。作为一个医学生，每每在网络上浏览到各路程序猿大神们自己搭建的个人博客，心中都无比羡慕。最近看到[谢益辉](https://yihui.org/)、[王诗翔](https://shixiangwang.github.io/home/)、[庄闪闪](https://zhuanlan.zhihu.com/p/391528071)等人介绍的用R语言来搭建个人博客，心中羡慕之情如滔滔江水无法阻挡。于是自己动手，在奋斗了2天1夜之后，终于把我的个人博客[阿狸的Blog](https://condescending-banach-c90b09.netlify.app/)的雏形搭建出来了，途中踩坑数个，在这里做个记录。也许有人要问，搭建个博客要这么久么。这里不必担心，其实这个时间是对我这个新手来说的，看了此介绍，没准你10分钟就搞定啦。有图有真相：

![20210726171009](https://gitee.com/alingyisheng/tupian/raw/master/img/20210726171009.png)

这里克隆了[王诗翔](https://shixiangwang.github.io/home/)的相关设置，部分内容还没来得及更改，部分内容不会更改。特别是这个头像下的“_上士闻道  勤而行之_”这两行字，到现在都没琢磨出来要如何删去。如果哪位师傅能指点一下，我将不胜感激。


## 1. R Blogdown 包介绍
这个R包的作者就是前面提到的[谢益辉](https://yihui.org/)，在他的博客里可以看到他的写作原则：反对被抄袭和不用脑子的被复制被粘贴。无奈我还是在这里复制粘贴了，希望大佬能够见谅。下面就是作者谢益辉自述的建立Blogdown包的过程：

   <u>_2004 年我开始在博客中国（后来改名为 bokee）写博客，后来改到 blog.com.cn，再后来到 MSN Space 写英文，再后来自己用 Bo-blog 建站，两年后再次换系统为如今流行的 WordPress，三年后我到了码农的乐土，Jekyll，一个以纯文本文件形式写博客的系统，五年后我越来越不能忍受 Jekyll 之慢（本地预览动不动要花 30 秒），于是投奔了以速度见长的 Hugo，并写了一个 R 包装 [blogdown](https://github.com/rstudio/blogdown)。</u>_

原来大佬们做事都是这么轻描淡写，看来**解决的问题能力决定了我们遇到问题时的情绪**呀。想让心情好点，赶紧翻书学习吧。

多说一句，我们直接用[Hugo](https://gohugo.io/)+[Netlify](https://www.netlify.com/)就可以建站的，我以前也鼓捣过，比如另一个[阿狸的Blog](https://www.aliyisheng.blog/)。之所以用[blogdown](https://github.com/rstudio/blogdown)。一个是个人崇拜（谢益辉用的这个主题好像有点让人爱不释手）。另外，据庄闪闪介绍说：<u>_Rmarkdown 与 hugo 结合后，可以将Rmarkdown 的文章自动上传上去。而 Rmarkdown 的优势在于，代码结果可以轻松呈现_</u>。当然，目前我还不会用Rmarkdown，所以这个优势还无法体会。

## 2. 准备工作
### 1. 注册github
因为博客托管在[github](https://github.com)上，所以你要注册一个github账号，这里可以参考[一步一步教你注册GitHub账号及简单使用](https://cloud.tencent.com/developer/article/1487508)。

![20210726173425](https://gitee.com/alingyisheng/tupian/raw/master/img/20210726173425.png)

### 2. 注册netlify
有了github账号之后，注册[Netlify](https://www.netlify.com/)就轻松多了，进官网直接点击篮框里的`Get started for free`。直接用github的账号授权登陆就可以了。

![20210726174228](https://gitee.com/alingyisheng/tupian/raw/master/img/20210726174228.png)

### 3. 安装 blogdown 包
打开Rstudio后，输入：
```text
install.packages("blogdown")
```


## 3. 建站过程
### 1. 使用Blogdown包
这里我们从Rsudio开始，前面我们已经安装了blogdown 包。步骤参考庄闪闪的[使用Blogdown构建个人博客](https://zhuanlan.zhihu.com/p/391528071)，内容十分详细，他把整个过程分为了三个步骤，当我们按流程走完第一个1/3之后，我将遇到第一个坑（**注意**：是我遇到的，你可能不会遇到）。

![20210726175631](https://gitee.com/alingyisheng/tupian/raw/master/img/20210726175631.png)

### 2. 将项目与 github 相连
当我按照教程继续往下走的时候，发现我的**GitHub 桌面版**，好像不太好使，在将创建好的仓库publish上去的时候，无论如何也publish不上去。能够建立仓库，但仓库里没有内容。咋办哩？所以，只能想别的办法。于是，我打开：[Visual Studio Code](https://code.visualstudio.com/)，用github账号登陆。然后把刚才用“**GitHub 桌面版**”建立了的但没有文件的仓库克隆到本地，然后把文件通过vscode上传到gihub，最后终于成功了，这个上传过程相当的慢，反复了几次，看来我的网速不太行。如果你有提高速度的方法，请留言告诉我。

![20210726185516](https://gitee.com/alingyisheng/tupian/raw/master/img/20210726185516.png)

到这里，第二部通过。

![20210726190449](https://gitee.com/alingyisheng/tupian/raw/master/img/20210726190449.png)

### 3.使用 Netify 部署网站
按照庄闪闪的教程走到最后一步，本来以为会马上结束，无奈我用的是以王诗翔的网站设置为模板，所以这里要注意的这里：

![20210726190804](https://gitee.com/alingyisheng/tupian/raw/master/img/20210726190804.png)

这里`publish directory`在王诗翔的设置中用的是`docs`, 所以要把`public`换成`docs`。好吧，我的2天时间都是在这个坑里趴着的，再次感叹自己，没文化真可怕呀。

## 4. 感言
1. 通过这阵折腾，亲自实践了，非程序猿通过R语言Blogdown 包是可以成功建立个人博客的，例如我克隆的这个[阿狸的Blog](https://condescending-banach-c90b09.netlify.app/)（还需修改）。如果你打算继续学习Rmarkdown语法的话，可以去尝试一下。
2. 向github上传文件是真的慢，总的说就是不靠谱，有时尝试几篇都不行，甚至网页都打不开，这严重限制了工作效率。不知道有没有好的办法解决，有待学习。
3. 写博客并非短跑，需要耐力坚持，一旦建了，就需要时常打理。如果建了后收藏起来吃灰，还是别折腾了。

好吧，我是阿狸，今天的内容就是这些。如果你坚持看完并有所收获的话，顺手点个“赞”吧。再见。
