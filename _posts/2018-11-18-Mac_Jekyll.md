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

　　首先打开 [Jekyll 中文文档](https://www.jekyll.com.cn/)，按照指令进行环境准备。

    $ gem install jekyll
    
　　这一步可能会遇到一些问题：
   
　　![](/images/posts/Mac_Jekyll/1.png)

　　如上图所说，我对 /Library/Ruby/Gems/2.3.0 这个文件夹没有写权限，指令未完成，那就给文件夹权限呗。

    $ cd /Library/Ruby/Gems

    $ sudo chmod -R 777 2.3.0/
    
    Password:
    
    $ gem install jekyll
    
> 注意： 是 cd 到对应文件夹的父目录，然后执行 sudo chmod -R 777 后面跟上文件夹名称，然后输入密码，再执行一次，完成。

<br>

　　接下来进入到博客文件夹，启动服务。

    $ cd *****.github.io
    
    $ jekyll serve
    
　　此时出现了新的问题：

　　![](/images/posts/Mac_Jekyll/2.png)

    Configuration file: /Users/czre/git/blog/_config.yml
       Deprecation: The 'gems' configuration option has been renamed to 'plugins'. Please update your config file accordingly.
    Dependency Error: Yikes! It looks like you don't have jekyll-paginate or one of its dependencies installed. In order to use Jekyll as currently configured, you'll need to install this gem. The full error message from Ruby is: 'cannot load such file -- jekyll-paginate' If you run into trouble, you can find helpful resources at https://jekyllrb.com/help/! 

　　这是因为没有 jekyll-paginate，使用如下指令安装一下就好了。

    $ gem install jekyll-paginate 
    
　　另外也有可能出现没有 jekyll-gist 和 jekyll-sitemap 等错误，解决方法同上，这些错误取决于模板所采用的一些服务，需要安装好这些服务。 

　　![](/images/posts/Mac_Jekyll/3.png)

　　经过上述步骤，输入以下指令就可以在 [http://127.0.0.1:4000/](http://127.0.0.1:4000/) 或者 [http://localhost:4000](http://localhost:4000) 见到博客了。

    $ jekyll serve

　　![](/images/posts/Mac_Jekyll/4.png)


#### 以上

___
### Q&A

随笔有不妥的地方感谢留言指正，谢谢您！  
其他知识可上网查找资料，共同学习进步。  
在操作过程中或者随笔有问题的话欢迎在 [在 macOS 中安装 Jekyll](https://liuxy0551.github.io/2018/11/Mac_Jekyll/) 里提问或指正，或者从 [关于我](https://liuxy0551.github.io/about/) 中可以找到我的联系方式。


<br>
转载请注明：[刘先玉的博客](https://liuxy0551.github.io/) » [在 macOS 中安装 Jekyll](https://liuxy0551.github.io/2018/11/Mac_Jekyll/)
