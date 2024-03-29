---
title: wx2bat工具分享
date: 2019-12-22 08:31:04
tags:
    - 前端工程化
categories:
    - 前端工程化
---

> 作者：[iplaycodex](http://iplaycodex.com)
> 仓库：[github](https://github.com/iplaycodex)、[codePen](https://codepen.io/iplaycodex)
> 博客：[掘金](https://juejin.im/user/3597257774478359)、[segmentfault](https://segmentfault.com/u/iplaycodex)、[知乎](https://www.zhihu.com/people/CallMeAllenLliu)、[简书](https://www.jianshu.com/u/9cd27f169c7e)、[博客园](https://www.cnblogs.com/)、[leetcode](https://leetcode-cn.com/u/iplaycodex/)
> 公众号：[FEZONE](http://iplaycodex.com)
> 联系我：[iplaycodex@163.com](iplaycodex@163.com)
> 特别声明：原创不易，未经授权不得对此文章进行转载或抄袭，否则按侵权处理，如需转载或开通公众号白名单可联系我，尊重原创尊重知识产权从我做起

# 1. 前言

最近在公司接到了一个需求:`把一个微信小程序快速变成字节跳动小程序`,开发时间只有一个星期!显然从 0 开始开发字节跳动的小程序是不可能的.所以只能想办法看如何快速的把`微信小程序`转为`字节跳动小程序`~

# 2. 解决之道

经过查询得知,其他家的小程序的`api`和微信几乎`90%`一样,只是可能文件后缀换了自己的后缀.还有一些语法也变了:例如:

```javascript
// wechatApp
wx:if

// 头条
tt:if

// 百度
swan:if
```

<!--more-->

这样的话就比较简单了,我们只需要写一个工具把哪些差异性的东西修改一下就可以了.经过半天的辛苦编码:`wx2bat`工具写完了,支持将`微信小程序`源码快速转为`百度小程序`,`支付宝小程序`以及`头条小程序`.并已经发布到了`npm`上面

# 3. 如何使用?

step 1:

```javascript
npm i -g wx2bat
```

step 2:

```javascript
wx2bat <wechatAppPath> <outputPath> <platform>
```

通过上面一行命令即可将`微信小程序`的源码转为`目标小程序的源码`.然后需要修改一下特定平台的差异性代码即可.例如:`授权登录`,`支付`,`分享`...

# 4. 相关链接

[wx2bat](https://www.npmjs.com/package/wx2bat)

# 5. 结束语

❤️ 关注 + 点赞 + 收藏 + 评论 + 转发 ❤️ <br/>原创不易，鼓励笔者创作更好的文章~
