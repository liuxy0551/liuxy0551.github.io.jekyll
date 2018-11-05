---
layout: post
title: Vue 编程之路（二）——跳转页面传值
date: 2018-07-27
tag: Vue
---

___
##### 　　最近公司的一个项目中使用 Vue 2.0 + element UI 实现一个后台管理系统的前端部分，属于商城类型。其中我负责的部分有一项需要跳转页面，由于跳转前的页面是多个组件构成的，
##### 所以在跳转页面的时候，并不适合用传统的 href，于是使用路由进行传值。在这里分享一下开发的过程。

##### 　　如何引入路由，可查看官方文档：[https://router.vuejs.org/zh/installation.html](https://router.vuejs.org/zh/installation.html)，也可自行搜索。

___

### 一、我采用的实现方法

　　![](/images/posts/Transmit-Value/1.png)

　　上图，跳转前的页面。给每一行的按钮绑定点击事件，并将每一行的数据携带上。

　　![](/images/posts/Transmit-Value/5.png)

　　上图，按钮的点击事件。首先创建 props ，然后在 props 中创建对应的属性名，之后即可在 template 中使用接收到的对象。

　　![](/images/posts/Transmit-Value/3.png)

　　上图，跳转前的页面所对应的响应事件。其中 path 所对应的 '/order/orderDetails' 我已经在 src/router/index.js 中注册声明，如下图：

　　![](/images/posts/Transmit-Value/4.png)

　　上图，在 src/router/index.js 中注册声明。

　　点击“订单详情”按钮后，页面跳转，此时的 URL 为：

　　![](/images/posts/Transmit-Value/2.png)

　　![](/images/posts/Transmit-Value/6.png)

　　上图，接收页接收数据。此时刷新页面，数据依然存在，因为 URL 没有改变，接收页直接从 URL 截取参数去接口中拿数据，故刷新页面不会影响接收页的数据。可以看到，这边是把需要的参数写入 URL 了，然后在接收页接收数据：


### 二、介绍一下先前采用的方法

　　拿着整个订单对象用路由传，实际上能传成功，但是会在刷新页面后拿不到数据，观察 URL 发现显示的是 Object ，可能是刷新后解析问题导致拿不到数据。
  
　　具体的采用可参照官方文档：[https://router.vuejs.org/zh/guide/essentials/navigation.html](https://router.vuejs.org/zh/guide/essentials/navigation.html)，我当时也是照着文档写的，获取参数可以用 this.$route.query。


### 三、其他方法

　　其实跳转页面传值的方法有很多，就我所听过的就还有以下方法，不过我没有实验过，有兴趣的可以自行尝试：
  
#### 1、使用 router-link 也会在刷新页面后丢失数据

    <router-link :to="{ name: 'user', params: { userId: 123 }}">User</router-link>

#### 2、通过 parent, children 等方法调取用层级关系的组件内的数据和方法
    
　　通过下面的方法调用，虽然用起来比较灵活，但是容易造成代码耦合性高，导致后期维护困难。

    this.$parent.$data.id       // 获取父元素data中的id
    this.$children.$data.id     // 获取父元素data中的id

#### 3、通过 eventBus 传递数据

　　使用前可以在全局定义一个 eventBus

    window.eventBus = new Vue();
    
    
　　在需要传递参数的组件中，定义一个 emit 发送需要传递的值，键名可以自己定义（可以为对象）
    
    eventBus.$emit('eventBusName', id);
    
    
　　在需要接受参数的组件重，用 on 接受该值（或对象）
    
    eventBus.$on('eventBusName', function(val) {
        console.log(val)
    });
    
　　最后记住要在 beforeDestroy() 中关闭这个 eventBus
    
    eventBus.$off('eventBusName');
　　
#### 4、借道 sessionStorage / localStorage

　　localStorage与sessionStorage存储的必需是字符串，而获取的交互数据是Object，所以我们一般要把JSON格式的字符串转成字符。

    JSON.stringify();  // 将Json对象转为字符串。
    JSON.parse();      // 将字符串转为json格式。
 

___
### Q&A

随笔有不妥的地方感谢留言指正，谢谢您！  
其他知识可上网查找资料，共同学习进步。  
在操作过程中或者随笔有问题的话欢迎在 [Vue 编程之路（二）——跳转页面传值](https://liuxy0551.github.io/2018/07/Transmit-Value/) 里提问或指正，或者从 [关于我](https://liuxy0551.github.io/about/) 中可以找到我的联系方式。


<br>
转载请注明：[刘先玉的博客](https://liuxy0551.github.io/) » [Vue 编程之路（二）——跳转页面传值](https://liuxy0551.github.io/2018/07/Transmit-Value/)
