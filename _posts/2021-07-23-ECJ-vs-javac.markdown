---
layout: post
title: "ECJ vs javac"
date: 2021-07-23 14:04:02 +0800
categories: ["java"]
tags: ["tools"]
---


这是`Eclipse`基金会推出的一款`Java`编译器，相比于早期`Java`自带的编译器其有以下三个有点：

1. 支持多线程编译

2. 支持增量编译

3. 编译的过程中遇到错误也不会停止编译，而是会把所有编译中遇到的错误都展示出来




会了解这个的原因是当时入职了一家公司，那家公司全部员工用的都是`Eclipse`而我比较喜欢`Intellij`，但是有一次我写完代码准备跑一下测试一下，傻眼了我从当天晚上编译到第二天早点还没编译好整个项目，而其他用`Eclipse`的同事写完立马就能测试了，不对劲呀，为什么，打开任务管理器一看一个线程在那玩命的编译，其他线程动都不动一下，看下其他同事的，人家都是所有线程一起编译，编译的贼快。

这肯定不能忍啊，立马回来一顿搜索，原来`ECJ`是`Eclipse`默认的编译器，所以当时的`Eclipse`编译速度很快。而`Intellij`默认用的是`javac`，这玩意是单线程的所以我的代码编译的贼慢，好在`Intellij`支持`ECJ`，后来我切换成`ECJ`好家伙，编译速度立马就提上来了，我也能写完代码就立即测试了，然后我的印象中就一直留下了`javac`垃圾的印象。



后来又入职了一家新公司，我一直记得`javac`垃圾的印象，但当时忙着熟悉项目，没有时间调试`IDE`，等过了一段时间之后，我就开始着手优化`Intellij`，第一件事就是把垃圾的`javac`换成`ECJ`，但是项目中用了`lombok`，在那搞了好半天，又是加参数，又是升级`lombok`，搞了大半天，搞好之后编译一看，我的天啊，怎么和没换之前的编译时间差不多。之后又用`javac`和`ECJ`分别测试了编译和重新编译了好几次，对比了一下两者相差时间没啥差别啊。立马跑官网上看了一下现在官网上对`ECJ`的描述是相对与`javac`他可以遇到编译错误的时候继续编译下去，这不对啊，和我印象不一样啊，立马又是上网一顿搜，但是都是在说`javac`是单线程的，或者只说`ECJ`可以遇到编译错误继续下去。搜寻无果放弃了。



后来又过了好几星期在网上逛着逛着就看到了一个大佬说`javac`提高了编译速度也支持了增量编译[`JEP139`](http://openjdk.java.net/jeps/139)，原来`jdk8`之后`javac`也支持多线程和增量编译了，只是遇到编译错误之后不再继续编译下去了。我还到处跟别人说`javac`垃圾，丢人啊。网上那些评论也是害人啊，人云亦云都不深入了解一下。

