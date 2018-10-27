---
layout: post
title: 在 VMware 中安装 MacOS High Sierra 10.13
date: 2018-10-27
tag: MacOS
---

___
##### 　　最近抽空把以前在 VMware 中安装 MacOS 的过程回忆了一下，同时在自己电脑上再次安装了一遍，记录一下，随笔图片较多。

___
## 工具 / 原料

Windows 系统、VMware、unlocker（使得 VMware 可以识别到 MacOS）、MacOS High Sierra 10.13 镜像

___
## 方法 / 步骤

### 1、准备工作

　　(1) 这篇随笔记录的过程是在 Windows 系统上完成，准备工作需要在 Windows 上安装好 VMware，并下载好所需文件，链接: [https://pan.baidu.com/s/1FJ5KlH0ea6Fdb12siwOV4Q](https://pan.baidu.com/s/1FJ5KlH0ea6Fdb12siwOV4Q)
 
 提取码: p8jp。　　其中文件夹是第二个压缩包解压后的文件，第一个压缩包备用，第三个压缩包就是 MacOS High Sierra 10.13 镜像。如果链接失效，可以从[关于我](https://liuxy0551.github.io/about/)中找到我的联系方式。
　　
　　![](/images/posts/VMware-MacOS/36.png)

　　(2) 保证 VMware 运行需要的几个服务已经启动，没设置过这些服务手动启动的可忽略。VMware 在关闭状态时，解压 unlocker-master.zip 文件，进入解压的文件夹，右击 win-install.cmd 文件，

以管理员运行，等待运行完成即可。VMware 软件运行时以管理员运行该文件可能会报错，如果没有运行完成的话，可能会在新建虚拟机的时候发现没有 Apple Mac OS X(M) 操作系统选项。

　　![](/images/posts/VMware-MacOS/1.png)<br>

### 2、新建虚拟机，载入 MacOS

　　在完成以上准备工作后，就可以开始新建虚拟机载入 MacOS 了，后续步骤以图片为主。

　　![](/images/posts/VMware-MacOS/2.png)
　　![](/images/posts/VMware-MacOS/3.png)
　　![](/images/posts/VMware-MacOS/4.png)
　　![](/images/posts/VMware-MacOS/5.png)
　　![](/images/posts/VMware-MacOS/6.png)<br>

　　下图中的内存和处理器的分配数量可依主机性能而定，多多益善。

　　![](/images/posts/VMware-MacOS/7.png)
　　![](/images/posts/VMware-MacOS/8.png)
　　![](/images/posts/VMware-MacOS/9.png)

　　    正常情况下，初次开启此虚拟机后会出现如下图的错误，unlocker 的开发者给出了解决方法：找到并打开安装目录下的 XXXX.vmx 文件，使用记事本打开后，在 smc.present = "TRUE" 后添加

以下代码后保存，问题即可解决。

    smc.version = "0"

　　![](/images/posts/VMware-MacOS/10.png)
　　![](/images/posts/VMware-MacOS/11.png)<br>

　　按上图修改安装文件后，再次点击开启此虚拟机，即可开始初次开机时系统的安装过程。

　　![](/images/posts/VMware-MacOS/12.png)
　　![](/images/posts/VMware-MacOS/13.png)
　　![](/images/posts/VMware-MacOS/14.png)

　　![](/images/posts/VMware-MacOS/15.png)<br>

　　安装时会出现上图中的情况，只有一个磁盘。为了文件管理方便，我将磁盘抹掉并改名，然后将系统安装在新出现的磁盘上。点击继续后就是系统的安装过程，静候佳音。

　　![](/images/posts/VMware-MacOS/16.png)
　　![](/images/posts/VMware-MacOS/17.png)
　　![](/images/posts/VMware-MacOS/18.png)<br>

　　接下来就是系统的一些基本设置。

　　![](/images/posts/VMware-MacOS/19.png)
　　![](/images/posts/VMware-MacOS/20.png)<br>

### 3、安装 VMware Tools

　　VMware 中安装 VMware Tools 后，可支持自由拖拽的功能，鼠标也可以在虚拟机与主机之前自由移动（不用再按 Ctrl + Alt），且虚拟机屏幕也可以全屏了，好处多多。

　　![](/images/posts/VMware-MacOS/21.png)
　　![](/images/posts/VMware-MacOS/22.png)
　　![](/images/posts/VMware-MacOS/23.png)
　　![](/images/posts/VMware-MacOS/24.png)
　　![](/images/posts/VMware-MacOS/25.png)
　　![](/images/posts/VMware-MacOS/26.png)<br>

　　安装完成后重启，会报错 - 系统扩展已被阻止，按照图片顺序设置，允许载入该系统软件。

　　![](/images/posts/VMware-MacOS/27.png)
　　![](/images/posts/VMware-MacOS/28.png)<br>

　　允许载入后按上述步骤重新安装 VMware Tools。

　　![](/images/posts/VMware-MacOS/29.png)
　　![](/images/posts/VMware-MacOS/30.png)
　　![](/images/posts/VMware-MacOS/31.png)
　　![](/images/posts/VMware-MacOS/32.png)
　　![](/images/posts/VMware-MacOS/33.png)<br>

　　安装完成后重启，按下图推出“ VMware Tools ”，这样桌面就很干净了。

　　![](/images/posts/VMware-MacOS/34.png)
　　![](/images/posts/VMware-MacOS/35.png)<br>


>**注意**
>* 1、unlocker 的储存路径不要有中文字符，否则会安装失败，而且没有失败的提示；
>* 2、有什么问题可以多重启，多百度。
>* 3、如果系统可以使用，尽量不更新；

___
### Q&A

随笔有不妥的地方感谢留言指正，谢谢您！  
其他知识可上网查找资料，共同学习进步。  
在操作过程中或者随笔有问题的话欢迎在[在 VMware 中安装 MacOS High Sierra 10.13](https://liuxy0551.github.io/2018/10/VMware+MacOS/) 里提问或指正。

<br>

转载请注明：[刘先玉的博客](https://liuxy0551.github.io/) » [在 VMware 中安装 MacOS High Sierra 10.13](https://liuxy0551.github.io/2018/10/VMware+MacOS/)
