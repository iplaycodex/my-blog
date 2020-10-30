---
title: react-native屏幕适配
date: 2019-08-09 14:11:14
tags:
    - react-native
categories:
    - react-native
---

> 作者：[iplaycodex](http://iplaycodex.com)
> 仓库：[github](https://github.com/iplaycodex)、[codePen](https://codepen.io/iplaycodex)
> 博客：[掘金](https://juejin.im/user/3597257774478359)、[segmentfault](https://segmentfault.com/u/iplaycodex)、[知乎](https://www.zhihu.com/people/CallMeAllenLliu)、[简书](https://www.jianshu.com/u/9cd27f169c7e)、[博客园](https://www.cnblogs.com/)、[leetcode](https://leetcode-cn.com/u/iplaycodex/)
> 公众号：[FEZONE](http://iplaycodex.com)
> 联系我：[iplaycodex@163.com](iplaycodex@163.com)
> 特别声明：原创不易，未经授权不得对此文章进行转载或抄袭，否则按侵权处理，如需转载或开通公众号白名单可联系我，尊重原创尊重知识产权从我做起

# 1. 前言

在使用`react-native`进行开发的时候我们参见官方文知道做屏幕适配是使用`flexBox`来进行布局.

[戳我查看 flexBox 布局](https://reactnative.cn/docs/flexbox/)

有关`flexBox`的属性这里不做太多介绍,不会的请参考官方文档.这里只是说一下,因为在做屏幕适配的时候的解决之道.

> 在 react-native 中我们使用 StyleSheet 这个对象来进行样式的开发.例如:

```javascript
import { StyleSheet } from "react-native";

// 声明了一个style的变量,使用它来给组件添加样式
let style = StyleSheet.crate({
    title: {
        fontSize: 14,
        color: "#BBB",
    },
    subTitle: {
        marginTop: 10,
        marginBottom: 10,
        paddingLeft: 10,
        paddingRight: 10,
    },
});
```

<!--more-->

可以看到在`react-native`中写样式和在`web`中写`CSS`还是有很大的区别的.哪些好用的`less`,`sass`等基本上不可以用.而且也不可以`用复合样式`.例如:

**web 中写样式**

```css
/* web */
.title {
    padding: 10 20 15 5;
}
```

**react-native 中写样式**

```javascript
/* react-native */
title:{
    paddingTop:10,
    paddingRight:20,
    paddingBottom:15,
    paddingLeft:5
}
```

可以看到在`rn`中写样式还是比较麻烦的.

# 2. 使用`flexbox`布局

`flexBox`给我们提供了很方便的布局方法,但是有时候我们还是需要一些常规属性,例如:`width`,`height`,`paddingTop`,`fontSize`等等...因为在`rn`中样式是没有单位的(默认`dp`),那么这个时候问题就来了,在不同的屏幕上它的`dpi`是不同的,如何做适配呢?

通过查看官方文档,找到了解决方法.封装了一个方法`dp2px`,代码如下所示:

```javascript
import { Dimensions } from "react-native";
const deviceWidthDp = Dimensions.get("window").width;
// 默认设计稿375
const uiWidthPx = 375;
function dp2px(uiElementPx) {
    return (uiElementPx * deviceWidthDp) / uiWidthPx;
}
export default dp2px;
```

这样在开发中如果需要使用一些`宽度`,`高度`等属性的时候直接引用这个方法就可以了.如下所示:

```javascript
import dp2px from './dp2px';

title:{
    paddingTop:dp2px(10),
    paddingRight:dp2px(20),
    paddingBottom:dp2px(15),
    paddingLeft:dp2px(5)
}
```

这样就完成了适配的工作.但是这个就是最优解了么,显然不是.每次写样式的都需要把这个函数引用进来,而且每次都要写大量的`dp2xp`,实在是非常的麻烦.那么问题来了,我们如何优化?

# 3. 封装 CustomStyleSheet 代替原生 StyleSheet

通过翻看源码,发现`StyleSheet`不是一个类,我们不需要继承它,重写它的这个方法,只需要自己封装一个类似`StyleSheet`这样的一个函数在它的内部进行一些计算,然后在需要写样式的地方,统一使用我们的`CustomStyleSheet`代替原生的`StyleSheet`即可.代码如下所示:

```javascript
import { StyleSheet } from "react-native";
import dp2px from "./dp2px";

let MyStyleSheet = {
    create(style) {
        let s = { ...style };
        // 目前仅对以下的属性进行处理
        let list = [
            "width",
            "height",
            "marginTop",
            "marginBottom",
            "marginLeft",
            "marginRight",
            "paddingTop",
            "paddingRight",
            "paddingBottom",
            "paddingLeft",
            "top",
            "right",
            "bottom",
            "left",
            "fontSize",
            "lineHeight",
        ];
        for (outKey in s) {
            for (innerKey in s[outKey]) {
                if (
                    list.includes(innerKey) &&
                    typeof s[outKey][innerKey] == "number"
                ) {
                    s[outKey][innerKey] = px2dp(s[outKey][innerKey]);
                }
            }
        }
        return StyleSheet.create(s);
    },
};
export default MyStyleSheet;
```

通过上述封装后使用起来就很方便了.在`react-native`组件中直接使用它来代替原生的`StyleSheet`即可.例如:

```javascript
import MyStyleSheet from "./myStyleSheet";

// 使用封装好的MyStyleSheet来代替原生StyleSheet,直接写数字即可自动转换为不同屏幕适配的dp
let style = MyStyleSheet.create({
    title: {
        fontSize: 14,
        width: 100,
    },
    subTitle: {
        paddingTop: 10,
        paddingBottom: 10,
        marginTop: 10,
        marginBottom: 10,
    },
});
```

至此,结束.附上相关资料,供学习.

---

参考资料:

[阮一峰的 Flex 教程](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html?utm_source=tuicool)

# 4. 结束语

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
      id: 'react-native-r14i',
        });
      gitalk.render('gitalk-container');
</script>
