---
title: 如何解决iOS模拟器卡顿?
date: 2019-07-08 16:57:40
categories:
    - iOS
tags:
    - iOS
---

> 作者：[iplaycodex](http://iplaycodex.com)
> 仓库：[github](https://github.com/iplaycodex)、[codePen](https://codepen.io/iplaycodex)
> 博客：[掘金](https://juejin.im/user/3597257774478359)、[segmentfault](https://segmentfault.com/u/iplaycodex)、[知乎](https://www.zhihu.com/people/CallMeAllenLliu)、[简书](https://www.jianshu.com/u/9cd27f169c7e)、[博客园](https://www.cnblogs.com/)
> 联系我：[iplaycodex@163.com](iplaycodex@163.com)
> 特别声明：原创不易，未经授权不得对此文章进行转载或抄袭，否则按侵权处理，如需转载或开通公众号白名单可联系我，尊重原创尊重知识产权从我做起

# 1. 前言

自从升级到 macSierra 10.12 之后，在模拟器上面滑动视图很卡。后面就一直用的真机调试。但是有的时候跑一些小 demo 还是模拟器比较方便。所以就百度了一下怎么解决模拟器卡顿的问题.

1、看到网上有一个解决方法 在终端里面输入 sudo sysctl -w kern.timer.coalescing_enabled=0 然后就不卡了,这是一个解决方法，第一次是很好用的，但是后面过了一段时间，模拟器又重新变得很缓慢卡顿。

2、第二种解决方法就是查看模拟器菜单栏的 Debug 选项卡，查看 Slow Animations 选项是否被选中，去掉勾，在运行模拟器以后就 OK 了，模拟器操作变得很顺畅.搞不明白苹果为什么要这样设计,建议直接使用第二种就可以了

<!--more-->

# 2. 结束语

❤️ 关注 + 点赞 + 收藏 + 评论 + 转发 ❤️ <br/>原创不易，鼓励笔者创作更好的文章~

<link rel="stylesheet" href="https://unpkg.com/gitalk/dist/gitalk.css">
<script src="https://unpkg.com/gitalk@latest/dist/gitalk.min.js"></script>

<div id="gitalk-container"></div>     
<script type="text/javascript">
    var gitalk = new Gitalk({
    // gitalk的主要参数
      clientID: `e4890482436f9cd96039`,
      clientSecret: `0425bf39d0c5cdedf4ae60a72fbd7a3d58d7d99e`,
      repo: `codeCheeseIssues`,
      owner: 'wawsc5354524',
      admin: ['wawsc5354524'],
      id: 'ios-r10n',
        });
      gitalk.render('gitalk-container');
</script>
