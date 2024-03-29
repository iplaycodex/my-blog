---
title: web开发规范之HTML
date: 2019-10-31 18:01:37
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

团队内部整理的一份 HTML 开发规范,供参考

# 2. 基本规范

## 2.1. HTML5 doctype

在每个 `HTML` 页面开头使用这个简单地 `doctype` 来启用标准模式，使其每个浏览器中尽可能一致的展现。

```html
<!-- bad -->
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html>
    <head> </head>
</html>

<!-- good -->
<!DOCTYPE html>
<html>
    <head> </head>
</html>
```

<!--more-->

## 2.2. 字符编码

由于历史原因，X 系不同产品都是采用了不同的字符编码。对于以后的新业务如无特殊要求，统一使用 UTF-8 字符编码，便于统一。

## 2.3. Language attribute

根据 `HTML5` 规范：鼓励网站作者在 `html` 元素上指定 `lang` 属性，来指出页面的语言。这样做会有助于语言合成工具来确定怎样发音，以及翻译工具决定使用的规则，等等。

## 2.4. IE 兼容模式

`Internet Explorer` 支持使用兼容性 `<meta>` 标签来指定使用什么版本的 `IE` 来渲染页面。如果不是特殊需要，通常通过 `edge mode` 来通知 `IE` 使用最新的兼容模式。

```html
<meta http-equiv="X-UA-Compatible" content="IE=Edge,chrome=1" />
```

## 2.5. 引入 CSS 和 JavaScript

-   1.根据 `HTML5` 规约, 通常在引入 `CSS` 和 `JavaScript` 时不需要指明 `type`，因为`text/css` 和 `text/javascript` 分别是他们的默认值.

```html
<!-- bad -->
<!DOCTYPE html>
<head>
    <link type="text/css" rel="stylesheet" href="code-guide.css" />
    <script type="text/javascript" src="example.js"></script>
</head>

<!-- good -->
<!DOCTYPE html>
<head>
    <link rel="stylesheet" href="code-guide.css" />
    <script src="example.js"></script>
</head>
```

-   2.此外，引入 `CSS` 必须在 `<head></head>` 标签里引入。对于引入 `Javascript`，除了基础库等比较基础性的脚本文件，其他都在靠近 `body` 结束标签前面引入。

```html
<!-- bad -->
<!DOCTYPE html>
<html>
    <head>
        <script src="mod-a.js"></script>
        <script src="jquery.js"></script>
    </head>
    <body>
        <style>
            .mod-example {
                padding-left: 15px;
            }
        </style>
    </body>
</html>

<!-- good -->
<!DOCTYPE html>
<html>
    <head>
        <style>
            .mod-example {
                padding-left: 15px;
            }
        </style>
        <script src="jquery.js"></script>
    </head>
    <body></body>
</html>
```

## 2.6. 缩进使用四个空格

```html
<!-- bad -->
<div>
    <p>just a example</p>
</div>

<!-- good -->
<div>
    <p>just a example</p>
</div>
```

## 2.7. 标签名称和标签属性统一使用小写

```html
<!-- bad -->
<div id="test"></div>

<!-- good -->
<div id="test"></div>
```

## 2.8. 建议的 html 脚手架(适合 PC 开发)

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8" />
        <meta lang="zh" />
        <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
        <meta name="renderer" content="webkit" />
        <meta name="description" content="" />
        <meta name="keyword" content="" />
        <title>Project Name</title>
        <link rel="stylesheet" href="example.css" />
    </head>
    <body>
        <script src="example.js"></script>
    </body>
</html>
```

# 3. 属性规范

## 3.1. 属性引号用双引号

```html
<!-- bad -->
<link rel="stylesheet" href="example.css" />

<!-- good -->
<link rel="stylesheet" href="example.css" />
```

## 3.2. Boolean 属性

-   `Boolean` 属性指不需要声明取值的属性。XHTML 需要每个属性声明取值，但是 HTML5 并不需要。
-   一个元素中 `Boolean` 属性的存在表示取值 `true`，不存在则表示取值 `false`。简而言之，尽量不要为 `Boolean` 属性添加取值。

```html
<!-- bad -->
<input type="text" disabled="disabled" />

<input type="checkbox" value="1" checked="checked" />

<select>
    <option value="1" selected="selected">1</option>
</select>

<!-- good -->
<input type="text" disabled />

<input type="checkbox" value="1" checked />

<select>
    <option value="1" selected>1</option>
</select>
```

## 3.3. 自定义属性

建议自定义属性必须以 `data-` 为前缀，便于阅读。

```html
<!-- bad -->
<a modal="toggle" href="#"> Example link </a>

<!-- good -->
<a data-modal="toggle" href="#"> Example link </a>
```

## 3.4. 属性顺序

-   `HTML` 属性应该按照特定的顺序出现以保证易读性，而且一致的属性顺序可能提升 1.5%的 gzip 压缩率
    -   `class`
    -   `id`, `name`
    -   `data-*`
    -   `...`
-   `Classes` 是为高可复用组件设计的，所以他们处在第一位。Ids 更加具体而且应该尽量少使用（例如, 页内书签），所以他们处在第二位。

```html
<!-- bad -->
<a href="#" data-modal="toggle" id="... class="..."">
    Example link
</a>

<input type="text" class="form-control">

<!-- good -->
<a class="..." id="..." data-modal="toggle" href="#">
    Example link
</a>

<input class="form-control" type="text">
```

# 4. 标签规范

不要在自动闭合标签的结尾处使用斜线，如`<br>`、`<hr>`、`<input>`、`<meta>`、`<source>`

# 5. 命名规范

-   对于需要自定义属性，属性名命名统一使用 `data-` 前缀，具体参考`custom-data-attribute`
-   `class` 命名和 `css` 编码规范中的保持一致
-   `id` 命名，当作为 JS 钩子使用 时，以 J\_ 为前缀，后面接大驼峰命名，且这类选择器不能出现在 css 中，例如 J_ExampleIdForJs。其他使用用法，例如充当锚点，label 对应 input 的 id，都正常默认使用即可。

# 6. 多媒体兼容

-   为 `img` 标签添加 `alt` 属性以声明替代文本；
-   在多媒体标签内部提供指示浏览器不支持该标签的说明，如`object`、`audio`、`video`

```html
<!-- bad -->
<audio controls>
    <source src="horse.ogg" type="audio/ogg" />
    <source src="horse.mp3" type="audio/mpeg" />
</audio>

<!-- good -->
<audio controls>
    <source src="horse.ogg" type="audio/ogg" />
    <source src="horse.mp3" type="audio/mpeg" />
    Your browser does not support the audio tag.
</audio>
```

# 7. 注释规范

由于 html 代码一般不会经过预处理，出于安全考虑，html 代码中不能出现任何关于业务相关敏感信息的注释。

# 8. 结束语

❤️ 关注 + 点赞 + 收藏 + 评论 + 转发 ❤️ <br/>原创不易，鼓励笔者创作更好的文章~
