---
title: 深入浅出react+redux之jsx
date: 2019-08-22 15:03:46
categories:
    - react.js
tags:
    - react.js
---

> 作者：[iplaycodex](http://iplaycodex.com)
> 仓库：[github](https://github.com/iplaycodex)、[codePen](https://codepen.io/iplaycodex)
> 博客：[掘金](https://juejin.im/user/3597257774478359)、[segmentfault](https://segmentfault.com/u/iplaycodex)、[知乎](https://www.zhihu.com/people/CallMeAllenLliu)、[简书](https://www.jianshu.com/u/9cd27f169c7e)、[博客园](https://www.cnblogs.com/)
> 联系我：[iplaycodex@163.com](iplaycodex@163.com)
> 特别声明：原创不易，未经授权不得对此文章进行转载或抄袭，否则按侵权处理，如需转载或开通公众号白名单可联系我，尊重原创尊重知识产权从我做起

# 1. 需求

单独把`JSX`拿出来说一下,因为我觉得这个东西有必要深入研究一下.下面是我当时学习`react.js`的时候想到的几个问题:

-   为什么要在`react.js`中使用`jsx`?
-   将事件声明写在了`JSX`中是一种进步还是一种倒退?
-   `react.js`是如何根据`diff`算法底层实现模板高性能重新渲染的?(因为我们知道每执行一次`setState()`,都会执行一次`render()`函数,`react.js`底层做了什么?它是如何优化的?

下面我们带着这几个问题,来深入研究一下什么是`JSX`.

<!--more-->

# 2. JSX

`JSX`是`facebook`推荐在开发`react`项目的时候替代`HTML`的写法,当然你也可以使用`HTML`,但是极度不推荐使用.下面我们看一个最简单的例子:

```javascript
import React, { Component } from "react";
import CustomComp from "./CustomComp";

class T extends Components {
    constructor(props) {
        super(props);
    }
    render() {
        return (
            <div>
                {/*原生标签*/}
                <p>我是原生组件</p>
                {/*react.js自定义组件*/}
                <CustomComp />
                {/*定义一个事件*/}
                <button onClick={this.click}>BUTTON</button>
            </div>
        );
    }
    click() {
        alert("btn did clicked!");
    }
}
```

可以看到和我们之前写`HTML`大不同的地方就是`react.js`把`HTML`直接写在了`js`中.上面那个`render()`函数中包裹的就是`JSX`.

**注意:在使用 JSX 的代码中必须导入 React,也就是说第一行代码的`import React,{ Component } from 'react'`虽然看起来在代码中我们没有使用`React`,但是它是很有用的.因为`JSX`会被转译成依赖`react.js`的`表达式`**

# 3. 分析为什么要在`react`中使用`jsx`?

第一节我们已经知道了`JSX`是个什么东西,这一节我们分析一下为什么要在`react.js`中使用`jsx`.因为在`react`的设计思想中是`all in js`.所以我们如果在要在`JS`中写`DOM`的话,则需要创造一个一个的`DOM`对象.用`JS`来写，会非常的冗余并且不能一目了然的看清楚`DOM`的结构。所以这个时候`JSX`就诞生了!

思考一个问题：如何用`JavaScript`对象来表现一个`DOM`元素的结构，举个例子：

```html
<div class="box" id="content">
    <div class="title">Hello</div>
    <button>Click</button>
</div>
```

每个 `DOM` 元素的结构都可以用 `JavaScript` 的对象来表示。你会发现一个 `DOM` 元素包含的信息其实只有三个：`标签名`，`属性`，`子元素`。

其实这个 `DOM` 结构我们是可以使用一个`js`对象来描述的,如下所示:

```javascript
{
  tag: 'div',
  attrs: { className: 'box', id: 'content'},
  children: [
    {
      tag: 'div',
      arrts: { className: 'title' },
      children: ['Hello']
    },
    {
      tag: 'button',
      attrs: null,
      children: ['Click']
    }
  ]
}
```

你会发现，`HTML` 的信息和 `JavaScript` 所包含的结构和信息其实是一样的，我们可以用 `JavaScript` 对象来描述所有能用 `HTML` 表示的 `UI` 信息。但是用 `JavaScript` 写起来太长了，结构看起来又不清晰，用 `HTML` 的方式写起来就方便很多了。

于是 `React.js` 就把 `JavaScript` 的语法扩展了一下，让 `JavaScript` 语言能够支持这种直接在 `JavaScript` 代码里面编写类似 `HTML` 标签结构的语法，这样写起来就方便很多了。编译的过程会把类似 `HTML` 的 `JSX` 结构转换成 `JavaScript` 的对象结构.

那么下面的这个代码:

```javascript
class Header extends Component {
    render() {
        return (
            <div>
                <h1 className="title">React 小书</h1>
            </div>
        );
    }
}
```

经过编译会变成:

```javascript
class Header extends Component {
    render() {
        return React.createElement(
            "div",
            null,
            React.createElement("h1", { className: "title" }, "React 小书")
        );
    }
}
```

`React.createElement` 会构建一个 `JavaScript` 对象来描述你 `HTML` 结构的信息，包括标签名、属性、还有子元素等。这样的代码就是合法的 `JavaScript`代码了。所以使用 `React` 和 `JSX` 的时候一定要经过编译的过程。

这里再重复一遍：**所谓的 JSX 其实就是 JavaScript 对象**。每当在 `JavaScript` 代码中看到这种 `JSX` 结构的时候，脑子里面就可以自动做转化，这样对你理解 `React.js` 的组件写法很有好处。

有了这个表示 `HTML` 结构和信息的对象以后，就可以拿去构造真正的 `DOM` 元素，然后把这个 `DOM` 元素塞到页面上。这也是我们最后一段代码中 `ReactDOM.render` 所干的事情：

```javascript
ReactDOM.render(<Header />, document.getElementById("root"));
```

`ReactDOM.render` 功能就是把组件渲染并且构造 `DOM` 树，然后插入到页面上某个特定的元素上（在这里是 id 为 root 的 div 元素）。

总结一下从`JSX`到页面都发生了什么?

![过程](http://ww2.sinaimg.cn/large/006y8mN6gy1g68j7f8khdj30g806k0t0.jpg)

有些同学可能会问，为什么不直接从 `JSX` 直接渲染构造 `DOM` 结构，而是要经过中间这么一层呢？

-   第一个原因是，当我们拿到一个表示 `UI` 的结构和信息的对象以后，不一定会把元素渲染到浏览器的普通页面上，我们有可能把这个结构渲染到 `canvas` 上，或者是手机 `App` 上。所以这也是为什么会要把 `react-dom` 单独抽离出来的原因，可以想象有一个叫 `react-canvas` 可以帮我们把 `UI` 渲染到 `canvas` 上，或者是有一个叫 `react-app` 可以帮我们把它转换成原生的 `App`（实际上这玩意叫 `ReactNative`）。
-   第二个原因是，有了这样一个对象。当数据变化，需要更新组件的时候，就可以用比较快的算法操作这个 `JavaScript` 对象，而不用直接操作页面上的 DOM，这样可以尽量少的减少浏览器重排，极大地优化性能。这个在以后的章节中我们会提到。

总结为下面的几个点:

-   `JSX` 是 `JavaScript` 语言的一种语法扩展，长得像 `HTML`，但并不是 `HTML`。
-   `React.js` 可以用 `JSX` 来描述你的组件长什么样的。
-   `JSX` 在编译的时候会变成相应的 `JavaScript` 对象描述。
-   `react-dom` 负责把这个用来描述 `UI` 信息的 `JavaScript` 对象变成 `DOM` 元素，并且渲染到页面上。

> 这里借鉴了[react.js 小书](http://huziketang.mangojuice.top/books/react/lesson6)的部分内容,感谢作者的分享

# 4. 在 JSX 中声明事件是进步还是倒退?

讨论完了`JSX`底层如何进行处理的,现在我们讨论一下:使用`JSX`是进步还是倒退?尤其是当在`JSX`中需要给某个组件定义一个事件的时候.

**html**

```html
<button onclick="click">BUTTON</button>
```

**react**

```javascript
render(){
  return (
    <button onClick={()=>alert('hello,react')}>BUTTON</button>
  )
}
```

在以前我们所有接触到的知识都告诉我们,写`web`的时候要模板,样式及逻辑分离.不可以直接在`html`中定义事件.直到今天这个观点我们也不会改变,在`html`中使用`onclick`很不专业!(注意是`onclick`而非`react.js`中的`onClick`).主要是因为一下几个点:

-   在`html`中添加的`onclick`的事件处理函数是全局的,这样容易污染全局环境,导致一些不可预知的错误
-   给很多标签绑定事件,会导致性能问题.网页需要处理的事件函数越多,性能就越低
-   对于使用了`onclick`的 DOM 元素,如果要把它动态的从页面中删除掉,那么它的事件处理器也要被注销掉.否则会有导致内存泄露的 BUG,而且这种 BUG 一般很难排查.

**上述说的问题,在`JSX`中不存在!**

-   首先,在`JSX`中声明的事件方法,仅在该组件内部有效.避免了污染全局环境
-   在`JSX`中所有的事件都委托给了顶层的`DOM`,当接收到用户的`action`的时候`react.js`会被顶层`DOM`的事件处理函数捕获,然后根据组件分发给不同的方法/函数.方法委托自然比一个一个事件绑定效率高
-   在`react.js`中组件存在声明周期,当组件被`unmount`的时候(也就是卸载/销毁)的时候,`react.js`会自动帮我们注销挂载在`JSX`上对应的事件处理方法.那么就不存在内存泄露的问题了.

# 5. 虚拟 DOM 和 diff 算法

这个稍微有些复杂,后面会再开一节进行详细说明

# 6. 结束语

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
      id: 'react-shenruqianchu-2-jsx',
        });
      gitalk.render('gitalk-container');
</script>
