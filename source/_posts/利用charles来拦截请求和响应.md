---
title: 利用charles来拦截请求和响应
date: 2019-11-12 17:41:11
categories:
    - 调试
tags:
    - 调试
---
今天简单分享一下如何使用`charles`来进行`HTTP`的拦截和修改.
>`charles`是一款非常好用的`http`调试工具,相信做开发的同学们应该都知道
其实使用`charles`来做`HTTP`拦截很简单.
### 1.拦截请求
打开`charles`,在输入框中输入要拦截的`API`地址:
![](https://tva1.sinaimg.cn/large/006y8mN6gy1g8vef97dmqj30xt0azmym.jpg)
在`API`上鼠标右键选择`breakPoint`即可打个断点.然后重新请求的时候这个`HTTP`就会被拦截,如下所示:
<!--more-->
![](https://tva1.sinaimg.cn/large/006y8mN6gy1g8veioukh0j30p40g4q4w.jpg)
切到`Edit Request`tab即可修改`request`的入参,如下图所示:
![](https://tva1.sinaimg.cn/large/006y8mN6gy1g8veka0nx8j30p90g9wg4.jpg)
### 2.拦截响应
![](https://tva1.sinaimg.cn/large/006y8mN6gy1g8vermrajlj30qw0i776l.jpg)
修改返回的数据:
![](https://tva1.sinaimg.cn/large/006y8mN6gy1g8vete06koj30r00i8acb.jpg)
其实也是很简单的操作,这里写出来分享给不知道的同学.
***
>PS:修改`请求`或者`响应`的时候要快一点,否则容易失败!切记!