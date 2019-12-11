---
title: node在前端架构中是如何做中间层的一点学习
date: 2019-07-09 11:43:34
categories:
    - node
tags:
    - node
---
今天上午看了几篇文章,写的是在前端架构中`node`是如何扮演一个中间层的角色,以及使用`node`来扮演一个中间层这样的架构设计有什么好处.下面作一个简单的介绍:
首先我我们知道在广义的前后端分离中我们都是前端直接处理页面,通过`Ajax`,`jsonp`,`fetch`等从服务器端进行数据请求,然后在前端进行数据处理,从而渲染页面.
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
      id: 'node-n20e',
        });
      gitalk.render('gitalk-container');
</script>