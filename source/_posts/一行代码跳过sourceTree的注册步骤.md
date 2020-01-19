---
title: 一行代码跳过sourceTree的注册步骤
date: 2020-01-19 15:34:22
tags:
    - Git
categories:
    - Git
---
## RT
最近帮朋友装电脑,发现`sourceTree`得注册,很麻烦.遂找到如下解决方法:

<!--more-->
- 打开`sourcetree`
- 关闭sourcetree
- 命令终端输入如下内容,然后运行:
```javascript
defaults write com.torusknot.SourceTreeNotMAS completedWelcomeWizardVersion 3
```
- 打开`sourceTree`即可跳过注册!
