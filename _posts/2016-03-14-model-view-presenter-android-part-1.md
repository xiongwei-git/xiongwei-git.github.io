---
layout: post
title: 【译】Android中的MVP设计模式（一）
date:       2016-03-14
author:     "Ted"
tags:
    - 翻译
    - 工具
---

## 【译】Android中的MVP设计模式（一）
> 原文地址：[MODEL VIEW PRESENTER (MVP) IN ANDROID, PART 1](http://www.tinmegali.com/en/model-view-presenter-android-part-1/) 

![mvp][1]
**架构模式**是计算机科学中的一个基本组成部分。使用设计模式能够保持项目的简洁性、扩展性和可测试性。**MVP**设计模式是一个已经发展了多年时间并且被认为是设计标准的解决方案。**MVP**还在不断的发展，并且Android SDK中逐步的取代了**MVC**设计模式。

本系列文章的第一部分，我们重点讨论**MVC**(Model View Controller)和**MVP** (Model View Presenter)的不同之处，以及为什么**MVC**正在被淘汰、**MVP**在Android SDK中的运用和它的一些优秀特性。

*附上另外两篇文章的地址，后期再翻译。*  
- [Model View Presenter (MVP) in Android, part 2](http://www.tinmegali.com/en/model-view-presenter-mvp-in-android-part-2/)  
- [Model View Presenter (MVP) in Android, part 3](http://wp.me/p7gH7l-34)

## The Android SDK
当我们简要分析Android SDK之后，尤其是`layout`和`activity`之间的关系，能很强烈的感觉到最适合Android的设计模式是**MVC**。但是随着项目复杂性的增加，**MVC**对于一些功能点的分离支持的不是特别好，尤其是单元测试。

然而，Android SDK正在逐渐允许我们使用其他类型的架构模式，甚至没有任何设计模式，即所谓的反模式。尽管**MVC**是一个可靠的众所周知的解决方案，但是它正在被后继者**MVP**所击败，后者能够提供一些前者没有的优势，比如更明确的功能点分离。

## 在项目中我该用MVC还是MVP？
这个问题没有绝对正确的答案。有些人认为**MVC**是最佳选择，而有些人会选择**MVP**。还有一些人甚至会选择其他的方案，比如**MVVM**。这些选择中，每一个都有优点和缺点。也就是说，要回答这个问题的唯一办法就是要了解每种解决方案的优劣，只有这样才能明智的做出最佳选择。

### MVC、MVP的定义说明
> **Model–view–controller (MVC)**主要是（但不限于）用于在计算机上实现用户界面的软件架构设计模式。它把一个既定的软件应用程序分为三个相互连接的部分，以便于把显示内容或者从用户获取信息的这两种内在的数据表现动作分离出来。  
[wikipedia](https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller)  
> **Model–view–presenter (MVP) **是MVC设计模式的推导，并主要用于构建用户界面。在MVP中Presenter承担了“中间人”的功能，并且所有的表示逻辑都交给了Presenter。  
[wikipedia](https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93presenter)

![MVC-vs-MVP][2]

### MVC和MVP的不同之处

**Model View Presenter**  

* View更多的从Model中分离出来。Presenter则是Model和View的中间传递者。  
* 更加容易创建单元测试。  
* 通常来说，View和Presenter是一一对应的关系，也有可能比较复杂的View需要多个Presenter。  

**Model View Controller**

* Controller基于行为，并且可以共享不同的View。  
* View可以直接和Model通信。  

## Android中的MVP设计模式
Android中功能点如何分离并没有很好的定义。用Activity举例，数据机制有着过于密切的关系。尽管，对于一个应用变的可扩展、可维护和可测试来说，更重要的是使重要的功能点深度分离。这或许就是我们采用MVP设计模式获取的最大优势。
![MVP][3]

## 如何更好的采用MVP模式
这其实是一个很模糊的话题。对于MVP，有很多有趣的方法和不同的解决方案，使其来适应Android。该模式的实现方式是，根据Presenter承担的角色变化而变化。唯一不能改变的是MVP的核心：

> **Presenter**  
Presenter的责任是扮演View和Model的中间人。它从Model中检索数据并且将其格式化返回给View。不同于MVC的是，它也能决定当你跟View互动时发生什么。  
> **View**    
View通常由Activity或者Fragment实现，持有一个对Presenter的引用。View唯一要做的事情就是每一个页面操作时调用Presenter的方法。  
> **Model**  
在一个有着良好的分层架构应用程序中，Model只会通向数据领域层或者业务逻辑。把它当做我们用来呈现到视图上的数据的提供者。  

以上这些优秀的定义摘自[Antonio Leiva’s article.](http://antonioleiva.com/mvp-android/)

在本系列的下一篇文章中，我们将在Android中实现MVP设计模式。我们将采用保守的方式，使用规范的代码，没有Android SDK以外的任何库。这种方法将有助于了解MVP的各层间不同的关系。

如果你想查看相关代码，[在这里](https://github.com/tinmegali/simple-mvp/tree/master/AndroidMVP/mvp/src/main/java/com/tinmegali/mvp/mvp)，这个版本是参考了[Dr. Douglas C. Schmidt](https://en.wikipedia.org/wiki/Douglas_C._Schmidt)的代码。代码拿去干啥都行，不用问我。
再见！

> 参考：  
* http://antonioleiva.com/mvp-android/  
* http://hannesdorfmann.com/android/mosby  
* http://www.codeproject.com/Articles/288928/Differences-between-MVC-and-MVP-for-Beginners  
* https://github.com/konmik/konmik.github.io/wiki/Introduction-to-Model-View-Presenter-on-Android  
* https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93presenter

[1]:http://7vzsca.com1.z0.glb.clouddn.com/2016-03-14-MVP.png_img800w
[2]:http://7vzsca.com1.z0.glb.clouddn.com/2016-03-14_MVC-vs-MVP.png_img800w
[3]:http://7vzsca.com1.z0.glb.clouddn.com/2016-03-14_MVP_2-en.png_img800w