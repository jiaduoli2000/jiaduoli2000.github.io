---
title: obsidian配合anki制作儿童学习卡片
author: 阿狸的Blog
date: '2021-09-06'
slug: obsidian and anki for flashcard
categories:
  - 效率工具
tags:
  - anki
---

我的启蒙教育，大概是从卡片开始的。我是个80后，大约4、5岁的时候，爷爷开始教我识字，他用毛笔把一些简单的字写在硬纸片上，然后教我，考我，这就是爷爷对我的教育方式。爷爷年轻时做过村里的中学老师，是村里不多的 “读书人"。他很严厉，除了识字卡片。爷爷的抽屉里还有一把戒尺，虽然不常用，但我还是品尝过被敲打的滋味，至今记忆尤新。四五岁的小孩毕竟懵懂无知，谁愿意去背枯燥无味的卡片。爷爷的眼神不好，所以我常常趁着爷爷不注意，抓起几张卡片藏在一边。这个儿时的”污点“，至今还常常被长辈们提起，成为了我儿时的趣事儿。

![当年爷爷抄写的中药方](https://gitee.com/alingyisheng/tupian/raw/master/img/IMG_20210906_152241_BURST001_COVER%5B1%5D.jpg)

爷爷过世已经近30年了，但他的身影却永远停留在了我的记忆里。有了孩子之后，我却没有把爷爷的卡片传承下去。妈妈常常说：“别整天鼓捣你的电脑，抽点时间去培养你的孩子，比啥都强！”。这是妈妈的原话。没错，我把教育丢给学校，作为父母确实不太负责。其实，初为父母会很困惑，如何教孩子，教什么，从什么时候开始教…… 一大堆的问题。在这个教育机构以及电子产品乱飞的时代，怎样教孩子变得更加难以抉择。

我想我还是要把爷爷的”卡片教育法“传承下去，无论教育的效果如何。至少多年之后，这段经历能留在孩子们的记忆里。如今键盘代替了毛笔，平板手机成了新的知识载体。即使”卡片精神“不变，”卡片形式“也许要与时俱进了。于是，就有了今天的工作流：obsidian配合anki制作儿童学习卡片。

今天的内容，我只是提供一制作卡片的方法。关于卡片，无论是制作方法，还是制作内容，都是仁者见仁、智者见智。希望你有更好的方法或者内容分享给我。我也很想了解一些关于儿童教育的知识。当然，卡片的用法很多，可以用来背单词、刷题，如果这种方法适合你的话。

## 安装
> 安装Obsidian（黑曜石），[Obsidian下载: https://obsidian.md/](https://obsidian.md/)，有人说obsidian是完美的笔记管理软件，虽然有些过誉，但我已成为iobsidian的忠实粉丝，它正在帮我打理我的电脑和文件。我发现，无论在知乎还是B站，都有一大群爱好者关注着obsidian的变化，几乎每天都有新的插件诞生。开源，本地化，双向链接，强大的插件系统让obsidian迅速成为了笔记软件中的璀璨新星。希望obsidian能像他说的那样，`for you, forever`。

![20210906120039](https://gitee.com/alingyisheng/tupian/raw/master/img/20210906120039.png)

> 在obsidian中安装插件：`Flashcards plugin`，我会把插件链接放在下方。安装插件的方法，就是下载好之后，解压文件，形成一个文件夹，然后放在`.obsidian`的`plugins`的文件夹中，如果没有`plugins`这个文件夹，那就自己建一个。安装完成后记得在obsidian中的`第三方插件中`启用。

![20210906123916](https://gitee.com/alingyisheng/tupian/raw/master/img/20210906123916.png)

> 安装Anki（暗记），[Anki下载：https://apps.ankiweb.net/](https://apps.ankiweb.net/)。安装过程同常规软件。安装完成后要注册账号才可以在电脑和手机之间同步，这样也可以防止制作的卡片丢失。

![20210906123717](https://gitee.com/alingyisheng/tupian/raw/master/img/20210906123717.png)

> 在Anki中安装插件`AnkiConnect`。启动Anki后，依此点击，`工具-插件-获取插件-代码`，输入：`2055492159`，点击ok。

![20210906125101](https://gitee.com/alingyisheng/tupian/raw/master/img/20210906125101.png)

配置插件`AnkiConnect`，选中`AnkiConnect-配置`，把下面的代码粘贴到绿框中，替换原有的代码，点击`ok`。**重新启动**。

```
{
    "apiKey": null,
    "apiLogPath": null,
    "webBindAddress": "127.0.0.1",
    "webBindPort": 8765,
    "webCorsOrigin": "http://localhost",
    "webCorsOriginList": [
        "http://localhost",
        "app://obsidian.md"
    ]
}
```

![20210906125435](https://gitee.com/alingyisheng/tupian/raw/master/img/20210906125435.png)

## 使用
### 制作卡片
打开obsidian，打开anki（制卡期间不要关闭），在obsidian中新建一个`markdown`文件，这里我命名为`test-儿童卡片`，我在笔记里先插入一张图片`把闹钟调到六点`（卡片正面），然后输入`#card`，然后输入`set the alarm clock for six`（卡片背面）-制作中遗漏了字幕`r`。然后点击obsidian里的`flashcard`插件的图标，会弹出一个创建开片成功的提示。

![20210906134320](https://gitee.com/alingyisheng/tupian/raw/master/img/20210906134320.png)

### 查看卡片
我们打开anki来看一下制作好的卡片，点击`未学习：1`，这是我们刚刚做好的那张卡片，`Default`是我们默认的牌组，牌组相当于一个分类的卡片盒，我们可以起一个好听的名字。然后点击：`现在学习`。

![20210906135256](https://gitee.com/alingyisheng/tupian/raw/master/img/20210906135256.png)

小学生，测试开始：（请用英语说出）

![20210906135820](https://gitee.com/alingyisheng/tupian/raw/master/img/20210906135820.png)

看看你的回答对么？点击`显示答案`。并按照你的回答结果，分别选择`忘记-困难-良好-简单`，anki会根据你的选择按时间`1分-6分-10分-4天`来再次进行测试。

![20210906135926](https://gitee.com/alingyisheng/tupian/raw/master/img/20210906135926.png)

### 同步手机或平板

当我们制作了多个卡片之后，我们就可以应用了。如果觉得电脑不方便的话，可以通过anki账号登陆到手机或平板使用。这里我是在华为的应用商店里搜索“`anki 记忆卡`”。然后按照手机app，登陆账号，同步刷新就好。这里注意不要频繁刷新，会有卡顿，建议间隔10分钟以上。

![20210906150655](https://gitee.com/alingyisheng/tupian/raw/master/img/20210906150655.png)
如果手机显示下图中的`同步错误：`

![20210906150132](https://gitee.com/alingyisheng/tupian/raw/master/img/20210906150132.png)

按下图选中进行设置即可解决：选中`旧时区处理`

![20210906145417](https://gitee.com/alingyisheng/tupian/raw/master/img/20210906145417.png)


今天的内容就是这些了，关于卡片的内容，我还不能确定要给孩子灌输哪些知识。即使这样，让他们体验一下这种卡片记忆法也是好的。如果他们感兴趣，我就多做一些卡片，如果不太感冒的话，我再看看有没有别的办法。我并不希望给他们灌输知识，我希望他们对世界充满好奇，并勇敢的探索未知世界，有求知欲，又有自己的学习方法。

好吧，今天的内容就是这些。这里是阿狸的Blog，再见。







附件：
**Flashcards plugin：**
链接：https://pan.baidu.com/s/11s50lkyAHDUtIQuPTyMhrw 
提取码：z1c6
