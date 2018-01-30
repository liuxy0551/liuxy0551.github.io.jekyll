---
layout: post
title: 轻松搞定 Android 开发环境的搭建
date: 2017-03-30
tag: Android
---

　　在Windows下安装Android的开发环境虽说不简单但也算不上复杂，本篇经验写给同为小白的朋友们，文章步骤经作者测试正确可行，希望对准备进入Android开发的你们有所帮助。

## 工具 / 原料


JDK 1.8（其他版本同理）
Eclipse
Android SDK
ADT


## 方法 / 步骤

### 一、JDK的安装与环境变量的配置

   选择[Oracle官网](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)下载对应版本或者直接选择百度“JDK”下载。安装完成后出现两个文件夹jdk和jre，接下来我们需要设置三个系统变量，右击	我的电脑->属性->高级系统设置->环境变量->系统变量，三个系统变量分别是：

>* 1、JAVA_HOME：变量值为JDK在你电脑上的安装路径
			变量名：JAVA_HOME
			变量值：E:\java\jdk1.8.0_121
>* 2、CLASSPATH：注意变量值字符串前面有一个"."表示当前目录
			变量名：CLASSPATH
			变量值：.;%JAVA_HOME%\lib;%JAVA_HOME%\lib\tools.jar
>* 3、Path：Path属性已存在，可直接编辑，在原来变量后追加即可
			变量名：Path
			变量值：;%JAVA_HOME%\bin;%JAVA_HOME%\jre\bin;


### 2、申请包含 Network Extension 的描述文件
			![](/images/posts/AndroidIDE/javamulu.jpg)
			![](/images/posts/AndroidIDE/xinjianxitongbianliang.jpg)
			![](/images/posts/AndroidIDE/cmd-javac.jpg)

		测试是否安装配置成功：Win+R，输入cmd，按Enter继续，输入javac，按Enter，出现相关内容即证明安装配置成功。

### 1、向 Apple 申请开发 Network Extension 权限

　　首先要先写封邮件给 [networkextension@apple.com](mailto:networkextension@apple.com) ，问苹果要开发 Network Extension 的权限。     
苹果收到邮件后会自动回复邮件，在 [https://developer.apple.com/contact/network-extension/](https://developer.apple.com/contact/network-extension/) 里面填写申请表格，内容包括：     

```
Organization：               

Company / Product URL:             

What's your product's target market?              

What's your company's primary function?             

Describe your application and how it will use the Network Extension framework.            

What type of entitlement are you requesting?                     

。。。
```

申请后大概两周左右能收到 Aplle的 确认信，如：

```
Hi,

Thanks for your interest in the Network Extension APIs.

We added a new template containing the Network Extension entitlements to your team.

。。。。
```

### 2、申请包含 Network Extension 的描述文件

![](/images/posts/Wifilist/PastedGraphic.png)

选择包含 Network Extension 的描述文件，后点击下载，下载完成双击描述文件。

### 3、配置 Info.plist

Xcode Info.plist 里 Required background modes 添加 一个 network-authentication(item)

![](/images/posts/Wifilist/infoplist.png)

### 4、配置 entitlements

Demo.entitlements（Demo是项目名称） 里添加 Key-Value: com.apple.developer.networking.HotspotHelper -> YES

![](/images/posts/Wifilist/entitlement.png)

### 5、iOS 获取 Wifi 列表代码实现

导入头文件

```
#import <NetworkExtension/NetworkExtension.h>  
```

代码实现

```                
- (void)getWifiList {

	if (![[[UIDevice currentDevice] systemVersion] floatValue] >= 9.0) {return;}
	dispatch_queue_t queue = dispatch_queue_create("com.leopardpan.HotspotHelper", 0);
	[NEHotspotHelper registerWithOptions:nil queue:queue handler: ^(NEHotspotHelperCommand * cmd) {
		if(cmd.commandType == kNEHotspotHelperCommandTypeFilterScanList) {
			for (NEHotspotNetwork* network  in cmd.networkList) {
				NSLog(@"network.SSID = %@",network.SSID);
			}
		}
	}];
}
```
kNEHotspotHelperCommandTypeFilterScanList： 表示扫描到 Wifi 列表信息。

NEHotspotNetwork 里有如下信息：

>* SSID：Wifi 名称
>* BSSID：站点的 MAC 地址
>* signalStrength： Wifi信号强度，该值在0.0-1.0之间     
>* secure：网络是否安全 (不需要密码的 Wifi，该值为 false)
>* autoJoined： 设备是否自动连接该 Wifi，目前测试自动连接以前连过的 Wifi 的也为 false 。
>* justJoined：网络是否刚刚加入
>* chosenHelper：HotspotHelper是否为网络的所选助手

[官方文档连接](https://developer.apple.com/reference/networkextension/nehotspotnetwork)


### 6、获取Wifi列表回调

当你把上面的代码写完，并成功运行项目后，发现并没有Wifi列表的回调。因为你还没刷新Wifi列表，你需要：

* 打开手机系统设置 -> WLAN -> 系统 Wifi 列表加载出来时，上面代码部分才会回调，才能获取到 Wifi 列表。

<img src="/images/posts/Wifilist/WLAN.png" height="360" width="200">  

这个时候你就能看到控制台源源不断的Log。

### 注意事项

* 1、获取Wifi列表功能由于是需要申请后台权限，所以能后台激活App(应用程序)，而且激活后App的进程能存活几个小时。
* 2、整个获取Wifi列表不需要App用户授权，也就是在App用户无感知下获取设备的Wifi列表信息，使用时请正当使用。
* 3、Wifi列表获取 NetworkExtension 是 iOS 9以后才出的，目前 iOS 9 已经覆盖很广了。


下面付一张来自 [TalkingData 对iOS操作系统的统计报表](https://www.talkingdata.com/index/#/device/os/zh_CN)，时间：2017-01-03

<img src="/images/posts/Wifilist/systemVersion.png" height="280" width="600">  

### Q&A

在操作过程或者文章有问题的话欢迎在 [原文](http://baixin.io/2017/01/iOS_Wifilist/) 里提问或指正。

>* 使用 Demo 我就不提供了，你如果没有申请 NetworkExtension 权限，提供了 Demo 你也无法使用。

<br>

参考资源：[NEHotspotHelper NetworkExtension API iOS9.0](http://stackoverflow.com/questions/31704292/nehotspothelper-networkextension-api-ios9-0)

<br>
转载请注明：[潘柏信的博客](http://baixin) » [Wifi 定位原理及 iOS Wifi 列表获取](http://baixin.io/2017/01/iOS_Wifilist/)  
