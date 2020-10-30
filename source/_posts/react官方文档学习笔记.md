---
title: react官方文档学习笔记
date: 2019-07-09 18:27:55
categories:
    - react.js
tags:
    - react.js
---

> 作者：[iplaycodex](http://iplaycodex.com)
> 仓库：[github](https://github.com/iplaycodex)、[codePen](https://codepen.io/iplaycodex)
> 博客：[掘金](https://juejin.im/user/3597257774478359)、[segmentfault](https://segmentfault.com/u/iplaycodex)、[知乎](https://www.zhihu.com/people/CallMeAllenLliu)、[简书](https://www.jianshu.com/u/9cd27f169c7e)、[博客园](https://www.cnblogs.com/)、[leetcode](https://leetcode-cn.com/u/iplaycodex/)
> 公众号：[FEZONE](http://iplaycodex.com)
> 联系我：[iplaycodex@163.com](iplaycodex@163.com)
> 特别声明：原创不易，未经授权不得对此文章进行转载或抄袭，否则按侵权处理，如需转载或开通公众号白名单可联系我，尊重原创尊重知识产权从我做起

# 1. 函数组件和 class 组件

在`react`中组件分为`函数组件`和`class组件`,他们是有区别的,并不是说任何时候都可以用`class组件`.

-   函数组件

```javascript
// 定义一个函数组件
function welcome(props) {
    return <div>{props.name}</div>;
}
```

该函数是一个有效的`React组件`，因为它接收唯一带有数据的`props`（代表属性）对象与并返回一个`React`元素。这类组件被称为`函数组件`，因为它本质上就是`JavaScript 函数`。

-   class 组件

```javascript
// 定义一个class组件
class Welcome extends React.Component {
    render() {
        return <div>{this.props.name}</div>;
    }
}
```

上述两个组件在`react`中其实是等价的,但是不是相同的.`class`组件会有一些额外的特性.这个在后面会仔细分析.

<!--more-->

> **注意!在 react 中所有的组件都必须大写字母开头**

React 会将以小写字母开头的组件视为原生 DOM 标签。例如，`<div />`代表 HTML 的 div 标签，而 <Welcome /> 则代表一个组件，并且需在作用域内使用 Welcome。

---

# 2. 组件嵌套

其实就是自定义的组件是可以随意嵌套的,这里不在赘述.

---

# 3. Props 的只读性

`react`规定:组件无论是使用函数声明还是通过`class`声明，都决不能修改自身的`props`。组件的`props`

-   纯函数

```javascript
// 这样的函数被称为“纯函数”，因为该函数不会尝试更改入参，且多次调用下相同的入参始终返回相同的结果。
function sum(a, b) {
    return a + b;
}
```

-   非纯函数

```javascript
// 相反，下面这个函数则不是纯函数，因为它更改了自己的入参
function withdraw(account, amount) {
    account.total -= amount;
}
```

React 非常灵活，但它也有一个严格的规则：<br/>
**所有 React 组件都必须像纯函数一样保护它们的 props 不被更改。**

当然，应用程序的 UI 是动态的，并会伴随着时间的推移而变化。在下一章节中，我们将介绍一种新的概念，称之为 `state`。在不违反上述规则的情况下，`state` 允许 React 组件随用户操作、网络响应或者其他变化而动态更改输出内容。也就是说父组件传递过来的`props`是严禁修改,而组件自己内部的`state(状态)`是可以被修改的.

---

# 4. state 和生命周期

## 4.1. state

`State` 与 `props` 类似，但是 `state` 是私有的，并且完全受控于当前组件。<br/>
使用`state`需要组件是`class`组件,定义一个`class`组件如下所示:

```javascript
import React,{ Component } from 'react;

class Mine extends Component{
    constructor(props){
        // 构造器中必须super(props),这个是固定的写法
        super(props);
        // state 必须定义在这里
        this.state = {
            name:'ALLEN'
        }
    }
    render(){
        return <div>my name is {this.state.name}</div>;
    }
}
export default Mine;
```

**注意!在 react 的设计思想中,组件的 state 也是不可以直接修改的!这个叫做 react 的`immutable`设计思想.**

它是为了性能更加好,所以一般我们如果要修改`state`的值,建议拷贝一个它的副本,然后修改他的副本,再将修改之后的副本重新赋值给`state`,从而完成`state`的修改.

> state 有一下几个点需要特别注意:

-   1.不能直接赋值修改 state,而是使用`this.setState()`这样的一个方法来进行修改

```javascript
this.state.name = "bob"; //错误!
this.setState({
    //正确
    name: "bob",
});
```

-   2.State 的更新可能是异步的
    出于性能考虑,不建议在`this.setState()`中直接传入一个对象,而是传递一个函数来进行修改.

```javascript
this.setState({
    //normal
    name: "bob",
});
this.setState((state, props) => ({
    //better
    name: "bob",
}));
```

# 5. 生命周期

组件的生命周期,顾明思意,不必多言.下面列出`react`的几个生命周期的方法:

```javascript
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date:'2019'};
  }
  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
      </div>
    );
  }
  // react 的几个生命周期钩子
  componentDidCatch(){}
  componentWillMount(){}
  componentDidMount(){}
  componentWillUpdate()
  componentDidUpdate(){}
  componentWillReceiveProps(){}
  componentWillUnmount(){}
}
```

有关`react生命周期钩子`的详细解释,请翻阅官方文档`api章节`.

# 6. 单向数据流

在`react`中一个重要的设计思想就是`单向数据流`!

-   不管是父组件或是子组件都无法知道某个组件是有状态的还是无状态的，并且它们也并不关心它是函数组件还是 class 组件。
-   这就是为什么称 state 为局部的或是封装的的原因。除了拥有并设置了它的组件，其他组件都无法访问。
-   组件不关心`this.props`的值到底是父组件的`this.state`还是`this.props`还是用户输入的数据.

---

# 7. 事件处理

在`react`中处理事件也很简单,例如下面的代码:

```html
// 事件处理 <button onClick="{this.toggleBtnClick}">点击</button>
```

### 7.0.1. 可以看到和一般的 js 不同,在`react`定义一个方法名是小驼峰的写法,例如:`onClick`,`onChange`,`onFoucs`...

### 7.0.2. 被调用的方法使用`{}`进行包裹

### 7.0.3. 在 `React` 中另一个不同点是你不能通过返回 `false` 的方式阻止默认行为。(也就是`return false`)你必须显式的使用 `preventDefault` 才可以阻止默认事件.例如:

```javascript
function ActionLink() {
    function handleClick(e) {
        e.preventDefault();
        // return false 不行!
        console.log("The link was clicked.");
    }

    return (
        <a href="#" onClick={handleClick}>
            Click me
        </a>
    );
}
```

# 8. this 的问题

在`react`的组件方法中如果你想用`this`的话,这个时候问题就来了,如果你没有进行`bind`操作,那么这个时候`this`的值就是`undefined`,那么如何解决这个问题,有下面三种方法:

```html
<!--1. 在render中使用bind来进行绑定-->
<button onClick="{this.submit.bind(this)}">提交</button>
```

```javascript
// 2.在构造函数中进行绑定
constructor(props){
  super(props);
  this.submit = this.submit.bind(this);
}

// 3.使用实验性的 publicClassFields 语法,同样也可以解决这个问题
submit = () => {}
```

# 9. 向事件处理方法传参

有两种方法,废话不多说直接看代码:

```html
<button onClick={(e) => this.deleteRow(id, e)}>Delete Row</button>
<button onClick={this.deleteRow.bind(this, id)}>Delete Row</button>
```

上述两种方式是等价的，分别通过`箭头函数`和 `Function.prototype.bind` 来实现。

在这两种情况下，`React` 的事件对象 `e` 会被作为第二个参数传递。如果通过箭头函数的方式，事件对象必须显式的进行传递，而通过 `bind` 的方式，事件对象以及更多的参数将会被隐式的进行传递。

---

# 10. 条件渲染

不像`vue`里面有封装好指令`v-if`或者`v-show`来供我们使用,在 react 中如果我们需要使用条件渲染的话,我们可以使用`if(){...}`或者`三元运算符`或者`true && expression(与运算符)`,如下所示:

```javascript
// 1.使用if来进行判断
function Greeting(props) {
    const isLoggedIn = props.isLoggedIn;
    if (isLoggedIn) {
        return <UserGreeting />;
    }
    return <GuestGreeting />;
}

// 2.三元
{
    isLoggedIn ? <UserGreeting /> : <GuestGreeting />;
}

// &&,之所以能这样做，是因为在 JavaScript 中，true && expression 总是会返回 expression, 而 false && expression 总是会返回 false。因此，如果条件是 true，&& 右侧的元素就会被渲染，如果是 false，React 会忽略并跳过它。

{
    isLoggedin && <UserGreeting />;
}

// 如果什么都不渲染的话直接返回null就可以了
{
    isLoggedIn ? <UserGreeting /> : null;
}
```

上述就是在`react`中,虽然没有很方便的`v-if`,`v-show`指令,我们完成条件渲染的方法.

# 11. 结束语

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
      id: 'react-r11i',
        });
      gitalk.render('gitalk-container');
</script>
