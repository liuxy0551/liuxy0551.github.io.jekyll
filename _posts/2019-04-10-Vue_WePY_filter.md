---
layout: post
title: Vue 和 WePY 中过滤器写法
date: 2019-04-10
tag: filter
---

___
##### 　　现有前端框架中普遍有 filter 的使用，最近在写一个小程序，需要显示金额，常规保留两位小数，记录一下处理方法及前端框架中的普遍用法。

___

　　小程序是基于腾讯官方 WePY 框架来实现的，但是由于小程序技术生态比较闭合，导致很多前端框架积累出的成果都没有实现。

　　filter 可以理解为管道加工处理，接收一组数据，经过各种不同类型的管道加工，产出新的数据，但是又不会影响原有数据，最终展示给用户。
<br><br>

### 一、现有前端框架的 filter

　　![](https://raw.githubusercontent.com/liuxy0551/liuxy0551.github.io.jekyll/master/images/posts/Vue_WePY_filter/3.png)
    
　　在后端同学没有返回适合显示的数据或者不方便处理数据时，可以在前端使用过滤器处理，上述对时间和金额进行处理，使用 `|` 作为管道符，传递参数进行序列化。
date 的过滤写法可参考 [date.js](https://github.com/liuxy0551/liuxy0551.github.io/blob/master/images/posts/Vue_WePY_filter/date.js) 。
   

### 二、小程序中过滤器的使用

　　![](https://raw.githubusercontent.com/liuxy0551/liuxy0551.github.io.jekyll/master/images/posts/Vue_WePY_filter/2.png)

　　![](https://raw.githubusercontent.com/liuxy0551/liuxy0551.github.io.jekyll/master/images/posts/Vue_WePY_filter/1.png)

　　上图是小程序对金额的处理效果（基于 WePY），可参考 [微信小程序 WXS 文档](https://developers.weixin.qq.com/miniprogram/dev/framework/view/wxs/index.html?search-key=wxs)。

　　在 template 中引入 [money.wxs](https://github.com/liuxy0551/liuxy0551.github.io/blob/master/images/posts/Vue_WePY_filter/money.wxs) 文件，并传入数据进行转换，页面代码可参考 [detail.wpy](https://github.com/liuxy0551/liuxy0551.github.io/blob/master/images/posts/Vue_WePY_filter/detail.wpy)

　　![](https://raw.githubusercontent.com/liuxy0551/liuxy0551.github.io.jekyll/master/images/posts/Vue_WePY_filter/4.png)

<br>

#### 以上
___
### Q&A

随笔有不妥的地方感谢留言指正，谢谢您！  
其他知识可上网查找资料，共同学习进步。  
在操作过程中或者随笔有问题的话欢迎在 [Vue 和 WePY 中过滤器写法](https://liuxy0551.github.io/2019/04/Vue_WePY_filter/) 里提问或指正，或者从 [关于我](https://liuxy0551.github.io/about/) 中可以找到我的联系方式。


<br>
转载请注明：[刘先玉的博客](https://liuxy0551.github.io/) » [Vue 和 WePY 中过滤器写法](https://liuxy0551.github.io/2019/04/Vue_WePY_filter/)
