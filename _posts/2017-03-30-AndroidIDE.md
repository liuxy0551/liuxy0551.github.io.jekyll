---
layout: post
title: 轻松搞定 Android 开发环境的搭建
date: 2017-03-30
tag: Android
---

___
#### 　　在Windows下安装Android的开发环境虽说不简单但也算不上复杂，本篇经验写给同为小白的朋友们，  
#### 文章步骤经作者测试正确可行，希望对准备进入Android开发的你们有所帮助。

___
# 工具 / 原料
    JDK 1.8（其他版本同理）、Eclipse、Android SDK、ADT

___
# 方法 / 步骤

## 一、JDK的安装与环境变量的配置

　　选择[Oracle公司官网](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)下载对应的版本直接选择百度“JDK”下载。安装完成后出现两个文件夹 jdk 和 jre，接下来我们需要设置三个  
系统变量，右击	我的电脑->属性->高级->系统设置->环境变量->系统变量，三个系统变量分别是：

|变量名|变量值|备注|
|----|----|----|
|JAVA_HOME|`E:\java\jdk1.8.0_121`|变量值为JDK在你电脑上的安装路径|
|CLASSPATH|`.;%JAVA_HOME%\lib;%JAVA_HOME%\lib\tools.jar`|注意变量值字符串前面有一个"."表示当前目录|
|Path|``;%JAVA_HOME%\bin;%JAVA_HOME%\jre\bin;``|Path属性已存在，可直接编辑，在原来变量后追加即可|

- 变量值中如果有内容，用;隔开
- 测试是否安装配置成功：Win+R，输入cmd，按Enter继续，输入javac，按Enter，出现相关内容即证明安装配置成功

## 二、下载安装Eclipse

　　Eclipse是一种Java应用程序及Android开发的IDE（集成开发环境），不需要安装，下载后解压，剪切eclipse文件夹到你想安装的地方，打开  
时设置你的工作目录即日后各种项目的存放位置，此时已完成了普通java应用程序的开发环境准备。本篇经验下载的是Eclipse IDE for Java EE   Developers版本，下载时无需输入邮箱，等待浏览器左下方的“正在连接”完成即可弹出下载界面。

## 三、下载安装Android SDK

我们要使用Eclipse来开发Android应用程序，那么需要下载Android SDK和在Eclipse中安装ADT插件，这个插件能让Eclipse和Android SDK关联起来。

### 1.下载

### 2.安装

#### (1).安装

#### (2).将SDK Manage上的https请求更改成http请求

#### (3).安装ADT（离线安装）

___
# 注 意 事 项
