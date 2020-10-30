---
title: react-native字体大小不随系统字体大小同步改变
date: 2019-07-18 13:51:46
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

最近在做`react-native`的开发,昨天项目提测了以后没想到在测试人员的测试手机上直接炸了!好几台手机都显示异常,`iPhone7`,`iPhoneX`,`iPhoneX Max`均出现字体变大,样式乱套的问题.

惊了!但是很纳闷在我的手机和模拟器都是没有问题的,遂查看测试的手机发现该测试人员均修改了几台测试手机的系统字体(修改步骤:`设置 -> 显示与亮度 -> 字体大小`),几台测试机的字体均被不同程度放大!这个就是问题的根源!

> 原来在`react-native`中`Text`和`TextInput`组件的字体大小会默认跟随系统的字体大小!

# 2. 解决之道

既然我们知道了导致这个问题的所在原因,那么就着手解决掉就可以了.经过查`react-native`的官方文档得知:在`react-native`中用来显示文字的，一般会用到两个组件：`Text`和`TextInput`。所以，我们只要针对这两个组件做好工作，那就基本上解决了字体大小适配的问题

而他们两个有个共同的属性`allowFontScaling`,这个属性的值模式是`true`,这个属性是什么意思呢?

> 是否随系统指定的文字大小变化而变化。默认值为 true

<!--more-->

## 2.1. 解决方法一:设置`allowFontScaling`属性为`false`

```html
// 设置该属性为false
<Text allowFontScaling="{false}" />
<TextInput allowFontScaling="{false}" />
```

但是这个方法有个弊端,也就是说在每次使用`Text`,`TextInput`组件的时候都要设置这个属性为`false`,有点麻烦,万一那次不小心忘了.就又炸了.

## 2.2. 解决方法二:封装原生`Text`和`TextInput`组件

每次使用`Text`或者`TextInput`组件的时候都要设置这个属性为`false`好烦,那么我们不禁会想到自己封装一个公共组件,如下所示:

```javascript
import React from "react";
import { Text } from "react-native";

export default class MyText extends React.Component {
    // 封装react-native原生组件为MyText
    render() {
        return (
            <Text allowFontScaling={false} {...this.props}>
                {this.props.children}
            </Text>
        );
    }
}
```

> TextInput 组件同理

这样每次在使用`Text`组件的时候就使用封装好的`MyText`就行了,这个问题也就解决了.但是,这不是更麻烦吗?每次使用的时候还需要导入这个组件,万一忘了就又炸了!这个方案 PASS!

## 2.3. 解决方案三:修改组件的`defaultProps`

翻看一下组件的源码:

> TextInput

```javascript
...
  getDefaultProps(): Object {
    return {
      allowFontScaling: true,
      underlineColorAndroid: 'transparent',
    };
  },
...
```

> Text

```javascript
...
  static defaultProps = {
    accessible: true,
    allowFontScaling: true,
    ellipsizeMode: 'tail',
  };
...
```

通过这两个代码片段可以知道，在定义 Text 和 TextInput 时，都有给组件设置默认属性的操作.那么就有解决方案就有了:

```javascript
TextInput.defaultProps = Object.assign({}, TextInput.defaultProps, {
    defaultProps: false,
});
Text.defaultProps = Object.assign({}, Text.defaultProps, {
    allowFontScaling: false,
});
```

切记这段代码要写在你`react-native`的入口处,我写在了`index.js`里面.使用该方法真正实现了一劳永逸,所以这个方法是最方便的.

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
      id: 'react-native-r25n',
        });
      gitalk.render('gitalk-container');
</script>
