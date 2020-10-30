---
title: "react-native在安卓手机运行起来一片空白,为何?"
date: 2019-07-22 18:04:45
categories:
    - react-native
tags:
    - react-native
---

> 作者：[iplaycodex](http://iplaycodex.com)
> 仓库：[github](https://github.com/iplaycodex)、[codePen](https://codepen.io/iplaycodex)
> 博客：[掘金](https://juejin.im/user/3597257774478359)、[segmentfault](https://segmentfault.com/u/iplaycodex)、[知乎](https://www.zhihu.com/people/CallMeAllenLliu)、[简书](https://www.jianshu.com/u/9cd27f169c7e)、[博客园](https://www.cnblogs.com/)、[leetcode](https://leetcode-cn.com/u/iplaycodex/)
> 公众号：[FEZONE](http://iplaycodex.com)
> 联系我：[iplaycodex@163.com](iplaycodex@163.com)
> 特别声明：原创不易，未经授权不得对此文章进行转载或抄袭，否则按侵权处理，如需转载或开通公众号白名单可联系我，尊重原创尊重知识产权从我做起

# 1. 问题

今天在搭`react-native`的`android`开发环境,`JDK`,`android-studio`等一堆东西配好了以后.`android-studio`连上我的大华为手机,本地的`rn`服务已经成功启动.然后打开 APP 以后,进入`rn`调试页面,`WTF???`一片空白...

看了下`终端`是没有任何报错的,`android-studio`也是编译通过了,没有任何报错,为啥一片空白?

关掉真机,启动卡如狗的安卓模拟器,发现在模拟器里是可以正常展示的.那么问题来了?为啥模拟器可以真机不行?真机哪里出现了问题?

经过`google`,`stack-overflow`多方查阅后知道,解决方案如下所示:

-   设置 -> APP -> 权限管理 -> 悬浮框权限(开启)
-   手机需要和电脑在一个`WIFI`网络下,或者挂`代理`

真是一个坑啊,至此:`react-native`的项目应该在`安卓真机`上可以正常的显示了.

---

2019/07/24 补充:

今天下午开会提到了这个问题,如果生产环境还是这样那岂不是炸了,用户是不可能会主动打开`悬浮窗`的权限的.后来安卓小伙伴补充到:原来这个问题只会在`dev`环境中出现,等上生产环境了以后,直接加载`bundle`包是不会有这个问题的.Thank godness!

# 2. 结束语

❤️ 关注 + 点赞 + 收藏 + 评论 + 转发 ❤️ <br/>原创不易，鼓励笔者创作更好的文章~

<!--more-->
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
      id: 'react-native-r24e',
        });
      gitalk.render('gitalk-container');
</script>
