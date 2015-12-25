---
layout: post
title: Material Design风格之极简便签
date:       2015-02-26
author:     "Ted"
tags:
    - App
    - 开源
    - 烂笔头
---


年前新做的项目里想使用一下Google最新的Material Design风格设计，趁着年假回家前几天，大家都打酱油的时间，我抽时间看了一下Google的官方文档，借助一些大神的开源库，花了两个小时时间倒腾出来一个小app，起了个名字，叫[烂笔头],英文名叫`EasyNote`。

之所以开发这个app的原因是因为之前看过一个国外的类似的app，极简风格，应用极小，只能支持一条便签，当然方便之处也正是在于这里，生活中我们很多时候都想随手记下来一个东西，比如朋友给了你一个手机号码，如果打开联系人存储，可能会比较慢，要输入的选项比较多，甚至会让你选择同步到哪个账号里，如果对手机操作不熟悉的话，甚至手忙脚乱，最后耽误时间。

如果有了烂笔头这个app，只要你添加小部件到桌面上，随时点开，随时输入内容，不用费心的去找保存按钮在哪里，只要输入进去的内容，应用自动保存。等到晚上到了家，再认真整理烂笔头记下的内容，没有人催促你，慢慢保存吧。

文章底部我贴了几张app的截图，显示一下所谓的极简风格是多么的简单

在这个app里面，我使用了github上两个大神提供的Material Design控件库，以便在低版本上面支持Material Design风格。

* [MaterialDesignLibrary] 一个提供了不少Material Design风格空间的库，唯一不爽的是对话框不太好用，所以我用了下面这个库。
* [material-dialogs] 专门提供Material Design风格对话框的库。


顺便说一句，用了Gradle编译项目之后，使用开源库是越发的简单了，希望自己也能尽快贡献出来优质的代码给世界上的开发者使用，想想那种感觉都是很美好的事情。

这个app的功能很简单，实现起来也就两个钟头的事情，主要集中在以下两个方面：

* 本地数据保存以及显示
* widget创建以及数据更新

跑到公司找UI给了个icon切图，就打包上架了，顺便喷一下豌豆荚的审核，真慢。

后来，我自己又加了几个小功能：

* 皮肤切换
* 参看开发者信息
* 清空内容时后悔的选项

这几天我又想出了几个功能点，准备在后期加上：

* 接收其他app分享功能
* 监听剪切板功能
* 摇一摇快速添加功能
* ……

哈哈，一个只有一个类的app，我自己在这里自娱自乐，权当练手好了，毕竟初衷就是练习Material Design开发的。

目前的代码量很少，大多是采用别人的开源库，这里先不开源代码了，没有参考价值，等后期实现了所有我想要的功能之后，我再把代码开源共享。

> **3月5日更新:**  
> 新增“摇一摇”快速记录剪切板内容功能  
> 新增“接收其他应用分享”功能，在浏览器中即可分享内容到烂笔头  
> 新增“查看教程”功能，通过教程学习如何快速记录内容到烂笔头  
> * 2.0版本之后，[烂笔头](http://www.wandoujia.com/apps/com.ted.jots.myjot)这个小项目就暂时停止了，着手开发下一个app，要看到时候有什么好的`Idea`了。


下面是烂笔头的运行截图，如果有人想实际使用一下的话，可以下载[烂笔头]。

![EasyNoteJpg1](http://7vzsca.com1.z0.glb.clouddn.com/tedcoderOneNote-1.jpg_img500w) ![EasyNoteJpg2](http://7vzsca.com1.z0.glb.clouddn.com/tedcoderOneNote-2.jpg_img500w)
![EasyNoteJpg3](http://7vzsca.com1.z0.glb.clouddn.com/tedcoderOneNote-3.jpg_img500w) ![EasyNoteJpg4](http://7vzsca.com1.z0.glb.clouddn.com/tedcoderOneNote-4.jpg_img500w)
![EasyNoteJpg5](http://7vzsca.com1.z0.glb.clouddn.com/tedcoderOneNote-5.jpg_img500w)

[烂笔头]: http://apk.hiapk.com/appinfo/com.ted.jots.myjot
[MaterialDesignLibrary]: https://github.com/navasmdc/MaterialDesignLibrary
[material-dialogs]: https://github.com/afollestad/material-dialogs




