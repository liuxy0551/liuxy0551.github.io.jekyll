---
layout: post
title: Vue 中实现验证码倒计时功能
date: 2018-08-19
tag: Vue
---

___
##### 　　公司项目中有根据手机号获取验证码的环节，倒计时的实现还是比较有趣的，记录一下。

___

### 实现效果

![](https://raw.githubusercontent.com/liuxy0551/liuxy0551.github.io.jekyll/master/images/posts/Vue_Countdown/1.gif)


### 具体实现

#### 1、HTML 部分

![](https://raw.githubusercontent.com/liuxy0551/liuxy0551.github.io.jekyll/master/images/posts/Vue_Countdown/2.png)

    <li>
      <div>
        <span>手机号</span>
      </div>
      <div>
        <input type="text" class="m-edit-input" v-model="ustelphone">
      </div>
    </li>
    <li>
      <div>
        <span>验证码</span>
      </div>
      <div>
        <input type="text" class="m-edit-input-s" v-model="identifyingcode" maxlength="6">
        <span class="m-get-code active" v-if="!getCode" @click="getInforcode">获取验证码</span>
        <span class="m-get-code" v-if="getCode">{{ count }} 秒后再次获取</span>
      </div>
    </li>

#### 2、JS 部分

![](https://raw.githubusercontent.com/liuxy0551/liuxy0551.github.io.jekyll/master/images/posts/Vue_Countdown/3.png)

    data() {
      return {
        getCode: false,               // 是否已获取验证码
        ustelphone: '',               // 手机号码
        timer: null,                  // 倒计时
        count: ""                     // 倒计时
      }
    }

![](https://raw.githubusercontent.com/liuxy0551/liuxy0551.github.io.jekyll/master/images/posts/Vue_Countdown/4.png)

      // 获取验证码
      getInforcode() {
        if(!this.ustelphone){
          Toast("请先输入手机号码");
          return false;
        }
        // 倒计时60秒
        const TIME_COUNT = 10;
        if (!this.timer) {
          this.count = TIME_COUNT;
          this.getCode = true;
          this.timer = setInterval(() => {
            if (this.count > 0 && this.count <= TIME_COUNT) {
              this.count --;
            } else {
              this.getCode = false;
              clearInterval(this.timer);
              this.timer = null;
            }
          }, 1000);
        }
        axios.get(api.get_inforcode + "?ustelphone=" + this.ustelphone).then(res => {
          Toast(res.data.message);
        });
      }
      
#### 3、CSS 部分

![](https://raw.githubusercontent.com/liuxy0551/liuxy0551.github.io.jekyll/master/images/posts/Vue_Countdown/5.png)

    .m-get-code{
      display: inline-block;
      padding: 4px 15px;
      border-radius: 10px;
      background-color: #CCCCCC;
      color: #fff;
      box-shadow:0 3px 6px rgba(0,0,0,0.16);
      font-size: 21px;
      line-height: 40px;
      &.active{
        background-color: @mainColor;
      }
    }


#### 以上

___
### Q&A

随笔有不妥的地方感谢留言指正，谢谢您！  
其他知识可上网查找资料，共同学习进步。  
在操作过程中或者随笔有问题的话欢迎在 [Vue 中实现验证码倒计时功能](https://liuxy0551.github.io/2018/08/Vue_Countdown/) 里提问或指正，或者从 [关于我](https://liuxy0551.github.io/about/) 中可以找到我的联系方式。


<br>
转载请注明：[刘先玉的博客](https://liuxy0551.github.io/) » [Vue 中实现验证码倒计时功能](https://liuxy0551.github.io/2018/08/Vue_Countdown/)
