---
title: 修改homebrew源解决下载速度慢的问题
date: 2020-10-09 16:26:17
categories:
    - 前端工程化
tags:
    - 前端工程化
---
[TOC]

# 1. 问题
今天使用`homebrew`下载软件的时候发现特别的慢(官方源因为有一道墙,大家都知道特别的慢)但是我记得我已经修改为了`清华大学`的源了,然而今天还是特别的慢.最后发现原来是清华大学的源坑了,修改为了`中科大`的源后解决了这个问题,这里记录一下.共同样掉坑的同学参考

# 2. 看一下那个源
```bash
# 进入 brew 的仓库根目录
cd "$(brew --repo)"

# 查看仓库地址
git remote -v

# 如下所示,目前是清华大学源
origin    https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/brew.git (fetch)
origin    https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/brew.git (push)
```
打开清华大学的源的仓库,发现404,坑了.

![](https://tva1.sinaimg.cn/large/007S8ZIlgy1gjj6ab3tjuj31140jmaad.jpg)

`清华大学`的源不能用了,那就换一个源.这里我们换成`中科大`的源

# 3. 修改源
执行以下命令:
```bash
# 进入 brew 的仓库根目录
cd "$(brew --repo)"

# 修改为中科大的源
git remote set-url origin https://mirrors.ustc.edu.cn/brew.git
```
同理，修改 `homebrew-cask`、`homebrew-core`、`homebrew-services` 的远程仓库地址:
```bash
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-cask"
git remote set-url origin https://mirrors.ustc.edu.cn/homebrew-cask.git

cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
git remote set-url origin https://mirrors.ustc.edu.cn/homebrew-core.git
```
修改完仓库地址后，更新一下，加上 `-v`参数可以看到当前跑的进度：
```bash
brew update -v
```

# 4. 结尾
将源修改为`中科大`的源后再安装软件发现熟悉的速度又回来啦~