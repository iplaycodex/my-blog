---
title: npm ERR! publish Failed PUT 403
date: 2019-11-02 13:33:25
categories:
    - 前端
tags:
    - 前端
---
## 问题
最近遇到的一个问题,最近在`npm`发布了一个包.使用命令`npm publish`之后发生了如下错误:
```javascript
npm ERR! code E403
npm ERR! 403 Forbidden - PUT https://registry.npm.taobao.org/kda-cli - [no_perms] Private mode enable, only admin can publish this module

npm ERR! A complete log of this run can be found in:
npm ERR! /Users/allenliu/.npm/_logs/2019-11-02T05_52_32_439Z-debug.log
```
出现这个问题呢,一般都是因为修改了`npm`的`源`.我们可以在很多文档上看到因为国内的网络问题,很多时候文档上都建议修改`npm`的源为`taobao`源.

## 解决方法如下所示:
##### 1.查看npm是否被设置成了taobao源,打开终端,输入:
```html
npm config get registry
```
这个时候会如下显示:(如果非淘宝源头也就不会出现上述问题了)
```html
https://registry.npm.taobao.org/
```
<!--more-->
##### 2.设置为官方源
同样,打开终端输入以下指令:
```html
npm config set registry=http://registry.npmjs.org
```
##### 3.登录`npm`账户(如果没有登录),再次发布
```javascript
// step 1
npm login 或者添加用户 npm adduser

// step 2
npm publish
```
##### 4.发布成功之后根据需求再次将源设置为`taobao`镜像
```html
npm config set registry=https://registry.npm.taobao.org/
```
*PS:不建议设置为淘宝源,建议找一个稳定的VPN.或者推荐安装`yarn`.cnpm在安装依赖包的时候会经常发生一些莫名其妙的问题*