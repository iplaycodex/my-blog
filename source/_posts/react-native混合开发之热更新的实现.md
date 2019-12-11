---
title: react-native混合开发之热更新的实现
date: 2019-08-01 14:54:44
tags:
    - react-native
categories:
    - react-native
---
### 前言
`react-native`可以独立写APP,但是在更多的公司中以`混合开发模式`居多.也就是说部分模块使用`native`去开发,部分模块使用`react-native`来进行开发.这种开发模式带来的优点是显而易见的,`native`+`react-native`可以在处理某些更新频繁,突发性需求或者对Ui页面灵活性要求比较高的地方.例如`618`,`双11`,`双12`...这种页面通常都有具有很大的灵活性.如果这个时候我们都用`native`来实现则灵活性欠佳.而使用`native`+`react-native`的混合开发模式则可以完美的解决这个问题.静默升级,用户体验佳.且`iOS`不用发版,不用提交审即可更新,大大的提高了产品的迭代速度,为用户带来更好的体验

#### 1.HOW
具体怎么做呢?首先当然是我们需要打包各平台对应的`bundle`包.如何打包,参见上一篇文章:`react-native优化之拆包`.下面的是已经打包好的图示:
- iOS
![iOS包](http://ww3.sinaimg.cn/large/006tNc79gy1g5k6ziz6kpj30bs04vglk.jpg)

- android
![](http://ww1.sinaimg.cn/large/006tNc79gy1g5k71duwz6j30be04r0sz.jpg)

可以看到针对`ios`和`android`两个平台我们都已经打包出来的各自的`bundle`包和静态资源.
<!--more-->
**这里对文件做一下解释说明:**
- `base.bundle`这个是项目中的基础包,也是上面所说的`react-native优化之拆包`中的基础包.此包中包含`react`的一些基础依赖,例如:`react`,`react-native`,`react-navigation`,`redux`等底层基础依赖
- `bus.bundle`则是业务包.它是动态的,会升级的比较频繁.一般基础包会持久化在APP的沙盒中,基本上处于静止状态,不做更新,除非有大的版本更新,才做基础包更新.
- `assets`这个是iOS平台依赖的图片静态资源.内含在`react-native`中使用的`@2x`图和`@3x`图
- `drawable-xhdpi`和`drawable-xxhdpi`这个是安卓平台依赖的图片资源
  
在实际应用中我们一般会将`bus.bundle`和`assets`或者`drawable-xhdpi(drawable-xxhdpi)`打包成为一个ZIP,一来这样体积更小,在APP上下载也更快,二来这样可以把`bundle`和`静态资源`打包到一起,更新的时候直接下载这个ZIP,解压缩即可

### 问题
这样其实就完成了`react-native`在`iOS`和`android`中的热更新.但是理想是美好的,现实是残酷的.这里把我踩到的坑分享一下
#### iOS
iOS接入很正常没有问题,没有任何毛病.按照上面所述直接接入就可以了,比较简单

#### Android
安卓有坑!而且这个坑很大!网上资料比较少.当时做rn拆包的时候参考官方文档的打包代码如下所示:
```javascript
node ./node_modules/react-native/local-cli/cli.js bundle --platform android --dev false --entry-file index.js --bundle-output ./release-android/myCenter.bundle --assets-dest ./release-android/ --config bus.config.js
```
这个时候我把`bundle`和`静态资源(图片)`放在了安卓的:
```javascript
android => app => src => main => assets => rn(新建的)
```
一切都看起来这么顺利这么美好,跑起来瞅瞅:
**发现问题:所有的图片都不展示!**

经过各种翻看文档,发现要把图片解压缩在:`android => app => src => main => res => drawable-xhdpi或者drawable-xxhdpi`里.遂尝试之.重新跑一下,成功显示!

遂告诉`android`开发只需要执行下载更新的时候把zip下载完毕了以后把图片解压缩到这个目录里面问题就解决了!然而安卓开发给我反馈了一个令人沮丧的消息,这个目录是`只读`的!Excuse Me!!!只读,特么的逗我?

没想到这个方案也不行,真是坑爹啊!`react-native`官网也不见有提示说混合开发的图片资源放哪里啊.这可咋整!吐槽完毕之后问题还是要解决的,经过不懈的各种查看文档,到处`google`,`stackoverflow`冲浪,终于功夫不费有心人,找到了解决方案:
**安卓需要把更新包解压缩至sdcard这个目录里!!!**

### 热更新终极解决方案
踩了这么多的坑,热更新的解决方案终于落地了:
- 安卓接入`react-native`的初始版本安卓会将基础包和业务包放在`assets`中.然后当服务器上有ZIP的更新的时候会静默自动下载ZIP包,解压缩至`sdcard`这个目录里.缓存起来.以后每次启动的时候就直接加载`sdcard`中的`bundle`.至此即完成了混合开发中安卓端的热更新.
- 而`iOS`则就比较简单了,看上面所述即可.直接解压缩到沙盒目录中即可.当然肯定不能放到可以被用户手动清除到的地方.例如:`cache`目录.
  
至此:`react-native`的混合开发之热更新就解决完毕了.有什么问题可以留言或者给我发邮件都可以.
***
参考资料:
[混合开发是如何实现热更新的](https://www.jianshu.com/p/39b9f3c3372e)
[react-native热更新实现](https://segmentfault.com/a/1190000008744826)
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
      id: 'react-native-r20n',
        });
      gitalk.render('gitalk-container');
</script>