---
title: 深入浅出react+redux之state和props
date: 2019-08-22 17:49:39
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

# 1. state 和 prop

> 差劲的程序员操心代码，优秀的程序员操心数据结构和它们之间的关系。

毫无疑问,在`react`中处理数据是需要我们多关心的事情.页面是由数据进行驱动的,那么如何科学,高效的处理数据则成为我们需要思考的问题.

在`react`中数据大体上分为两种:

-   state
    -   state 是组件内部的状态
-   prop
    -   prop 是组件对外的接口

其实很简单,就一句话:`state用来处理组件的内部状态,prop用来和外部组件进行交互`

<!--more-->

# 2. 组件的 props

当我们初始化一个`类组件`的时候,在构造器中我们都会调用`super(props)`这个方法,那么为什么需要调用这个方法,如果不调用会导致什么结果的发生?可能很多人都没有仔细想过,因为基本上大多数的教程也都是让我们记住即可.今天我们讨论一下这个问题.

```javascript
// 组件的构造函数(也可以称之为构造器)
constructor(props){
    super(props);
}
```

这是因为:如果在构造函数中没有调用 `super(props)`，那么组件实例被构造之后，类实例的所有成员函数就无法通过`this.props`访问到父组件传递过来的`props`值.

而且还会直接报错,如下所示:

```javascript
ReferenceError: Must call super constructor in derived class before accessing 'this' or returning from derived constructor
```

还有一个要特别要注意的地方:**决不能修改 props!**

## 2.1. 设置`prop`的数据类型

既然`prop`是组件对外暴露的接口,那么应该有一个接口规范来约束组件外传入的数据类型.这个`propTypes`就排上用场了,它的使用也很简单,首先导入,然后设置目标组件的`propTypes`就可以了,如下所示:

```javascript
import React, { Component } from "react";
import PropTypes from "prop-types";
class T extends Component {
    constructor(props) {
        super(props);
    }
}
/*
这样就设置了T这个组件的prop的数据类型,name为字符串类型,并且是必传的.id是number类型,非必须
*/
T.propTypes = {
    name: PropTypes.string.isRequired,
    id: PropTypes.number,
};
```

**注意:`propTypes`检查,仅限开发阶段,生产阶段需要剔除!生产阶段检查类型不但消耗资源,而且错误展示给用户也没有意义,故在生产阶段需要关闭`propTypes`检查,所幸我们可以使用`babel-react-optimize`来自动帮我们完成这个工作**

## 2.2. 设置`prop`的默认值

这个就很容易理解了,给组件的`prop`设置一些默认值,当父组件没有传数据的时候会有一个默认值,哪些限制了`isRequired`的就不会报错了.还是上面的那个组件`T`.看下面的代码:

```javascript
T.defaultProps = {
    name: "allen",
    id: 1,
};
```

# 3. 组件的`state`

在`react`中驱动组件渲染过程的除了`prop`还有`state`.这一节我们就讲一下`state`.由于`react`不能修改`prop`,那么我们要记录组件自己的状态,就要使用`state`.

## 3.1. 修改`state`的值

`react.js`规定要修改`state`的值,必须使用`setState({})`来修改,不可以直接修改.

当然你非要直接修改,也是可以的.但是你会发现,直接修改值.页面并不会发生改变,这是因为直接赋值,虽然看起来你是修改了 state 中的值.但是并不会驱动页面的变化.这就是`setState()`帮我们做的一个事情,首先它会修改`state`中的值,然后它还会驱动组件的更新(`执行render()方法`)

## 3.2. 使用场景

我们已经知道了`state`的用途.在深入一下,什么时候该使用`state`什么时候需要使用类的`属性`?例如:

```javascript
constructor(props){
    super(props);
    this.state = {
        list:[] //页面列表
    }
    this.sub = null;    //订阅对象
}
```

其实很简单,一些状态的改变如果会导致页面的重新渲染,那么它就应该被定义在`state`中.如果某个字段不会导致页面的重新渲染,只是辅助我们开发,那么它就可以定义为这个类的一个属性.

# 4. 区别

说了这么多,现在总结一下区别吧:

-   `prop`用户定义外部接口,`state`用于定义内部状态
-   `prop`不可修改,而`state`可以修改
-   `prop`赋值在外部,`state`在内部

# 5. 结束语

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
      id: 'react-shenruqianchu-3-state-prop',
        });
      gitalk.render('gitalk-container');
</script>

