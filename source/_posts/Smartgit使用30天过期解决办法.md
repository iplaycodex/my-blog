---
title: Smartgit使用30天过期解决办法
date: 2019-10-11 14:36:45
tags:
    - Git
categories:
    - Git
---

> 作者：[iplaycodex](http://iplaycodex.com)
> 仓库：[github](https://github.com/iplaycodex)、[codePen](https://codepen.io/iplaycodex)
> 博客：[掘金](https://juejin.im/user/3597257774478359)、[segmentfault](https://segmentfault.com/u/iplaycodex)、[知乎](https://www.zhihu.com/people/CallMeAllenLliu)、[简书](https://www.jianshu.com/u/9cd27f169c7e)、[博客园](https://www.cnblogs.com/)、[leetcode](https://leetcode-cn.com/u/iplaycodex/)
> 公众号：[FEZONE](http://iplaycodex.com)
> 联系我：[iplaycodex@163.com](iplaycodex@163.com)
> 特别声明：原创不易，未经授权不得对此文章进行转载或抄袭，否则按侵权处理，如需转载或开通公众号白名单可联系我，尊重原创尊重知识产权从我做起

# 1. 前言

`smartGit`是一款`git`比较好用的 GUI 工具.未注册版本提供 30 天的试用期,提供一个过期了以后还可以使用的方法:

-   1.打开`Finder`
-   2.使用快捷键 `command + shift + G`
-   3.复制 `~/Library/Preferences/SmartGit/` 到输入框
-   4.点击确定调转到指定的文件夹删除 settings.xml 文件

至此,即可在 30 天的试用期到了以后继续使用了.当然最后还是要说一句,如果有条件,请支持正版.

---

提醒:最近`smartGit`有更新,发现本方法仅对版本低于:`18.2.9 #13269`有效.高版本暂不支持

---

安装完毕后我们修改 `smGit` 检查更新的请求 host 到本地,避免不停的提醒更新,烦的要死.`host` 文件添加如下代码:

```bash
127.0.0.1 www.syntevo.com
```

就酱,很简单

# 2. 结束语

❤️ 关注 + 点赞 + 收藏 + 评论 + 转发 ❤️ <br/>原创不易，鼓励笔者创作更好的文章~
