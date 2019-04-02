---
layout: post
title: Element UI 日期选择器时间选择范围限制
date: 2019-04-02
tag: Element UI、DatePicker
---

___
##### 　　最近后台管理系统中的项目遇到了选择时间时需要加以限制的问题，记录一下。

___

　　DatePicker 组件代码：

    <el-date-picker
            v-model="time"
            type="date"
            placeholder="选择日期"
            :picker-options="pickerOptions">
    </el-date-picker>

### 一、选择今天及今天以后的日期

![](/images/posts/Element-UI-DatePicker/1.png)

    data() {
      return {
        time: '',
        pickerOptions: {
          disabledDate(time) {
            return time.getTime() < Date.now() - 8.64e7;
          }
        }
      }
    }


### 二、选择今天及今天以前的日期

![](/images/posts/Element-UI-DatePicker/2.png)

    data() {
      return {
        time: '',
        pickerOptions: {
          disabledDate(time) {
            return time.getTime() > Date.now() - 8.64e6
          }
        }
      }
    }


### 三、选择今天以后的日期（不含今天）

![](/images/posts/Element-UI-DatePicker/3.png)

    data() {
      return {
        time: '',
        pickerOptions: {
          disabledDate(time) {
            return time.getTime() < Date.now();
          }
        }
      }
    }


### 四、选择三个月之前到今天的日期

![](/images/posts/Element-UI-DatePicker/4_1.png)
![](/images/posts/Element-UI-DatePicker/4_2.png)

    data() {
      return {
        time: '',
        pickerOptions: {
          disabledDate(time) {
            let curDate = (new Date()).getTime();
            let three = 90 * 24 * 3600 * 1000;
            let threeMonths = curDate - three;
            return time.getTime() > Date.now() || time.getTime() < threeMonths;
          }
        }
      }
    }



#### 以上
___
### Q&A

随笔有不妥的地方感谢留言指正，谢谢您！  
其他知识可上网查找资料，共同学习进步。  
在操作过程中或者随笔有问题的话欢迎在 [Element UI 日期选择器时间选择范围限制](https://liuxy0551.github.io/2019/04/Element-UI-DatePicker/) 里提问或指正，或者从 [关于我](https://liuxy0551.github.io/about/) 中可以找到我的联系方式。


<br>
转载请注明：[刘先玉的博客](https://liuxy0551.github.io/) » [Element UI 日期选择器时间选择范围限制](https://liuxy0551.github.io/2019/04/Element-UI-DatePicker/)
