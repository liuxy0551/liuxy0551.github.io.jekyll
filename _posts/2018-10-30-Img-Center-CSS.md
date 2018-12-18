---
layout: post
title: 图片大小不固定时在 div 中居中显示
date: 2018-10-30
tag: CSS
---

___
##### 　　公司的一个商城项目中，需要实现商品详情页顶部图片非正方形时补白且居中，尝试了很多方法，实现后发现其实很简单，记录一下。

___

### 一、实现效果

<center>
    <iframe width="500" height="400" src="/images/posts/Img-Center-CSS/3.mp4" allowfullscreen></iframe>
</center>
<br>

　　项目是移动端的项目，基于 Vue + Mint UI 实现。效果区域使用的是 Mint UI 自带的 swipe 组件，取消了自动播放。

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


#### 以上

___
### Q&A

随笔有不妥的地方感谢留言指正，谢谢您！  
其他知识可上网查找资料，共同学习进步。  
在操作过程中或者随笔有问题的话欢迎在 [图片大小不固定时在 div 中居中显示](https://liuxy0551.github.io/2018/10/Img-Center-CSS/) 里提问或指正，或者从 [关于我](https://liuxy0551.github.io/about/) 中可以找到我的联系方式。


<br>
转载请注明：[刘先玉的博客](https://liuxy0551.github.io/) » [图片大小不固定时在 div 中居中显示](https://liuxy0551.github.io/2018/10/Img-Center-CSS/)
