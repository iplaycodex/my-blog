---
title: 如何发布自己的第一个npm包
date: 2020-08-03 14:49:25
categories:
    - 前端工程化
tags:
    - 前端工程化
---

# 1. 前言

`npm`是什么这里不必再多说,我相信现在做前端的没有不知道的.这里就不在赘述了.
我们平时开发中肯定是有很多可复用的类库或者组件的,那么把他们抽离出来复用就很有必要了,可以大大减少我们的工作量.下面简单介绍一下如何把一个包发布到`npm`上

# 2. 工具

> 首先我们安装一下好用的工具

-   nvm
    -   管理`node`的版本的一个工具,如何安装和使用自行搜索
-   nrm
    -   可以方便的切换`npm`源的一个工具.因为在国内`npm`的官方源经常网络连接不稳当,使用`cnpm`又会出现一个莫名其妙的 bug.故这里强力建议使用该工具来管理`npm`的源.且这个工具可以配置自定义源地址,方便我们搭建自己的私有 npm

> 上述两个工具的使用这里不再赘述,自己搜搜

# 3. 初始化一个 npm 包

## 3.1. 创建一个示例包

```javascript
// step 1
cd yourDic
// step 2
mkdir myFirstNpmPackage
// step 3
cd myFristNpmPackage
// step 4
npm init
```

<!--more-->

## 3.2. npm init

```json
{
    "name": "myFristNpmPackage",
    "version": "1.0.0",
    "description": "",
    "main": "index.js",
    "scripts": {
        "test": "echo \"Error: no test specified\" && exit 1"
    },
    "keywords": [],
    "author": "",
    "license": "ISC"
}
```

入口文件是`index.js`,接下来我们再新建一个`index.js`

## 3.3. create index.js

```js
export default printHelloWorld = () => {
    console.log("hello world!");
};
```

RT

# 4. 注册 npm 账号

> 注册一个 npm 账号,不再赘述

# 5. 发布

上面那个最简单的项目,我们打算发布到`npm`上,进入项目目录:

## 5.1. 确认是否官方源

上面已经安装了`nrm`,一般我们在开发的时候会切到`taobao`源或者是自己搭建的私有源.但是发布的时候需要切换到官方源.

```javascript
// step 1: change to npm
nrm use npm

// step 2: 登录,输入账号密码即可
npm loing

// step 3: 查看包名是否被占用,如果没有被占用即可发布,如果被占用了则需要更换新的包名
npm search myFristNpmPackage

// step 4: 发布
npm publish
```

# 6. 完成发布

这样就完成了一个包的发布,其实也是很简单的

# 7. 如何使用

当你完成了包的发布后,后面就是如何使用这个包了,当然也很简单:

```javascript
// install myFristNpmPackage
npm i myFristNpmPackage --save
```

# 8. 结束语

这样就一个简单的`npm`包就发布完毕了,还是很简单的~
