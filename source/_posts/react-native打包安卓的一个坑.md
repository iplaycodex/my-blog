---
title: react-native打包安卓的一个坑
date: 2019-07-29 16:34:10
categories:
    - react-native
tags:
    - react-native
---
### 写在前面
如果你在做一个混合开发的APP,也就是说部分模块使用`native`去开发,部分模块使用`react-native`去开发.这个时候如何使用图片资源就有的玩了.如何合理的使用图片资源也是一个问题.
>引申:在`react-native`中如何使用图片资源

根据官方文档所述:在`react-native`中使用`image`的话有几种方法:
- 1.使用APP中的图片资源
也就是说在JS中直接访问`APP`沙盒中存在的图片资源,`iOS`加载`assets`目录,安卓加载`drawable`目录.代码如下所示:

```javascript
<Image source={{uri:'test_img'}} style={{width:100,height:100}}>
```

使用这个方法加载图片资源的话不需要写后缀,但是!你必须要确保这个图片在APP的沙盒内部是一定存在的!`react-native`不会检查这个文件是否存在如果不存在则出现一个空白.

- 2.使用网络图片
这个就很简单了,看下面的代码:

```html
<Image source={{uri: 'https://facebook.github.io/react/logo-og.png'}}
       style={{width: 400, height: 400}} />
```
注意:`iOS`因为从`iOS8`开始只能使用`https`了,所以这里建议网络图片全部使用`https`,并且需要指定尺寸.

<!--more-->

- 3.使用base64

在`react-native`中是可以使用`base64`的图片的,在想目中一些`icon`你可以选择使用`iconFont`也可以选择使用`base64`.使用`base64`也很简单,找个在线转码的网站,把你需要转的图片转成`base64`就可以了.在代码中这样使用:

```html
<Image source={{uri:"data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAD8AAAA/CAYAAABXXxDfAAAD0ElEQVR4Ae2aA5A8VxDGO7Ztv57D65mLbZvd7xjbRunv2LZt2045KsS27aSDvT7PZg87e+9X1aVbfY/f13MwWohEIpFIJBKJJL7VO+KJ6OU65/mOohWS3ILEZ9elYas//vhjMshDw3ZjpnYUJjniX53nP2qh0PMjSO2LwUCg58vtG2toAD5Ilu+YA/rCZbxllzcRX5IQb5Y0Na80JJWFlYeqMOW1XCpHOC9fdeqRq/uZdXmyNFJpGA81QB3J0kjy83+6GpcLC0F39FAwL/o9y3aYFWoEJLnnP/FJKltDd3CVnWYy++NTUGpH/FklbRR27l88ySc1Jv5Ms+93ieKj+Cg+94FX++K10MvDLpPloOCoLvX5ucWb+h1JrlxzzR2mhYKhXh5JLnOef1Qt/Ypfc80xUyLJ/ioWib/rNgh3LLPMblNBThrW3GvGhMJRSHJKxZXKsXUkjWUJ97KF8/KD1dCveIsGACS+1b4Jia+HnGgqHNxgIq9CTtTEdE+kSPJC4uVo58OBSG0IeUhSPrjbj9go5wFz6OAmMnku1++l5u27/d6X60hWhP+LJiGzZJ6BHGhO0DSos1BpuTS09xlFDdgU5jcJTuuOlVY6cDqoBKL2udHzZ6VgkIU1q7PzJCfaGV9hhdaZB+uePKVz9sMkqDL0sHbEX5jktikMFhoDzcF3axVm9hXNrL82ZsyYyWGw0K6LEf84VBmYhp1M9+mqwR3ZrHk9c23cU3XiPR9mxE+EwUTvR7OszoUqw/mwd+d+5zNgMNErriQ+De1QZaijM1fcfTBY6F1rltRHf9nc6aHKUB+gOeTfbfmz3vlQKdrpRC+fl5YUhUMgJy5tXhU9H4PEx1dSiQ+75Tm9kfhBY8ZOqHDGmzd0xB+bjP/WgLNuEyLx94NlbxNqboYBUOvdNY2GzaEcNLpixqug5wv1A+zTjrqsZamyPsfzp4Mlvi4Lm+Q0YzeYW+lb9fq5Y6hNQ3af16fNDVAm3rcsrvExSWX3Sgqpee0yvnM2ffDSLY3erSbN9iRyNDPkByQ5Tj8QCoRuTQ01vTVmNPjoFhqoh/dNwzIdC0PxsF5/oj13Rl33tm6Ztvm0J4HEr4/a1rW6vig+io/ie/4vjjkVf7St6qJj+5CYSWtfFvHtTkvJm0Hx0Xt/Fuflw/909dnN1UBgnV1dxhvbUFE01GXawIMkb/SpRy2uvqBbw/9bR/xOAevj7g5vQKvckLYsb5Z/TZRmfDU7ufeJPtbVLF9s0fyL83J/Q9aSgSXvk5emph3nUp9ftNJujr2xIpFIJBKJREYNfwIbCE1RyoFBpwAAAABJRU5ErkJggg=="}} style={{width:100,height:100}}>
```
这种方式仅适合一些小图,例如一些`icon`之类的.同样需要指定图片的尺寸

- 4.使用js自己的图片资源
把图片放在某处,使用`require`关键字来引用,如下所示:

```html
<Image source={require('./my-icon.png')} />
```

说了这么多,其实在项目中我们使用的方法是:`小图使用base64+大图使用网络图片或者本地图片资源`.这样做的有什么好处呢?
因为项目是`混合开发`的一个项目,所以如果要做新模块的话,那么图片一般不会已经存在于`APP`的沙盒中,这就需要我们自己提供图片资源了.而且这样也比较好解耦,APP只需要下载我们的`zip`包.并且解压缩出来`bundle`包和图片资源即可完成静默升级.

## 继续:

之前有写过一个`react-native`拆包的文章,上次打包的时候在使用了命令:
```javascsript
node ./node_modules/react-native/local-cli/cli.js bundle --platform ios --dev false --entry-file index.js --bundle-output ./release-ios/myCenter.bundle --assets-dest ./release-ios/ --config bus.config.js
```
打出来的业务包的`bundle`和业务中的图片资源都在`realease-ios`目录下面,然后在`iOS`中直接把这个目标文件夹放在任何一个路径下面都是可以直接加载到的.

**BUT:问题来了!执行了打包方法之后打包出来的安卓bundle以及图片资源.图片在安卓上面无法展示!!!**

经过查看`react-native`的文档以及各种`google`和`stack-overflow`终于找到了问题,原来打包出来的图片资源只能放在安卓的特定的目录下面:这个目录如下所示:

```javascript
andorid -> app -> src -> main -> res -> drawable-xhdpi/drawable-xxhdpi(对应的尺寸解压缩到同名的文件夹里)
```
这样就解决了混合APP中安卓无法加载`bundle`包中的图片资源.
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
      id: 'react-native-r18g',
        });
      gitalk.render('gitalk-container');
</script>