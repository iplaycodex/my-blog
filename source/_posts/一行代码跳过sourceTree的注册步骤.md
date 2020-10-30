---
title: 一行代码跳过sourceTree的注册步骤
date: 2020-01-19 15:34:22
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

最近帮朋友装电脑,发现`sourceTree`得注册,很麻烦.遂找到如下解决方法:

<!--more-->

-   打开`sourcetree`
-   关闭 sourcetree
-   命令终端输入如下内容,然后运行:

```javascript
defaults write com.torusknot.SourceTreeNotMAS completedWelcomeWizardVersion 3
```

-   打开`sourceTree`即可跳过注册!

# 2. 结束语

❤️ 关注 + 点赞 + 收藏 + 评论 + 转发 ❤️ <br/>原创不易，鼓励笔者创作更好的文章~
