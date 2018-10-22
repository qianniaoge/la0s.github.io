---
layout: post
title: 谈谈我的Android逆向学习之路
key: 20150103
tags: Android Reverse
excerpt_separator: <!--more-->
---
不知不觉研一的生活已经结束了，想当初进实验室的时候被安排到了APP分析（移动安全）这个组，当时基本没接触过这方面的东西，大学都是打CTF，Web渗透&Windows逆向等，进来以后便开始了我的Android逆向之路。因为组里的主要的工作是协议分析和样本检测，前期积累了下来大量的样本，这里说的样本是具有比如说抓包失败，检测代理， 某壳加固，反调试反hook等特征，这是一个从量变到质变的前提。  
前面的文章已经谈了很多技术方面的东西，这里主要分享一下我的一些学习方法和经验。<!--more-->
1.善于使用搜索引擎Google，这个是最基本也可能是最重要的，尤其是需要懂得一些搜索语法，当报错一堆error的时候就很重要了。  
2.没事可以去weibo（你可以把微博这种东西当做成一种社交方式，也可以理解成为一种学习的方法）,尤其是里面的那些比如安全客，freebuf的日常推送和各种博主（非虫，riusksk，瘦蛟舞等）分享的技术文章。  
![Desktop Preview](https://raw.githubusercontent.com/la0s/la0s.github.io/master/screenshots/20180806.1.jpg)

github（比如说搜索关键词xposed然后按star排序就能收获很多牛逼的模块）  
![Desktop Preview](https://raw.githubusercontent.com/la0s/la0s.github.io/master/screenshots/20180806.2.jpg)

看雪论坛的精华版块（对一个领域最快最好的入门方式就是先把相关的精华文章读一遍，这都是前人总结的成果，另外看雪上大神真的很多...）  
![Desktop Preview](https://raw.githubusercontent.com/la0s/la0s.github.io/master/screenshots/20180806.3.jpg)

微信这种隔阂的东西只会蒙蔽了你的双眼，所以朋友圈这东西还是少刷吧（我从来都是点个赞就走），世界那么大，应该多出去走走（参考如何科学上网），我觉得我的社交方法都是跟着前辈宝哥走的，宝哥极力推荐twitter上有很多安全热点和技术资讯（这点其实和weibo是差不多的，但是Twitter的世界要大得多，研究人员和工具作者都更多）  
![Desktop Preview](https://raw.githubusercontent.com/la0s/la0s.github.io/master/screenshots/20180806.4.png)
![Desktop Preview](https://raw.githubusercontent.com/la0s/la0s.github.io/master/screenshots/20180806.5.png)

3.多动手多实践，这是提高技术的不二法门（看雪上的很多方法和工具我都亲自实践了一遍）。只看文章是不行的，必须是去验证这方法是否可以，过程中可能会碰到新的问题然后解决它，做到举一反三。比如我之前搞过的两个典型APP。我试过各种方法，总结其中的经验。  
![Desktop Preview](https://raw.githubusercontent.com/la0s/la0s.github.io/master/screenshots/20180806.6.png)
