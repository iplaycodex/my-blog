---
title: web开发规范之CSS
date: 2019-10-31 18:08:10
tags:
    - 前端
categories:
    - 前端
---

> 作者：[iplaycodex](http://iplaycodex.com)
> 仓库：[github](https://github.com/iplaycodex)、[codePen](https://codepen.io/iplaycodex)
> 博客：[掘金](https://juejin.im/user/3597257774478359)、[segmentfault](https://segmentfault.com/u/iplaycodex)、[知乎](https://www.zhihu.com/people/CallMeAllenLliu)、[简书](https://www.jianshu.com/u/9cd27f169c7e)、[博客园](https://www.cnblogs.com/)、[leetcode](https://leetcode-cn.com/u/iplaycodex/)
> 公众号：[FEZONE](http://iplaycodex.com)
> 联系我：[iplaycodex@163.com](iplaycodex@163.com)
> 特别声明：原创不易，未经授权不得对此文章进行转载或抄袭，否则按侵权处理，如需转载或开通公众号白名单可联系我，尊重原创尊重知识产权从我做起

# 1. 前言

团队内部整理的一份 CSS 开发规范,供参考

# 2. 基本规范

1.【推荐】缩进使用四个空格

```css
/* bad */
.mod-example {
    padding-left: 15px;
}

/* good */
.mod-example {
    padding-left: 15px;
}
```

2.在每个`声明块`的`左花括号`前添加一个空格

```css
/* bad */
.mod-example {
    padding-left: 15px;
}

/* good */
.mod-example {
    padding-left: 15px;
}
```

<!--more-->

3.声明块的右花括号应当单独成行

```css
/* bad */
.mod-example {
    padding-left: 15px;
}

/* good */
.mod-example {
    padding-left: 15px;
}
```

4.每条声明语句的 : 后应该插入一个空格，前面无空格

```css
/* bad */
.mod-example {
    padding-left: 15px;
}

/* good */
.mod-example {
    padding-left: 15px;
}
```

5.所有声明语句都以分号结尾，不能省略不写

```css
/* bad */
.mod-example {
    padding-left: 15px;
}

/* good */
.mod-example {
    padding-left: 15px;
}
```

# 3. 选择器规范

1.为选择器分组时，将单独的选择器单独放在一行

```css
/* bad */
.selector,
.selector-secondary {
    padding-left: 15px;
}

/* good */
.selector,
.selector-secondary {
    padding-left: 15px;
}
```

2.为选择器中的属性添加双引号

```css
/* bad */
.selector[type="text"] {
    padding-left: 15px;
}

/* good */
.selector[type="text"] {
    padding-left: 15px;
}
```

3.建议选择器层级不要超过 5 级

```css
/* bad */
.main .top .left .mod-a .content .detail {
    padding-left: 15px;
}

/* good */
.mod-a .content .detail {
    padding-left: 15px;
}
```

# 4. 属性规范

【推荐】建议相关的属性说明放在一组，并按照下面的顺序排列：

-   1. 定位（position、left、right、top、bottom、z-index）
-   2. 盒子模型（display、float、width、height、margin、padding、border、border-radius）
-   3. 排印（font、color、background、line-height、text-align）

由于`定位`可以从正常的文档流中移除元素，并且还能覆盖盒模型相关的样式，因此排在首位。而`盒模型`决定了组件的尺寸和位置，所以排第二位。`排印`只是影响元素的细节样式变化，所以放第三位。

```css
/* bad */
.mod-example {
    font: normal 13px "Helvetica Neue", sans-serif;
    display: block;
    position: absolute;
    z-index: 100;
    width: 100px;
    height: 100px;
    border: 1px solid #ccc;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    line-height: 1.5;
    text-align: center;
}
/* good */
.mod-example {
    /* 定位 */
    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    z-index: 100;
    /* 盒模型 */
    display: block;
    float: right;
    width: 100px;
    height: 100px;
    margin: 15px auto;
    padding: 10px 15px;
    border: 1px solid #ccc;
    /* 排印 */
    font: normal 13px "Helvetica Neue", sans-serif;
    line-height: 1.5;
    color: #333;
    background-color: #f5f5f5;
    text-align: center;
}
```

# 5. 简写形式的属性声明

对于 `background` 和 `font` 这两个简写形式的属性声明，要么就显式声明所有的值，要么就不要使用简写形式。

# 6. 和 单位

省略 `“0”` 值后面的单位。不要在 `0` 值后面使用单位，除非有值。

```css
/* bad */
.mod-example {
    padding-left: 0px;
}

/* good */
.mod-example {
    padding-left: 0;
}
```

# 7. 颜色值十六进制表示法

1.在可能的情况下，使用 3 个字符的十六进制表示法，并始终使用小写的十六进制数字

```css
/* bad */
.mod-example {
    color: #cccccc;
    background-color: #efefef;
}

/* good */
.mod-example {
    color: #ccc;
    background-color: #efefef;
}
```

2.应避免 16 进制表示法与 rgb 表示法混用的情况，并优先使用 16 进制表示法

```css
/* bad */
.example-part1 {
    color: #efefef;
}
.example-part2 {
    color: rgb(252, 252, 252);
}

/* good */
.example-part1 {
    color: #efefef;
}
.example-part2 {
    color: #fcfcfc;
}
```

# 8. 小数

1.对于使用到小数的情况，省略前边的 0

```css
/* bad */
.mod-example {
    opacity: 0.5;
}

/* good */
.mod-example {
    opacity: 0.5;
}
```

# 9. 引号

1.`属性选择器`或`属性值`用双引号 `""` 括起来，而 `URI` 值 `url()` 不要使用任何引号

```css
/* bad */
body {
    font-family: open sans, arial, sans-serif;
    background-image: url("https://allenliu.com.cn/");
}

/* good */
body {
    font-family: "open sans", arial, sans-serif;
    background-image: url(https://allenliu.com.cn/);
}
```

# 10. 自定义 `font-family`

1.对于自定义的 `font-family` 命名，必须使用`业务域名前缀`作为名字的开始，例如淘宝爱逛街的自定义字体：

```css
/* bad */
@font-face {
    /* 业务自定义字体 */
    font-family: icon-font;
    src: url(//allenliu.com.cn/yyw/wap/home/static/fonts/iconfont.969ef42.woff);
}

@font-face {
    /* 业务自定义字体 */
    font-family: guang-iconfont;
    src: url(//allenliu.com.cn/yyw/wap/home/static/fonts/iconfont.969ef42.woff);
}
```

# 11. 媒体查询(`Media query`)规约

媒体查询建议根据需要采用下面两种组织形式：

-   将媒体查询放在尽可能相关规则的附近，不要放在文档底部，否则容易被后来维护的人遗忘
-   媒体查询针对每一个种屏幕（大、中、小）的分别单独组织为一个文件

例如:

```css
.element {
}
.element-avatar {
}
.element-selected {
}
@media (min-width: 480px) {
    .element {
    }
    .element-avatar {
    }
    .element-selected {
    }
}
```

例如:

```css
.element {
}
.element-avatar {
}
.element-selected {
}

/* base-media-small.css */
@media (min-width: 480px) {
    .element {
    }
    .element-avatar {
    }
    .element-selected {
    }
}
```

# 12. 注释规范

代码是由人来编写和维护的。保证你的代码是描述性的，包含好的注释，并且容易被他人理解。好的代码注释传达上下文和目标。不要简单地重申组件或者 class 名称。

```css
/* bad */

/* Modal header */
.modal-header {
}

/* good */

/* Wrapping element for .modal-title and .modal-close */
.modal-header {
}
```

# 13. 文件注释

文件注释，即声明在文件头部，描述文件的元信息，表明这个文件的作用是什么，如下例子：

```css
/**
 * 这个文件的作用是什么，巴拉巴拉
 */
body {
    color: red;
}
```

# 14. 命名规范

1.小写字母加连字符(也叫烤串命名法),禁止下划线和驼峰命名

```css
/* bad */
.mod_example {
    padding-left: 15px;
}
.modExample {
    padding-left: 15px;
}
/* good */
.mod-example {
    padding-left: 15px;
}
```

3.需要在 javascript 中使用的类名以 J\_ 开头，接“大驼峰”命名。例如 J_ExampleClass， 并且这类的 class 不能出现在 CSS 文件中

```html
<!-- Bad Html Class for Javascript Hook -->
<div class="mod-example"></div>

<!-- Good Html Class for Javascript Hook -->
<div class="J_ExampleClass">Just a Example</div>
```

# 15. 结束语

❤️ 关注 + 点赞 + 收藏 + 评论 + 转发 ❤️ <br/>原创不易，鼓励笔者创作更好的文章~
