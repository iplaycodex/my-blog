---
title: linux下安装node环境以及配置软连接、pm2管理node进程
date: 2020-03-25 14:04:44
categories:
    - node
tags:
    - node
---

> 作者：[iplaycodex](http://iplaycodex.com)
> 仓库：[github](https://github.com/iplaycodex)、[codePen](https://codepen.io/iplaycodex)
> 博客：[掘金](https://juejin.im/user/3597257774478359)、[segmentfault](https://segmentfault.com/u/iplaycodex)、[知乎](https://www.zhihu.com/people/CallMeAllenLliu)、[简书](https://www.jianshu.com/u/9cd27f169c7e)、[博客园](https://www.cnblogs.com/)、[leetcode](https://leetcode-cn.com/u/iplaycodex/)
> 公众号：[FEZONE](http://iplaycodex.com)
> 联系我：[iplaycodex@163.com](iplaycodex@163.com)
> 特别声明：原创不易，未经授权不得对此文章进行转载或抄袭，否则按侵权处理，如需转载或开通公众号白名单可联系我，尊重原创尊重知识产权从我做起

# 1. 安装

在官方网站下载 linux 系统的安装包，然后上传到服务器进行解压安装:

执行解压命令：`tar -xvf node-v10.14.1-linux-x64.tar.xz`
重命名： mv `node-v10.14.1-linux-x64 nodejs`
确认一下`nodejs`下`bin`目录是否有`node`和`npm`文件，如果有执行软连接，如果没有重新下载执行上边步骤；
通过源码编译，在官方网站下载 Source code 文件，

```bash
tar xvf node-v10.14.1.tar.gz
cd node-v10.14.1
./configure
make
make install
cp /usr/local/bin/node /usr/sbin/ # 路径自己选择
```

查看当前安装的 Node 的版本 ： `node -v`

<!--more-->

# 2. 建立软连接,配置全局环境变量

```bash
ln -s /usr/local/nodejs/bin/npm /usr/local/bin/
ln -s /usr/local/nodejs/bin/node /usr/local/bin/

# 检查一下,是否配置好了
node -v
npm -v
```

# 3. 使用 pm2 进行 node 进程管理

```bash
安装：npm i pm2 -g
运行：pm2 start app.js
停止所有进程：pm2 stop all
重启所有进程： pm2 restart all
```

# 4. 查看 pm2 的一些指令

```bash
# user pm2 --help check more
pm2 --help
```

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
      id: 'node-20200305-0210',
        });
      gitalk.render('gitalk-container');
</script>
