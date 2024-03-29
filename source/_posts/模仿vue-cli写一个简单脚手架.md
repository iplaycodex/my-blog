---
title: 模仿vue-cli写一个简单脚手架
date: 2019-11-04 14:54:59
categories:
    - 前端工程化
tags:
    - 前端工程化
---

> 作者：[iplaycodex](http://iplaycodex.com)
> 仓库：[github](https://github.com/iplaycodex)、[codePen](https://codepen.io/iplaycodex)
> 博客：[掘金](https://juejin.im/user/3597257774478359)、[segmentfault](https://segmentfault.com/u/iplaycodex)、[知乎](https://www.zhihu.com/people/CallMeAllenLliu)、[简书](https://www.jianshu.com/u/9cd27f169c7e)、[博客园](https://www.cnblogs.com/)、[leetcode](https://leetcode-cn.com/u/iplaycodex/)
> 公众号：[FEZONE](http://iplaycodex.com)
> 联系我：[iplaycodex@163.com](iplaycodex@163.com)
> 特别声明：原创不易，未经授权不得对此文章进行转载或抄袭，否则按侵权处理，如需转载或开通公众号白名单可联系我，尊重原创尊重知识产权从我做起

# 1. 前言

我的朋友们,你是否遇到过下面的这种情况.每当要开始做新项目的时候(此文档仅针对`vue`,后续会继续扩展),每次都需要使用`vue-cli`去初始化一个项目:

```javascript
// init your project by vue-cli with webpack template
vue init webpack yourProject
```

一顿操作猛如虎生成了一个基于`webpack`的项目.BUT 距离开箱即用还是有一点距离.如果你的项目是个移动端的项目,那么针对移动端又需要安装大量的插件,第三方库.包括不限于如下所示:

-   `fastclick`
-   `babel-polyfill`
-   `reset.css`
-   `border.css`
-   `rem.js`
-   `flexable.js`
-   `axios`
-   `qs`
-   ...

一遍一遍,真的是烦的要死.而且现在是一个强调`工程化`的时代,任何可以交给程序的东西都交给程序自动化的去做.而且每次这样做也不利于项目的一致性,规范性.如果你是一个团队`owner`,如何统一化开发流程,如何解决这个问题.则迫在眉睫.

既然产生了问题,那么就要解决问题.

# 2. 思路

<!--more-->

前面的文章本人已经分享了自己编写的`HTML开发规范`,`CSS开发规范`以及`Javascript`开发规范.通过`code-review`来规范`HTML`和`CSS`的开发,通过`eslint`来规范`javascript`的开发.

> 通过`eslint`来规范`js`的开发,本人会在这个集合中再写一篇专门介绍如何使用`eslint`来规范`js`的开发.

## 2.1. 模板

既然`vue-cli`官方提供的模板不满足我们的需求(`vue inint webpack project`其实就是下载一个`webpack`的模板),那么我们就自定义一个满足自己项目需求的模板.在这个模板中配置好上述的所有`插件`,`第三方库`,`工具类`,`布局组件`,`ui库`,`eslint`,`webpack`配置等等...

做到真正的开箱即用,满足我们项目的使用.

## 2.2. cli

...未完,待续..

# 3. 结束语

❤️ 关注 + 点赞 + 收藏 + 评论 + 转发 ❤️ <br/>原创不易，鼓励笔者创作更好的文章~
