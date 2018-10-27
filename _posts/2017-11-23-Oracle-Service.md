---
layout: post
title: 如何快速开启和关闭 Orcale 所需的服务
date: 2017-11-23
tag: Oracle
---

___
##### 　　个人在学习 orcale 时，安装好后会在系统中添加七个 orcale 开头的服务，后文介绍。但这七个服务在启动后都很占资源，所以在
##### 我们不使用 orcale 的时候，就可以将这些服务关闭。这就是这篇经验解决的问题——快速开启或关闭 orcale 所需的服务。

___
## 工具 / 原料

Windows 系统、orcale 11g、PLSQL Developer 12（等第三方）

___
## 方法 / 步骤

### 1、更改服务启动类型

　　安装好 orcale 11g 和第三方工具 PLSQL Developer 12 后，右击我的电脑 -> 服务或者控制面板 -> 管理工具 -> 服务，找到 orcale 开头的七个或六个服务，将这些服务的启动类型全部改成手动。
<br>![](/images/posts/Oracle-Service/service.png)

### 2、理解服务含义

　　成功安装 Oracle 11g 后，共有七个服务，这七个服务的含义可以参照[这篇百度知道理解](https://zhidao.baidu.com/question/265616629111117845.html)，内容如下：
<br>![](/images/posts/Oracle-Service/seven.png)<br>

### 3、新建.bat文件

　　所以当我们使用 PLSQL Developer 12 等第三方可视化界面时，只需要启动 OracleServiceORCL 和 OracleOraDb11g_home1TNSListener 两个服务即可。新建一个文本文件，打开后复制粘贴下述文本，保存后将文件后缀名改为“bat”。

    @echo off
    for /f "skip=3 tokens=4" %%i in ('sc query "OracleServiceORCL"') do set "zt=%%i" &goto :next
    :next
    if /i "%zt%"=="RUNNING" (
      echo 1.服务OracleServiceORCL正在运行
    ) else (
      echo 1.服务OracleServiceORCL已停止
    )

    for /f "skip=3 tokens=4" %%i in ('sc query "OracleOraDb11g_home1TNSListener"') do set "zt=%%i" &goto :next
    :next
    if /i "%zt%"=="RUNNING" (
      echo 2.服务OracleOraDb11g_home1TNSListener正在运行
    ) else (
      echo 2.服务OracleOraDb11g_home1TNSListener已停止
    )

    choice /c:12 /m "启动/停止ORCALE服务[1启动,2停止]"
    if errorlevel 2 goto two
    if errorlevel 1 goto one
    :one
    echo 正在启用服务...
    net start "OracleServiceORCL"
    net start "OracleOraDb11g_home1TNSListener"
    echo 服务OracleServiceORCL、OracleOraDb11g_home1TNSListener 启动成功！

    choice /c:12 /m " 是否启动PLSQL Developer 12 ？[1是,2否]"
    if errorlevel 2 exit
    if errorlevel 1 start "" "E:\PLSQL Developer 12\plsqldev.exe"
    >nul

    :two
    echo 正在禁用服务...
    net stop "OracleServiceORCL"
    net stop "OracleOraDb11g_home1TNSListener"

    echo 服务OracleServiceORCL、OracleOraDb11g_home1TNSListener 禁用成功！
    echo 可按任意键退出...
    timeout 3
    exit

<br>![](/images/posts/Oracle-Service/bat.png)<br>

>**注意**
>　　上图中矩形方框中是你 PLSQL 的安装位置，椭圆形标注的是服务名，与系统中的服务名要一致。

<br>

### 4、美观步骤

　　将上述文本文件改名为“PLSQL Developer 12.bat”，将文件剪切到 PLSQL Developer 12 的安装目录（随意哪个目录），然后“发送到 -> 桌面快捷方式”右击桌面上该快捷方式 -> 属性 -> 更改图标 -> 浏览，进入 PLSQL 安装目录，选择 plsqldev.exe，一路确认，将快捷方式改名为“PLSQL Developer 12”。
<br>
<br>![](/images/posts/Oracle-Service/tubiao.png)<br>

### 5、启动与停止服务

　　打开快捷方式，根据提示选择，关闭服务后，两个服务已经停止。同理，启动服务按提示进行即可。使用后可前往“服务”查看服务是否已启动或停止。
<br>
<br>![](/images/posts/Oracle-Service/qidong.png)

上文提到的部分文件：
链接：[http://pan.baidu.com/s/1hr5J3JA](http://pan.baidu.com/s/1hr5J3JA) 密码：x705

___
### Q&A

随笔有不妥的地方感谢留言指正，谢谢您！  
其他知识可上网查找资料，共同学习进步。  
在操作过程中或者随笔有问题的话欢迎在[如何快速开启和关闭 Orcale 所需的服务](https://liuxy0551.github.io/2017/05/Oracle-Service/) 里提问或指正，或者从[关于我](https://liuxy0551.github.io/about/)中可以找到我的联系方式。 

>* 1、通过 bat 文件启动服务后需要等待 20~60 秒后才能登录，由电脑性能决定；
>* 2、类似的，MySQL的服务也可以这么解决，VMware也可以。


<br>
转载请注明：[刘先玉的博客](https://liuxy0551.github.io/) » [如何快速开启和关闭 Orcale 所需的服务](https://liuxy0551.github.io/2017/11/Oracle-Service/)
