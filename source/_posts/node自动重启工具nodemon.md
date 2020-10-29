---
title: node自动重启工具nodemon
date: 2019-11-07 15:50:48
categories:
    - node
tags:
    - node
---

> 作者：[iplaycodex](http://iplaycodex.com)
> 仓库：[github](https://github.com/iplaycodex)、[codePen](https://codepen.io/iplaycodex)
> 博客：[掘金](https://juejin.im/user/3597257774478359)、[segmentfault](https://segmentfault.com/u/iplaycodex)、[知乎](https://www.zhihu.com/people/CallMeAllenLliu)、[简书](https://www.jianshu.com/u/9cd27f169c7e)、[博客园](https://www.cnblogs.com/)
> 联系我：[iplaycodex@163.com](iplaycodex@163.com)
> 特别声明：原创不易，未经授权不得对此文章进行转载或抄袭，否则按侵权处理，如需转载或开通公众号白名单可联系我，尊重原创尊重知识产权从我做起

# 1. 问题

在开发`Node.js`的项目的时候,需要频繁的手动`close`掉,然后再重启,非常麻烦.经过百度以后发现了一个好用的工具:`nodemon`.它的作用是监听代码文件的变动,当代码改动了以后,自动重启.

# 2. 如何使用

打开终端,`win`平台使用命令行,输入以下指令完成安装.

```javascript
npm install -g nodemon
```

<!--more-->

创建一个`index.js`,开始写代码,如下所示:

```javascript
var express = require("express");

var app = express();

app.get("/", function (req, res) {
    res.send("hello express");
});

app.listen(3000, function () {
    console.log("server is running");
});
```

往常我们启动这个服务都是使用的是

```javascript
node index.js
```

安装了`nodemon`后就不用了,可以使用:

```javascript
nodemon index.js
```

启动.这个时候当我们修改以下源码就会看到`node`自动重启了.我们刷新一下浏览器,会发现内容已经更新了

# 3. 结束语

❤️ 关注 + 点赞 + 收藏 + 评论 + 转发 ❤️ <br/>原创不易，鼓励笔者创作更好的文章~
