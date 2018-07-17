---
layout: post
title: 带你深入一款Android应用程序动态分析工具———Inspeckage
key: 20150103
tags: Android Reverse
---
Inspeckage是一个用来动态分析安卓app的xposed模块。Inspeckage对动态分析很多常用的功能进行了汇总并且内建一个webserver。整个分析操作可以在友好的界面环境中进行  
安装和使用笔记[Inspeckage使用笔记](https://blog.csdn.net/tom__chen/article/details/78216732)  
[安卓分析工具Inspeckage介绍](http://xdxd.love/2016/08/09/安卓分析辅助工具Inspeckage介绍/)

打开APP选中要分析的进程，然后launch APP即可

![Desktop Preview](https://raw.githubusercontent.com/la0s/la0s.github.io/master/screenshots/20180717.1.png)

然后执行命令adb forward tcp:8008 tcp:8008，浏览器打开http://127.0.0.1:8008/

下面来看一个360加固的APP案例  
由于Inspeckage自带的clear功能无法清理日志，所以为了精确过滤数据，先打开APP到设置页面，然后使用Inspeckage的clear all清除掉所有数据，然后重新选择APP进程，Launch APP，打开数据刷新开关，点击版本更新，然后关闭刷新开关

![Desktop Preview](https://raw.githubusercontent.com/la0s/la0s.github.io/master/screenshots/20180717.2.png)

成功输出了密钥key和数据加密前后的结果（当key和iv是不可见字符其实是经过base64编码的数据，另外的缺点是不支持中文），可以配合抓包数据以确定我们APP可能采用的加密方式

![Desktop Preview](https://raw.githubusercontent.com/la0s/la0s.github.io/master/screenshots/20180717.3.png)

下面再来看比较关键的的自定义hooks功能  
在这个功能里，Inspeckage不提供重载，所以当我们需要分析的函数有多个重名的方法时是没有办法的，在这篇文章里[Android应用逆向工程](https://www.anquanke.com/post/id/86884)，作者是把这个方法单独重命名重打包来分析的
而且在加壳APP中由于Inspeckage只能hook Java自身的类和方法，所以是无法做到frida和xposed模板hook应用本身加固的方法的，所以这个功能实际上比较有限。

![Desktop Preview](https://raw.githubusercontent.com/la0s/la0s.github.io/master/screenshots/20180717.4.png)

前面我们使用frida或者是xposed来获得APP的key，iv，Instance等，都是通过hook Cipher类的相关构造和加解密方法比如SecretKeySpec，IvParameterSpec，doFinal函数等等，只不过Inspeckage在它的initAllHooks给我们集成化了这些东西，其他的文件监控和HTTP请求也是类似的原理，所以Inspeckage这个工具非常方便，但我们应该先通过frida，xposed或者其他的框架了解原理，再来用这个东西集中化测试，不然这个工具简化了大量的操作会让我们很容易陷入只了解工具而不知道原理的尴尬局面。  
附Inspeckage原理介绍[Xposed知多少？](http://www.freebuf.com/column/147856.html)
