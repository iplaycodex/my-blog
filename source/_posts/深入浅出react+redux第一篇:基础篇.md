---
title: '深入浅出react+redux第一篇:基础篇'
date: 2019-08-22 14:34:19
categories:
    - react.js
tags:
    - react.js
---
## 写在前面
本篇连载是我学习`react.js`的一个笔记,之前一直保存在`有道云笔记`中,最近打算发到博客上面来.
***
### 1.环境配置
首先我们需要下载`react.js`的一个官方的脚手架工具:`create-react-app`.终端执行下面的命令:
```javascript
npm install -g create-react-app
```
即可安装,然后终端中输入`create-react-app -V`,即可查看该脚手架的ban版本.目前最新版的是`3.0.1`.

脚手架已经安装完毕了,我们来创建一个`react.js`的应用吧.
```javascript
// 1.init project
create-react-app my-react-app

// 2.cd 
cd my-react-app

// 3.run
npm run start
```
### 2.浅尝组件
现代前端开发开始流行一种开发思想叫做:`组件式开发`.不论是`vue.js`,`anglar.js`亦或者是我们今天要学习的`react.js`都是倡导组件式开发,所谓`组件式开发`即是把一个项目认为是一棵`组件树`,而每一个页面/模块都是该组件树的一个分支,该分支上的页面又可以拆分为不同的小组件,各个组件堆砌组合成为了一个功能完整的页面乃至应用.

一个最简单的`react.js`的组件如下所示:

<!--more-->

```javascript
import React,{ Component } from 'react';

class MyComponent extends Component{
    constructor(props){
        super(props)
        this.state = {
            name:'hello,world'
        }
        this.btnDidClick = this.btnDidClick.bind(this);
    }
    render(){
        return(
            <div>
                <p>我是一个最基础的react.js组件</p>
                <div>
                    <p>{this.state.name}</p>
                    <button onClick={this.btnDidClick}>点我</button>
                </div>
            </div>
        )
    }
    btnDidClick(){
        this.setState({
            name:'hello,react.js'
        })
    }
}
```
可以看到定义一个组件是一件很简单的事情,这里细心的朋友应该发现了一个问题:我们导入了`import React,{ Component } from 'react';`,在代码中我们定义的类继承自`Component`这个基类.但是`React`好像并没有用?那是不是可以不用导入?

尝试删除`React`,发现报错了!
```
'React' must be in scope when using JSX  react/react-in-jsx-scope
```
报错信息是指在使用`JSX`的范围内,必须要有`React`!所以,记住:<br/>
**当我们使用`JSX`的时候必须导入`React`!**

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
      id: 'react-shenruqianchu-1-rumen',
        });
      gitalk.render('gitalk-container');
</script>