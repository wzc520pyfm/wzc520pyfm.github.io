---
layout: post
title: 'charles手机app抓包'
subtitle: '如何利用charles抓取手机app的网络通信数据包?'
date: 2021-11-10
categories: 技术
author: lalala
cover: ''
tags: 调试
---

### Charles如何抓包手机app

[TOC]



#### 安装Charles

1. 首先下载链接

   链接：https://pan.baidu.com/s/1YO7leuxEprZwdMVQuUPuUg 
   提取码：6xdh

2. 安装

   ![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/charlesDown1.png) 

   ![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/charlesDown2.png)

   ![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/charlesDown3.png)

   这里可以修改软件的安装路径，我这里保持默认路径，下一步

   ![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/charlesDown4.png)

   点击 install 等待安装完成

   ![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/charlesDown5.png)

3. 破解Charles

   ![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/charlesFly.png)

   将压缩包内的 charles.jar 复制到安装目录的lib目录下

#### 下载虚拟机

1. 推荐夜神模拟器

   [夜神安卓模拟器-安卓模拟器电脑版下载_安卓手游模拟器_手机模拟器_官网 (yeshen.com)](https://www.yeshen.com/)

#### 抓取http包

1. 配置charles端口号, 默认8888, 并勾选"Enable transparent HTTP proxying", 如下图

   ![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/charlesProxySetting.png)

2. 查看电脑的IP地址: 打开cmd命令行, 输入`ipconfig`, 回车,  找到Ipv4, 如下图

   ![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/charlesPcIpv4.png)

3. 在虚拟机中添加代理: 如下图

   ![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/charlesWLAN1.png) 

   ![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/charlesWLAN2.png)

   代理服务器是运行Charles的电脑IP地址，端口对应着Charles上的配置的代理端口号。

4. Charles上允许代理连接: 此时，手机配置好代理后，访问任意流量都会经过Charles工具，所以Charles工具会弹出如下图所示的提示信息，选择“Allow”，允许即可。

   ![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/charlesAllow.png)

   (PS: 这张图是我网上"借的", 所以你会发现弹出里的ip和我手机里输入的不一致)

5. 手机运行APP，比如柠檬班APP，就可以在Charles上捕获到对应的报文了。

   ![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/charlesHTTP.png)

#### 抓取https包

上面的讲述仅仅可以抓取http的包, 但是现在很多APP都是用的https协议的，所以怎么去抓取并分析https的协议的数据包呢？

1. 在Charles上开启SSL代理: 

   Proxy -> SSL Proxying Settings-->勾选Enable SSL Proxying,点击Add,点击Add，Host设置要抓取的https接口，

   Host : * (使用通配符表示检测所有网络请求；建议还是设置单个需要抓取的https host，尽量避免使用 * 通配符)

   Port：443

   ![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/charlesHTTPS1.png)

2. 手机端安装Charles证书

   点击SSL Proxying --> Install Charles Root Certificate on a Mobile Device or Remote Browser,会提示你如何在手机端配置代理以及安装证书：

   ![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/charlesHTTPS2.png)

   如下图所示：手机代理配置192.168.1.189（我电脑的IP地址），端口为8888（Charles配置的代理端口）：

   ![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/charlesHTTPS3.png)

   手机端浏览器里输入chls.pro/ssl网址，然后允许下载证书；并下载完成后去`设置->安全`里查看证书；

   ![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/charlesHTTPS4.png) 

   ![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/charlesHTTPS5.png) 

   ![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/charlesHTTPS6.png)

   (PS: 安装证书可以会先要求你设置锁屏密码, 直接选PIN码设置下就好了, 安装好后可以在`用户凭据`里看到)

3. 安装完成, 现在charles就可以抓到手机app的https包了

