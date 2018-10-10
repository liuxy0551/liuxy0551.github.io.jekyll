---
layout: post
title: Vue 生命周期
date: 2018-09-25
tag: Vue
---

___
##### 　　我在学习 Vue 的时候，经常会接触到 Vue 的生命周期函数，常见的为 created 和 mounted，所以记录一下每个 Vue 实例在被创建之前都要经过的一系列初始化过程，例如，需要设置数据监听、编译

##### 模板、将实例挂载到 DOM 并在数据变化时更新 DOM 等。同时在这个过程中也会运行一些叫做生命周期钩子的函数，这个过程便是 Vue 的生命周期。

<br>

### 一、生命周期图示

　　![](/images/posts/Vue-Life-Cycle/lifecycle.png)

　　上图展示了 Vue 实例的生命周期，这是[官网上的原图](https://cn.vuejs.org/images/lifecycle.png)，我在学习的时候也没有一下就弄懂这张图说的所有东西，但是随着 Vue 学习的深入，对这张图的兴趣越来越浓。可以看出，在 Vue 生命

周期中有很多钩子函数提供给我们在 Vue 生命周期不同时刻进行操作。我们先在图上确认所有的生命周期函数，然后再依次理解。


>* beforeCreate、created　　　　　　　　　　创建前后
>* beforeMount、mounted　　　　　　　　　挂载前后
>* beforeUpdate、updated　　　　　　　　　数据更新前后
>* beforeDestroy、destroyed　　　　　　　　 页面销毁前后


<br>
### 二、想象中的导出、导入数据文件

#### 以下为缺少表空间的错误：

1、在原先正常的电脑上使用 PL SQL 12 导出 32 个表，为 .dmp 格式文件，并在新电脑进行导入表的操作  
2、弹出一个窗口后秒关，尝试通过截图快捷键截图查看，以失败告终，请教项目组上的数据库老师后知道了这是缺少表空间的缘故，之后   就是各种恶补表空间知识。  
3、在 PLSQL 中新建 SQL 窗口，键入以下语句并执行：

    CREATE TABLESPACE OP
    LOGGING
    DATAFILE 'D:\Oracle\product\11.2.0\OP.DBF'
    SIZE 50M
    AUTOEXTEND ON
    NEXT 32M MAXSIZE UNLIMITED
    EXTENT MANAGEMENT LOCAL;

　　其中第三行语句含有表空间的存放位置，建议放在 Oracle 的安装目录里面，防止误删除。OP 为表空间名字，其他行语句想了解的可自行百度具体含义。删除已经使用的表空间会使得对应的用户无法登录使用，我是重装 Oracle 解决的，就是这么低技术含量，幸好是没有什么重要数据。可以删除表空间后再删除这个 .DBF 文件，删除语句如下：

    DROP TABLESPACE OP;

### 三、解决空表不导出的方法

1、在数据导出的时候，无法导出空表，提示错误“EXP-00011：table 不存在”。
产生原因：Oracle 11g 默认创建一个表时不分配 segment，只有在插入数据时才会产生（当然也可以强制分配），以节省磁盘空间。

2、解决方法：  
　　(1)第一种：在空表中插入一条数据然后再对插入的数据进行删除，便可以进行数据导出（我的那几个表添加假数据很难，如果表少的话可以手动执行，对于多个表的情况可以采用语句进行批量操作的）。  
　　(2)第二种：可以使用手工为空表分配 Extent 的方式，来解决导出之前建立的空表的问题。在 PLSQL 中新建 SQL 窗口，键入以下语句并执行：

    SELECT 'ALTER TABLE '||TABLE_NAME||' ALLOCATE EXTENT;' FROM USER_TABLES WHERE SEGMENT_CREATED='NO';

![](/images/posts/Oracle-PLSQL/result.png)<br>

可以通过语句导出查询结果，执行导出的语句即可（表数量少的话可以复制粘贴执行查询结果）。

<br>![](/images/posts/Oracle-PLSQL/yuju.png)

    set heading off;
    set echo off;
    set feedback off;
    set termout on;
    spool D:\Oracle\product\11.2.0\allocate.sql;
    SELECT 'ALTER TABLE '||TABLE_NAME||' ALLOCATE EXTENT;' FROM USER_TABLES WHERE SEGMENT_CREATED='NO';
    spool off;


导出后执行导出的语句：

    @ D:\Oracle\product\11.2.0\allocate.sql;

　　(3)第三种：设置deferred_segment_creation 参数，该参数值默认是TRUE，当改为FALSE时，无论是空表还是非空表，都分配segment。
    （这种方法我没有试过，你可以自行尝试）

    <br>

    SELECT 'ALTER TABLE '||TABLE_NAME||' ALLOCATE EXTENT;' FROM USER_TABLES WHERE NUM_ROWS=0;

>* 实测上面百度到的这句指令不显示空表结果，你可以自己试一试。
>* 下面这个语句可在 TNS 连接不上时导入表：

    imp scott/tiger@localhost:1521/orcl full=y  file= E:\my.dmp ignore=y;

___
### Q&A

随笔有不妥的地方感谢留言指正，谢谢您！  
其他知识可上网查找资料，共同学习进步。  
在操作过程中或者随笔有问题的话欢迎在[Vue 生命周期](https://liuxy0551.github.io/2018/09/Vue-Life-Cycle/) 里提问或指正。

>* 1、写这篇随笔的时候发现在 Atom 中选中单词，按住 Ctrl 后按 K， 再按 U，即可将选中的单词大写
>* 2、白天的技巧：Eclipse 中查看方法在哪里被调用了——选中方法，直接Ctrl+Shift+G或者Ctrl+Alt+H

<br>
转载请注明：[刘先玉的博客](https://liuxy0551.github.io/) » [Vue 生命周期](https://liuxy0551.github.io/2018/09/Vue-Life-Cycle/)
