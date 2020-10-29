---
title: mac环境下配置jdk
date: 2019-07-19 11:31:30
categories:
    - react-native
tags:
    - react-native
---

> 作者：[iplaycodex](http://iplaycodex.com)
> 仓库：[github](https://github.com/iplaycodex)、[codePen](https://codepen.io/iplaycodex)
> 博客：[掘金](https://juejin.im/user/3597257774478359)、[segmentfault](https://segmentfault.com/u/iplaycodex)、[知乎](https://www.zhihu.com/people/CallMeAllenLliu)、[简书](https://www.jianshu.com/u/9cd27f169c7e)、[博客园](https://www.cnblogs.com/)
> 联系我：[iplaycodex@163.com](iplaycodex@163.com)
> 特别声明：原创不易，未经授权不得对此文章进行转载或抄袭，否则按侵权处理，如需转载或开通公众号白名单可联系我，尊重原创尊重知识产权从我做起

# 1. 需求

开发`react-native`需要配置安卓开发环境,所以我们需要安装`javaJDK`以及配置相关的环境变量,网上`window`的配置教程居多,这里是一个简单的`mac`版的`jdk`配置流程,仅供参考.

# 2. 配置`java`开发环境

下载对应平台的`jdk`,去`oracle`官网即可下载:<br/>
[戳我去下载 JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)

# 3. 安装 JDK

安装下载的`JDK`,等待安装完毕以后,打开终端,输入:

```bash
java - version;
```

如果出现下所示,就说明`JDK`已经安装成功了!

```bash
java version "12.0.2" 2019-07-16
Java(TM) SE Runtime Environment (build 12.0.2+10)
Java HotSpot(TM) 64-Bit Server VM (build 12.0.2+10, mixed mode, sharing)
```

安装完毕以后就可以在`/Library/Java/JavaVirtualMachines`这里找到刚才安装的`JDK`,其中`Contents`下的`Home`文件夹，是该`JDK`的根目录

<!--more-->

# 4. 配置环境变量

-   1.打开`终端`,如果你是第一次配置环境变量，可以使用`touch .bash_profile`创建一个`.bash_profile`的隐藏配置文件(如果你是为编辑已存在的配置文件，则使用`open -e .bash_profile`命令)

-   2.新建了`.bash_profile`隐藏文件,以后执行命令`open -e .bash_profile`打开这个配置文件

-   3.输入以下配置

```bash
JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0_40.jdk/Contents/Home
PATH=$JAVA_HOME/bin:$PATH:.
CLASSPATH=$JAVA_HOME/lib/tools.jar:$JAVA_HOME/lib/dt.jar:.
export JAVA_HOME
export PATH
export CLASSPATH
```

**注意:**<br/>
上面的`JAVA_HOME`是你`JDK`安装的`home`路径,这里需要修改为你本机的`JDK->home`路径<br/>
然后保存,关闭窗口即可.

-   4. 执行命令`source .bash_profile`使配置生效

-   5. 输入 `echo $JAVA_HOME` 显示刚才配置的路径,如下所示:

```javascript
/Library/Java/JavaVirtualMachines/jdk-12.0.2.jdk/Contents/Home
```

至此,我们就完成了`JDK`的安装和环境变量的配置.

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
      id: 'react-native-m9k',
        });
      gitalk.render('gitalk-container');
</script>
