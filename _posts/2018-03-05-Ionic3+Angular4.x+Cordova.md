---
layout: post
title: Ionic 3 + Angularjs 4.x + Cordova 混合开发项目小战
date: 2018-03-05
tag: Ionic3, Angularjs 4.x, Cordova
---

___
##### 　　在实习过程中因项目组需要，学习了一段时间的混合开发，工银系统新版APP的部分开发工作。主要是利用 Ionic 3 + Angularjs 4.x + Cordova  混合开发这个项目，做的是一些基本工作，记录一下。内容很多，学会的也很多，记录下来的是一些此时觉得比较常用的知识点。

___
### 一、准备工作

    1、安装 python；
    2、安装编辑器： webstorm（个人推荐）或 VS Code，2 和 3中的具体步骤可自行百度；
    3、安装最新版本的 node js，运行命令 node -v 和 npm -v， 来验证一下你正在运行的是 node 6.9.x 和 npm 3.x.x 以上的版本。

### 二、了解 Angularjs

全局安装 Angular CLI 脚手架工具(只需要安装一次)：
安装 cnpm，npm 可能安装失败，建议先用 npm 安装一下，cnpm 用淘宝镜像安装 （https://npm.taobao.org/ )，指令：

    npm install -g cnpm --registry=https://registry.npm.taobao.org
使用 cnpm 安装脚手架：

    cnpm install -g @angular/cli

然后就可以新建项目了，进入刚才创建的项目里面启动服务:

    ng new my-app	    // 新建项目
    cd my-app
    cnpm install 		  // 安装依赖
    ng serve --open	  // 启动服务

### 三、ionic 3

全局安装 ionic，指令：

    npm install -g cordova ionic
新建带 tabs 的项目并启动服务（或menu）：

    ionic start ionicDemo02 tabs		// 新建项目
    cd ionicDemo02
    cnpm install 					          // 安装依赖（npm i）
    ionic serve 					          // 运行项目

ionic 3 新建组件的命令：ionic g page 组件名，如：

    ionic g page exam-online

### 四、打包项目

    这里只介绍我比较熟悉的 Android 打包，需要安装 Android SDK，（可参考[轻松搞定 Android 开发环境的搭建](https://liuxy0551.github.io/2017/03/AndroidIDE/)中安装 Android SDK 的部分）我安装的是 Android 8.0.0（API 26），与下文中的 gradle 4.1 相对应。
点此下载[gradle-4.1-all.zip](https://pan.baidu.com/s/1uvbvk2UBmsDHBHFckjq1ag) 密码：'yt35'。将这个压缩包解压，添加 bin 文件夹路径至环境变量 Path。
<br>![](/images/posts/Ionic3+Angular4.x+Cordova/path.png)

添加打包平台（Android）的命令：

    ionic cordova platform add android

修改 E:\AppDemo\Ionic2\cplease\platforms\android\cordova\lib\builders\GradleBuilder.js 中的第250行，将行末改为指向本地的gradle-4.1-all.zip，改为'../gradle-4.1-all.zip'。

打包成 apk 文件（生成一个 debug 包，无签名）的命令：

    ionic cordova build android  --prod
<br>![](/images/posts/Ionic3+Angular4.x+Cordova/building.png)
<br>![](/images/posts/Ionic3+Angular4.x+Cordova/success.png)

打包成 apk 文件的命令（比上一个打包出来的占用空间大）：

    ionic cordova build android

打包后的文件位置（自行对应这个文件夹下的 apk 文件）：

    E:\AppDemo\Ionic2\cplease\platforms\android\app\build\outputs\apk\debug

以下为部分真机测试时的截图
<br>![](/images/posts/Ionic3+Angular4.x+Cordova/1.png)
<br>![](/images/posts/Ionic3+Angular4.x+Cordova/2.png)
<br>![](/images/posts/Ionic3+Angular4.x+Cordova/3.png)
___
### Q&A

文章有不妥的地方感谢留言指正，谢谢您！
其他知识可上网查找资料，共同学习进步。
在操作过程中或者文章有问题的话欢迎在[本文](https://liuxy0551.github.io/2018/04/Ionic3+Angular4.x+Cordova/) 里提问或指正。

>* 1、写这篇文章的时候发现在 Atom 中选中单词，按住 Ctrl 后按 K， 再按 U，即可将选中的单词大写
>* 2、白天的技巧：Eclipse 中查看方法在哪里被调用了——选中方法，直接Ctrl+Shift+G或者Ctrl+Alt+H

<br>
转载请注明：[刘先玉的博客](https://liuxy0551.github.io/) » [Ionic 3 + Angularjs 4.x + Cordova 混合开发项目小战](https://liuxy0551.github.io/2018/04/Ionic3+Angular4.x+Cordova/)
