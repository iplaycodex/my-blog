---
title: 修改react-native组件的默认属性
date: 2019-08-08 17:08:17
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

我们在做网页开发的时候知道标签有自己的默认样式,例如`<ul/>`,`<li/>`等等.所以一般我们在开发项目的时候首先要做的就是先把标签的默认样式给清除掉.在开发 RN 的时候发现有些组件的默认属性很烦人.同样的需要重写这些默认属性.例如:

```html
<Text /> <TextInput />
```

这两个组件的`allowFontScaling=true`即:属性默认跟随系统字体大小,超级坑爹.

还有这个组件:

```html
<TouchableOpacity />
```

这个组件默认点击的时候会有一个阴影效果,因为它的默认透明度是`0.2`.

这些默认属性有时候会给我们带来很大的困扰,有些组件的属性默认值并不是我们想要的.那么该怎么做呢?在每次使用这个组件的时候手动修改该组件的属性值?

这样做可以满足需求,但是太蠢了.每次使用上述组件的时候都要修改某些属性值.太蠢.这个方法舍弃.

# 2. 解决之道:

<!--more-->

在开发`web`的时候我们可以修改标签属性的默认值,比较常用的有:`reset.css`或者`normalize.css`.那么在开发`RN`的时候我们可以修改组件的属性的默认值吗?答案是当然可以的啦.通过查看源码发现通过如下修改,即可覆写`react-native`的原生组件的属性的默认值:

-   新建一个`JS`文件,代码如下所示:

```javascript
import { Text, TextInput, TouchableOpacity } from "react-native";
/**
 * 说明:此文件为修改React-native的原生组件的一些默认属性配置
 * 1.修改Text和TextInput的属性,字体大小不跟随系统设置
 * 2.修改TouchableOpacity的默认属性0.2 => 1(即去除该组件默认的按下去的阴影效果 => 点击的时候按下去没有阴影效果)
 */
TextInput.defaultProps = Object.assign({}, TextInput.defaultProps, {
    allowFontScaling: false,
});
Text.defaultProps = Object.assign({}, Text.defaultProps, {
    allowFontScaling: false,
});
TouchableOpacity.defaultProps = Object.assign(
    {},
    TouchableOpacity.defaultProps,
    { activeOpacity: 1 }
);
```

这里修改了 3 个常用组件的默认值

-   2.在`RN`项目的入口处导入即可.我是在`index.js`中导入.

```javascript
// in index.js
`import './customComponentsConfig.js'`;
```

通过上述操作,即可重写掉`react-native`中组件的默认属性值.以上只是举例,根据自己的需求扩展即可.如果有问题,请翻看源码.

# 3. 结束语

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
      id: 'react-native-x21g',
        });
      gitalk.render('gitalk-container');
</script>
