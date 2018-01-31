---
layout: post
title: 轻松搞定 Android 开发环境的搭建
date: 2017-03-30
tag: Android
---

#####     在Windows下安装Android的开发环境虽说不简单但也算不上复杂，本篇经验写给同为小白的朋友们，文章步骤经作者测试正确可行，
##### 希望对准备进入Android开发的你们有所帮助。

## 工具 / 原料

	JDK 1.8、Eclipse、Android SDK、ADT

## 方法 / 步骤

### 一、JDK的安装与环境变量的配置

   选择[Oracle公司官网](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)下载对应版本或者直接选择百度“JDK”下载。安装完成后出现两个文件夹 jdk 和 jre，接下来我们需要设置三个系统变量，右击	我的电脑->属性->高级
   系统设置->环境变量->系统变量，三个系统变量分别是：

	 1、JAVA_HOME：变量值为JDK在你电脑上的安装路径
			变量名：JAVA_HOME
			变量值：E:\java\jdk1.8.0_121
	 2、CLASSPATH：注意变量值字符串前面有一个"."表示当前目录
			变量名：CLASSPATH
			变量值：.;%JAVA_HOME%\lib;%JAVA_HOME%\lib\tools.jar
	 3、Path：Path属性已存在，可直接编辑，在原来变量后追加即可
			变量名：Path
			变量值：;%JAVA_HOME%\bin;%JAVA_HOME%\jre\bin;

   测试是否安装配置成功：Win+R，输入cmd，按Enter继续，输入javac，按Enter，出现相关内容即证明安装配置成功。

### 二、下载安装Eclipse

        Eclipse是一种Java应用程序及Android开发的IDE（集成开发环境），不需要安装，下载后解压，剪切eclipse文件夹到你想安装的地方，
    打开时设置你的工作目录即日后各种项目的存放位置，此时已完成了普通java应用程序的开发环境准备。本篇经验下载的是[Eclipse IDE
    for Java EE Developers](https://www.eclipse.org/downloads/download.php?file=/technology/epp/downloads/release/oxygen/2/
    eclipse-jee-oxygen-2-win32-x86_64.zip) 版本，点击链接，点击 Download，下载时无需输入邮箱，等待浏览器左下方的“正在连接”完成
    即可弹出下载界面。

### 三、下载安装Android SDK

      我们要使用Eclipse来开发Android应用程序，那么需要下载Android SDK和在Eclipse中安装ADT插件，这个插件能让Eclipse和Android SDK
    关联起来。
		
#### 1.下载：

	打开http://developer.android.com/sdk/index.html（没有梯子打不开）可下载Android SDK。或者从下面两个网站下载
	[http://www.androiddevtools.cn/](http://www.androiddevtools.cn/)
	<img src="/images/posts/AndroidIDE/SDKTools1.png" height="526" width="298">

	[http://tools.android-studio.org/index.php/sdk/](http://tools.android-studio.org/index.php/sdk/)
	![](/images/posts/AndroidIDE/SDKTools2.png)

#### 2.安装：
			下载完成后双击解压“installer_r24.4.1-windows.exe”选择解压文件夹，解压完成后双击“SDK Manager”，加载可安装的安卓版本。
			![](/images/posts/AndroidIDE/AndroidSDKManager.png)

			因为国内有墙，有时候会出现加载安卓版本失败的情况。
			从万能的百度搜索上，找到了解决这个问题的方法：

##### 更改host文件
			在C:\Windows\System32\drivers\etc目录下，用记事本打开“hosts”文件，将下面两行信息加到hosts文件的末尾，保存退出。

			203.208.46.146 dl.google.com
			203.208.46.146 dl-ssl.google.com

##### 将SDK Manage上的https请求更改成http请求

			打开SDK Manager，Tools->Options，勾选 Force https://..sources to be fetched using http://... ，如图。退出重新打开SDK Manager，一般情况下就可以正常加载了。





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
