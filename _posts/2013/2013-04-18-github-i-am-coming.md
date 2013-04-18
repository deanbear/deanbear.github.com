---
layout: post
title: 乔迁大吉
date: 2013-04-18 21:44:48
categories:
- 胡说/Who Says
tags:
- jekyll
- github
---
转眼四月又过去一大半啦，日本回来也没写文细说，下次吧，专门写个。日本回来后还参加了虾米组织的凡人弹唱会，一如既往的人多就紧张到手颤和弦都没按住。然后下周就要去驾照场考场考了，一定要过！时间和金钱都很贵的！而且太丢人了！ "扛不牢…"

这篇文章标题是乔迁大吉，当然不是我换房子了，不过房子下个月就差不多到期又要租房子去了。乔迁大吉是说我的博客搬家了，从美国的服务器空间搬到了Github.com，从WordPress转化成Jekyll了！这样就可以用Markdown来写东西了，祝福Markdown能促进我勤奋一点。按照惯例，我讲一遍前因后果。

**起因**

Github火很久了。由于公司用的是SVN，我也一直没去研究，只是注册了Github的帐号，git clone过Spring Framework一次，后续就没有再搞了。在此之间陆续听闻了Jekyll以及Github Pages，以及在Mac上安装了一个Mou(真的巨好用作，者是中国人牛逼)用Markdown(不晓得?Google it!)写了几篇文章，再由于前天早上博客一直502访问不了，况且WordPress的编辑框难用已经让我隐忍很久了，然后我就开始琢磨着将博客迁移到Github Pages.这样也比较符合我的身份，再顺便开始用git，也符合历史潮流。

**过程**

[Jekyll Wiki](https://github.com/mojombo/jekyll/wiki)上有具体的教程，我就简述一下我自己两天来的历程。

先到WordPress Admin将所有内容都导出，变成一个*.xml文件。然后用exitwp将\*.xml转化成markdown文件。看了内容，格式内容之类的还是完整可以接收的。

接着打算新开一个Repo自己搞Jekyll的时候，就卡住了，不晓得从何处下手。当然在这步之前，Github相关帐户以及ssh key之类的事情都做掉了，顺便还学习了一把git命令，和svn有区别，但是还是可以适应的。然后我就卡着，卡着，然后就摸到了[jekyll bootstrap](http://jekyllbootstrap.com)，集成了基本的样式结构页面，傻瓜式安装，按照上面的教程在本地搭好框架，最后git push一把就可以生成博客了。但是作为一名伟大光荣正确的程序员，我当然是不能容忍没有经过我亲自雕琢的应用了。然后我就花了一天半的时间，搞了主题，调了样式，加了内容结构，设置了Disqus(第三方评论)和Google Analytic(数据分析)，最后把thedeanbear.com的域名指向了deanbear.github.io，全部做完之后，略有做站长的感觉与体会…除了耗费两天之外，其他方面都很满意。

**结果**

不务正业的搞了两天，收获也算不小。

- 终于玩上了git了，学会了基本操作，比svn确实略好使(起码从个人角度看)。
- 调了两天css，学会了一些基本的样式写法与规则，然后结论是前端工程师牛逼。我都快疯了，才搞到差不多满意。
- 开源真是好，我起码看了3个家伙放在Github的jekyll博客源码，偷师不少。

好的，现在看到的就是我的新博客，基于jekyll和Github Pages，并利用了jekyll bootstrap工具搭建而成。

乔迁大吉！Github我来了。





