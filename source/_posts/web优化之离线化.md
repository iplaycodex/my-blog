---
title: web优化之离线化
date: 2019-10-28 18:20:08
tags:
    - 性能优化
categories:
    - 性能优化
---

> 作者：[iplaycodex](http://iplaycodex.com)
> 仓库：[github](https://github.com/iplaycodex)、[codePen](https://codepen.io/iplaycodex)
> 博客：[掘金](https://juejin.im/user/3597257774478359)、[segmentfault](https://segmentfault.com/u/iplaycodex)、[知乎](https://www.zhihu.com/people/CallMeAllenLliu)、[简书](https://www.jianshu.com/u/9cd27f169c7e)、[博客园](https://www.cnblogs.com/)
> 联系我：[iplaycodex@163.com](iplaycodex@163.com)
> 特别声明：原创不易，未经授权不得对此文章进行转载或抄袭，否则按侵权处理，如需转载或开通公众号白名单可联系我，尊重原创尊重知识产权从我做起

# 1. 写在前面

现在混合开发的应用场景越来越多了.业内的解决方案也有很多,例:`native + react-native`的,支付宝或者微信的`native + 小程序`的.当然应用更多的还是`native + webView`这种场景.
使用`native + webView`的优点很多:

-   开发方便
-   方便快速迭代
-   ...

但是使用这套方案也有一个很致命的缺点:`那就是很慢!`,在`native`上点击了一个按钮触发一个打开`webView`的`action`操作,会经过以下几个过程:

`初始化webview` => `请求HTML,JS,CSS等静态资源` => `渲染模板` => `请求API`

这中间的时间很久.经过测试我们项目在安卓低端机上表现为平均加载完成时间为 4 ~ 5 秒.这是非常难以接受的!所以优化的需求就迫在眉睫了.

<!--more-->

优化的地方很多,本篇先介绍一下`资源静态化`!

-   使用静态化会将`HTML`和`CSS`以及`JS`保存在 APP 的沙盒中.当需要打开`h5`页面的时候直接从沙盒中通过`file:`读取,如此速度会大大提升!几乎可以做到近秒开.提升非常明显.

# 2. 如何做?

参见下面的 2 个流程图:

-   APP 启动流程图

![APP启动流程图](https://tva1.sinaimg.cn/large/006y8mN6gy1g8m03mtq2jj30e10h2dgn.jpg)

-   APP 中页面跳转流程图

![](https://tva1.sinaimg.cn/large/006y8mN6gy1g8m04hqehoj30do0iv75c.jpg)

# 3. 注意事项:

## 3.1. 登录态等数据存取使用`cookie`

## 3.2. 外链必须注明请求协议.例:`https:`

因为在内置包环境,打开`html`使用的是`file:`协议,故所有外链都必须写明资源协议,否则默认为`file:`.例:

```javascript
//bad
<script src="//baidu.com/jquery.js"></script>

//good
<script src="https://baidu.com/jquery.js"></script>
```

## 3.3. 页面跳转

模块内的页面跳转使用`vue-router`来实现,此处不再赘述.而模块间的页面跳转则需要使用` 全路径`.例:

```html
<button @click="pushToOtherModule">跳转到其他模块</button>
```

```javascript
methods:{
    pushToOtherModule(){
        // pushToOtherModule
        window.location.href = "http://baidu.com/web/h5/other/index.html#/goods/1";
    }
}
```

## 3.4. 跨域

使用`file:`协议加载`html`会导致跨域问题.该问题通过运维配置`nginx`已解决

## 3.5. 打包优化

`webpack`的图片处理,字体处理,以及`dllPlugin`,`treeshaking`等此处不在赘述.具体参见官方文档.

# 4. 名词解释

## 4.1. 内置包升级

通过`npm`打包成`zip`包上传后台即可

## 4.2. 开关

通过开关可以方便控制`APP`走内置包还是走服务器,方便一键切换

## 4.3. 白名单

白名单的作用是用来`映射URL`,即当用户触发一个`URL全链接`跳转的请求时,`APP`会进行拦截.通过匹配白名单,即可知道目标页面是走`内置包`还是走`HTTP`请求.

---

大致的思路目前就是这样,实现起来也不是很难.对于性能提升却是质的飞跃,所以强烈推荐.此文档登录态维护在`APP`端,故登录态没有详述.这个也不难,读者自己思考即可.

# 5. 结束语

❤️ 关注 + 点赞 + 收藏 + 评论 + 转发 ❤️ <br/>原创不易，鼓励笔者创作更好的文章~
