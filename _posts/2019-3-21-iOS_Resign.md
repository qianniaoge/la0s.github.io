---
layout: post
title: iOS重打包绕过签名校验防护
key: 20150103
tags: iOS Reverse
excerpt_separator: <!--more-->
---
还是上篇文章里那个有反调试的APP，我们这里来试一下静态patch的方法，也就是重打包的方法。一般来说iOS重打包有两种方法：  
第一种方法：直接使用Cydia Impactor使用开发者签名安装即可，这种情况下不会修改APP的BundleID（推荐）<!--more-->
![](https://raw.githubusercontent.com/la0s/la0s.github.io/master/screenshots/20190321.1.png)

第二种方法：先使用iOS App Signer手动签名
![](https://raw.githubusercontent.com/la0s/la0s.github.io/master/screenshots/20190321.2.png)
然后使用mobiledevice install_app ~/Downloads/*.ipa 命令安装
![](https://raw.githubusercontent.com/la0s/la0s.github.io/master/screenshots/20190321.3.png)
但是这种情况下会把自己的签名覆盖APP的BundleID，有可能会导致异常

针对于这个APP的ptrace反调试，直接使用Keypatch插件Nop掉sub_10004FF4C函数即可，然后Edit -> Patch program -> Apply patches to input file替换掉二进制文件即可
![](https://raw.githubusercontent.com/la0s/la0s.github.io/master/screenshots/20190321.4.png)

重新压缩成IPA文件，使用Cydia Impactor安装，但是一运行应用闪退了，这说明应用做了签名校验，一般来说iOS开发会用exit函数退出应用，直接找到_exit的调用者
![](https://raw.githubusercontent.com/la0s/la0s.github.io/master/screenshots/20190321.5.png)

一个很明显的OC函数[XYAppIdentifierManager appIdentifierWithOrganizationId:]，查看此函数
![](https://raw.githubusercontent.com/la0s/la0s.github.io/master/screenshots/20190321.6.png)

修改指向退出流程的跳转指令CBNZ -> CBZ，再重新打包应用就不会闪退了
![](https://raw.githubusercontent.com/la0s/la0s.github.io/master/screenshots/20190321.7.png)


