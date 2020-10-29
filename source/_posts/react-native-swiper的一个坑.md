---
title: react-native-swiper的一个坑
date: 2019-07-25 16:34:28
tags:
    - react-native
categories:
    - react-native
---

> 作者：[iplaycodex](http://iplaycodex.com)
> 仓库：[github](https://github.com/iplaycodex)、[codePen](https://codepen.io/iplaycodex)
> 博客：[掘金](https://juejin.im/user/3597257774478359)、[segmentfault](https://segmentfault.com/u/iplaycodex)、[知乎](https://www.zhihu.com/people/CallMeAllenLliu)、[简书](https://www.jianshu.com/u/9cd27f169c7e)、[博客园](https://www.cnblogs.com/)
> 联系我：[iplaycodex@163.com](iplaycodex@163.com)
> 特别声明：原创不易，未经授权不得对此文章进行转载或抄袭，否则按侵权处理，如需转载或开通公众号白名单可联系我，尊重原创尊重知识产权从我做起

# 1. 问题

项目有个需求是轮播,纵向滚动.遂在`github`上找到了一个`star`比较多的插件:`react-native-swiper`.接入的也是很方便的,美滋滋.然后想目跑起来,xcode 开起来,没毛病,挺好.

继续打开项目,在`android`环境下跑一跑,没想到出问题了,纵向滚动不生效.

遂上`github`看`issues`发现很多人都遇到了这个问题,这个组件纵向滚动的时候在`iOS`平台是没有问题的,但是在`安卓`下面都遇到这个问题,不能纵向滚动,只能横向滚动!

继续查看资料发现是`react-native-swiper - 1.5.14`版本存在的这个问题.解决这个问题需要切换到`react-native-swiper - 1.5.13`即可解决,或者使用另外一个库:`@nart/react-native-swiper`.这个库其实是基于`react-native-swiper - 1.5.13`的,使用这个库即可解决这个问题.

```javascript
// step 1,安装
npm i @nart/react-native-swiper --save

// step 2,在代码中引用
import Swiper from '@nart/react-native-swiper';
```

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
      id: 'react-native-r21g',
        });
      gitalk.render('gitalk-container');
</script>
