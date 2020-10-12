---
title: Smartgit使用30天过期解决办法
date: 2019-10-11 14:36:45
tags:
    - Git
categories:
    - Git
---
`smartGit`是一款`git`比较好用的GUI工具.未注册版本提供30天的试用期,提供一个过期了以后还可以使用的方法:
- 1.打开`Finder`
- 2.使用快捷键 `command + shift + G`
- 3.复制 `~/Library/Preferences/SmartGit/` 到输入框
- 4.点击确定调转到指定的文件夹删除settings.xml文件

至此,即可在30天的试用期到了以后继续使用了.当然最后还是要说一句,如果有条件,请支持正版.
***
提醒:最近`smartGit`有更新,发现本方法仅对版本低于:`18.2.9 #13269`有效.高版本暂不支持

***
安装完毕后我们修改 `smGit` 检查更新的请求 host 到本地,避免不停的提醒更新,烦的要死.`host` 文件添加如下代码:

```bash
127.0.0.1 www.syntevo.com
``

就酱,很简单
