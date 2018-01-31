---
layout: post
title: 轻松搞定 Android 开发环境的搭建
date: 2017-03-30
tag: Android
---

___
##### 　　在Windows下安装Android的开发环境虽说不简单但也算不上复杂，本篇经验写给同为小白的朋友们，  
##### 文章步骤经作者测试正确可行，希望对准备进入Android开发的你们有所帮助。

___
# 工具 / 原料
    JDK 1.8（其他版本同理）、Eclipse、Android SDK、ADT

___
# 方法 / 步骤

## 一、JDK的安装与环境变量的配置

　　选择[Oracle公司官网](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)下载对应版本的JDK直接选择百度“JDK”下载。安装完成后出现两个文件夹 jdk 和 jre，接下来我们需要设置  
三个系统变量，右击	我的电脑->属性->高级->系统设置->环境变量->系统变量，三个系统变量分别是：

|变量名|变量值|备注|
|----|----|----|
|JAVA_HOME|`E:\java\jdk1.8.0_121`|变量值为JDK在你电脑上的安装路径|
|CLASSPATH|`.;%JAVA_HOME%\lib;%JAVA_HOME%\lib\tools.jar`|注意变量值字符串前面有一个"."表示当前目录|
|Path|';%JAVA_HOME%\bin;%JAVA_HOME%\jre\bin;`|Path属性已存在，可直接编辑，在原来变量后追加即可|

- 变量值中如果有内容，用 ; 隔开
- 测试是否安装配置成功：Win+R，输入 cmd，按 Enter 继续，输入 javac，按 Enter，出现相关内容即证明安装配置成功

## 二、下载安装Eclipse

　　Eclipse 是一种 Java 应用程序及 Android 开发的 IDE（集成开发环境），不需要安装，下载后解压，剪切 eclipse 文件夹到你想安装的地方，打开时设置你的工作目录即日后各种项目的存放位置，此时已完成了普通 Java 应用程序的开发环境准备。本篇经验下载的是 [Eclipse IDE for Java EE Developers](https://www.eclipse.org/downloads/download.php?file=/technology/epp/downloads/release/oxygen/2/eclipse-jee-oxygen-2-win32-x86_64.zip) 版本，点击 `DOWNLOAD` 下载，然后等待浏览器下载。

## 三、下载安装Android SDK

　　我们要使用 Eclipse 来开发 Android 应用程序，那么需要下载 Android SDK 和在 Eclipse 中安装 ADT 插件，这个插件能让 Eclips 和 Android SDK 关联起来。

　　打开 http://developer.android.com/sdk/index.html（没有梯子打不开）可下载 Android SDK。或者从下面两个网站下载
[http://www.androiddevtools.cn/](http://www.androiddevtools.cn/)  
[http://tools.android-studio.org/index.php/sdk/](http://tools.android-studio.org/index.php/sdk/)

### 1.下载

### 2.安装

#### (1).安装

#### (2).将SDK Manage上的https请求更改成http请求

#### (3).安装ADT（离线安装）

___
# 注 意 事 项
