---
layout: post
title: 轻松搞定 Android 开发环境的搭建
date: 2017-03-30
tag: Android
---

#### 在Windows下安装Android的开发环境虽说不简单但也算不上复杂，本篇经验写给同为小白的朋友们，文章步骤  经作者测试正确可行，希望对准备进入Android开发的你们有所帮助。

****

|Author|刘先玉|
|---|---
|E-mail|liuxy0551@qq.com

****

# 工具 / 原料

    JDK 1.8（其他版本同理）、Eclipse、Android SDK、ADT

# 方法 / 步骤

## 一、JDK的安装与环境变量的配置

　　选择[Oracle公司官网](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)下载对应的  
版本直接选择百度“JDK”下载。安装完成后出现两个文件夹 jdk 和 jre，接下来我们需要设置三个系统变量，右击	我的电脑->属性->高级->  
系统设置->环境变量->系统变量，三个系统变量分别是：


|变量名|变量值|备注|
|----|----|----|
|JAVA_HOME|`E:\java\jdk1.8.0_121`|变量值为JDK在你电脑上的安装路径|
|CLASSPATH|``.;%JAVA_HOME%\lib;%JAVA_HOME%\lib\tools.jar`|注意变量值字符串前面有一个"."表示当前目录|
|Path|``;%JAVA_HOME%\bin;%JAVA_HOME%\jre\bin;``|Path属性已存在，可直接编辑，在原来变量后追加即可|

- 变量值中如果有内容，用;隔开
- 测试是否安装配置成功：Win+R，输入cmd，按Enter继续，输入javac，按Enter，出现相关内容即证明安装配置成功

## 二、下载安装Eclipse

## 三、下载安装Android SDK

### 1.下载

### 2.安装

#### (1).安装

#### (2).将SDK Manage上的https请求更改成http请求

#### (3).安装ADT（离线安装）

# 注 意 事 项
