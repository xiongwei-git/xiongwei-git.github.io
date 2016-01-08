---
layout: post
title: Android Dev Tips 3-使用SublimeText编译Java
date:       2015-07-15
author:     "Ted"
tags:
    - Tips
---


在Android Studio中开发Android项目时，经常会遇到Java语言相关的问题，就想随手写一个demo验证一下。如果使用比较庞大的IDE,比如Android Studio或者Eclipse，就有点大材小用。最近我因为学习Python，安装了SublimeText这个韩国人开发的软件，一个很轻量级的文本编辑器。今天突然灵机一动，能不能用这个文本编辑器直接运行java代码。网上一搜索，教程果然很多，今天这里记录一下我自己的配置过程。一共有以下三步：

 > * 配置java编译环境
 > * 添加java编译脚本
 > * 修改Sublime中Java编译配置
 
 ------

## 1.java编译环境的配置
很简单，此处略过。

## 2.修改java编译脚本
创建一个文本文件，建议使用Sublime，保存格式为 **UTF-8** 取名为`buildJava.bat`，文本内容如下:  
```
      @ECHO OFF
      cd %~dp1
      ECHO Compiling %~nx1.......
      IF EXIST %~n1.class (
         DEL %~n1.class
      )
      javac %~nx1
      IF EXIST %~n1.class (
         ECHO -----------OUTPUT-----------
         java %~n1
      )
```
保存位置为jdk目录中的bin目录下。例如：**C:\Program Files\Java\jdk1.7.0_79\bin**

## 3.修改Sublime中Java编译配置

 1. 菜单Perferences->Browse Packages,打开Sublime的包目录
 2. 进入Java目录
 3. 编辑`JavaC.sublime-build`文件，建议使用SublimeText编辑。
    原文件：
   
    ``` 
    {
	"cmd": ["javac", "$file"],
	"file_regex": "^(...*?):([0-9]*):?([0-9]*)",
	"selector": "source.java",
    }
    ```

    修改为：
    
    ```
    {
	"cmd": ["buildJava.bat", "$file"],
	"file_regex": "^(...*?):([0-9]*):?([0-9]*)",
	"selector": "source.java",
	"encoding": "cp936"
    }
    ```  

第一行的目的是为了调用我们刚才写的java编译脚本，最后一行的目的是为了指定编码格式。
    
接下来，重启你的SublimeText，写一段Java的HelloWorld代码，`Ctrl+B`,即可见证奇迹。



