---
layout: post
title: Android Studio 2.0预览版 v5 功能介绍
date:       2016-01-15
author:     "Ted"
tags:
    - 翻译
    - 工具

---

## Android Studio 2.0预览版 v5 功能介绍
原文地址：[https://sites.google.com/a/android.com/tools/recent/androidstudio20preview5available](https://sites.google.com/a/android.com/tools/recent/androidstudio20preview5available)

 我们刚刚通过金丝雀[^canary]版本渠道发布了Android Studio 2.0预览版 v5。相对于上个月的预览版 v4，这次构建做了很大一批的修复，主要包括：
   * **Instant Run（即时运行）**：在这块，我们做了巨大的修改。在之前提供的一些特性中（*原句：Among the user visible features*），我们提供了`冷修复`模式：即如果有一些无法通过热修复方式发布的不兼容的改动，会在编译之后通过重启app来发布这些改动。根据运行设备的API版本，我们使用了不同的办法来解决这个问题。
	-  在棉花糖版本的机器上，我们使用`APK分裂`方式，首先把代码库分割成不同的APK片，然后通过`adb install-multiple`方式安装它们。也就是说，在M设备上，不再像M之前的老设备那样使用类加载方式。
	-  在棒棒糖设备上，我们使用`multidex`来拆分代码到不同的dex块，然后推送到设备中。
	-  针对巧克力版本以及更低版本，我们创建了一个单独的dex块来存放被修改的类。
	-  针对提交了改动之后就需要重启app的`冷修复`，我们提供了`冻结修复`模式，即使app没有在运行，也能构建出来增量内容。这种情况下，我们通过adb把修改内容推送到设备上特定一个“收件箱”里。
	- 需要注意的是，Instant Run需要配合Gradle插件的最新版本，即**2.0-alpha5**（同样也在今天发布）- [该插件的发布日志](https://sites.google.com/a/android.com/tools/tech-docs/new-build-system)
	- 对`移除无用资源`（帮你找出项目中无用的资源并移除它们）功能做了一次重构。
	![Remove Unused Resources](https://raw.githubusercontent.com/xiongwei-git/xiongwei-git.github.io/master/img/blog/unused-resources.png)
	- 无用资源探测器已经被重写，支持对无用的资源进行“传递”标记（被引用的资源，但仅仅只能从无用的资源标记），支持在raw资源中进行探测，例如.html的图片引用。支持Gradle 的资源瘦身器经常使用的`tools:keep`和`tools:discard`属性，用来收集不活跃的资源集（例如在product flavors 和 build types中定义的资源）。并且能够妥善处理静态资源的声明。同时针对移除无用资源功能提供了快速修复功能（后悔了？）。
	- 隐式API检查。直到现在，lint依然能够在所有平台上根据你的最小sdk版本对方法调用和变量引用进行检查。但是，有很多的类已经实现了新的借口，比如`Closeable`，在最新的版本或者那些继承该类的子类都已经发生了变化。举个栗子，KeyEvent类只有在API 9版本才有个父类InputEvent。 这也就是说，在所有你隐式或者显示转换的地方，都有一个潜在的崩溃风险。现在，Lint开始跟踪这些API的变化并且全部隐式检查。
![implicit-cast](https://raw.githubusercontent.com/xiongwei-git/xiongwei-git.github.io/master/img/blog/implicit-cast.png)
	- 几个新的Lint检查-对使用RecyclerView 时容易犯的一个错误进行检查，对Parcelable 加载时一个潜在的崩溃进行检查，以及8个从字节码分析移植到IDE内部分析的Lint 检查功能，如此之后，它们便能在编辑器的后台运行。
![recyclerview](https://raw.githubusercontent.com/xiongwei-git/xiongwei-git.github.io/master/img/blog/recyclerview.png)
	- `@IntDef`,`@IntRange`和`@Size`检查不仅仅针对原始的整形进行检查，同样支持数组和可变参数。
	- 还有一些其他杂七杂八的改进，例如即使当前编辑器里面存在语法错误，Lint仍旧会运行，并且在IDE分析窗口中显示Lint检查的问题分类。使第三方的（来自AAR库）的lint检查规则在IDE里工作的更好，诸如此类等等。

   * **数据绑定**: 在XML编辑器中，支持数据绑定表达式的补全功能。
   ![dbcompletion](https://raw.githubusercontent.com/xiongwei-git/xiongwei-git.github.io/master/img/blog/dbcompletion.png)
   
   * **测试用例**：经过试验，测试用例功能（其中，同时在IDE中启用了单元测试和自动化测试）得到了进一步改善，现在默认打开。
	![artifacts](https://raw.githubusercontent.com/xiongwei-git/xiongwei-git.github.io/master/img/blog/artifacts.png)
	
   * 样式标签中的代码补全功能更加智能了，它能从父辈样式中寻找并给出合格的条目。
   * 我们同样在为了提升无障碍支持而努力，还包括SDK管理器和向导相关的一些基础功能有关的工作。
   * 最后一条，一如既往的，修复了很多bug。如果你发现了问题或者bug并没有修复，请告诉我们。

### 安装说明
您可以通过内置的补丁机制（检查更新），更新当前的2.0预览版本安装预览版 v5。
您还可以通过修补机制更新1.5版本至2.0预览版本，但你可能不希望这样做：点击查看[如果想体验预览版，如何同时安装两个版本的android studio](https://sites.google.com/a/android.com/tools/tips/using-multiple-android-studio-versions)
您也能直接下载完整预览版本的zip安装包，[下载地址](https://sites.google.com/a/android.com/tools/download/studio/builds/2-0-preview-5)

### 有问题？
如果您在使用过程中遇到问题，请检查[已知问题](http://tools.android.com/knownissues),我们会在必要的时候更新相关问题。
![20p5](https://raw.githubusercontent.com/xiongwei-git/xiongwei-git.github.io/master/img/blog/20p5.png)



[^canary ]: 还没有做好发布准备的代码  参考自[Google的产品质量之道](http://www.infoq.com/cn/news/2011/03/Ensuring-Product-Quality-Google/)