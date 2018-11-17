---
layout: post
title: 在 macOS 中安装 Jekyll
date: 2018-11-18
tag: macOS、Jekyll
---

___
##### 　　最近换了 macOS，所以把博客也迁移到了 macOS 上，这里做一些环境的准备，期间遇到了一些在 Windows 上没见过的问题，记录一下。

___

#### 电脑已经安装好 Git 环境，另外 macOS 自带有 Ruby，RubyGems 也需要，这个是我之前折腾 Consolas 字体时顺带安装的。
<br>

### 一、按部就班

　　首先打开 [Jekyll 中文文档](https://www.jekyll.com.cn/)，按照指令进行环境准备。

    $ gem install jekyll
    
　　这一步可能会遇到一些问题：
   
　　![](/images/posts/Mac-Jekyll/1.png)

　　如上图所说，我对 /Library/Ruby/Gems/2.3.0 这个文件夹没有写权限，指令未完成，那就给文件夹权限呗。

    $ cd /Library/Ruby/Gems

    $ sudo chmod -R 777 2.3.0/
    
    Password:
    
    $ gem install jekyll
    
> 注意： 是 cd 到对应文件夹的父目录，然后执行 sudo chmod -R 777 后面跟上文件夹名称，然后输入密码，再执行一次，完成。
<br>

　　![](/images/posts/Mac-Jekyll/2.png)






### 二、具体实现

#### 1、HTML 部分

　　![](/images/posts/Img-Center-CSS/1.png)

    <mt-swipe :auto="0">
      <mt-swipe-item class="product-swipe" v-for="item in product_info.images" :key="item.piid">
        <img :src="item.piurl" class="product-img">
      </mt-swipe-item>
    </mt-swipe>

#### 2、CSS 部分

　　![](/images/posts/Img-Center-CSS/2.png)

      .product-swipe {
        width: 750px;
        height: 750px;
        .product-img {
          max-width: 750px;
          max-height: 750px;
          position: absolute;
          top: 0;
          bottom: 0;
          left: 0;
          right: 0;
          margin: auto;
        }
      }
      .mint-swipe {
        width: 750px;
        height: 750px;
      }

___
### Q&A

随笔有不妥的地方感谢留言指正，谢谢您！  
其他知识可上网查找资料，共同学习进步。  
在操作过程中或者随笔有问题的话欢迎在 [图片大小不固定时在 div 中居中显示](https://liuxy0551.github.io/2018/11/Mac-Jekyll/) 里提问或指正，或者从 [关于我](https://liuxy0551.github.io/about/) 中可以找到我的联系方式。


<br>
转载请注明：[刘先玉的博客](https://liuxy0551.github.io/) » [图片大小不固定时在 div 中居中显示](https://liuxy0551.github.io/2018/10/Img-Center-CSS/)
