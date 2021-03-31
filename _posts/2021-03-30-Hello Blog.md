---
layout: post
title: 'Hello Blog'
date: 2021-03-30
author: lalala
cover: 'http://on2171g4d.bkt.clouddn.com/jekyll-banner.png'
tags: Blog
---

> 带领你亲手搭建专属自己的博客.

## Hello Blog!


带领你搭建个人博客,就像你现在在的博客,这是我的博客.
本人邮箱: wzc520pyf@qq.com

[TOC]

本文所参考的博客:
https://www.zhihu.com/question/20962496

https://zhengqing.blog.csdn.net/article/details/90765491?utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromMachineLearnPai2%7Edefault-9.control&dist_request_id=&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromMachineLearnPai2%7Edefault-9.control

https://blog.csdn.net/whbk101/article/details/102743250?utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7Edefault-8.control&dist_request_id=&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7Edefault-8.control

https://blog.csdn.net/qq_36361250/article/details/89920612?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.control&dist_request_id=&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.control 


**搭建博客**前你需要注册github账号,并了解一些它的基础操作.具体内容可参考我的另一篇博客.

### 0 开始搭建博客
搭建博客首先要登录你的GitHub账号,并在个人主界面里创建一个新的Repository.

![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/github_0.1.png)

进入后在Repository name的位置填写域名:  格式是username.GitHub.io

![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/github_0.2.png)

(因为已创建过同名仓库了,所以报错)

拉到底部:
![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/github_0.3.png)

进入刚刚建好的仓库:
![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/github_0.4.png)

在Setting里找到GitHub Pages
![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/github_0.5.png)

点击这个可以选一个博客主题:
![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/github_0.6.png)

仅作示范,就第一个试试吧:
![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/github_0.7.png)

选择完毕后,GitHub Pages就会自动帮你生成好网站,在它跳转到的页面底端点击Commit changes按钮,网站就可以访问了.  
然后在浏览器里输入你的项目名称,比如:wzc520pyfm.GitHub.io就可以看到你刚刚设置好的网站页面了:
大致是这样(我网上找了个别人的示例图):
![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/github_0.8.png)

你可以去修改index.md文件来自定义博客主页内容:
![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/github_0.9.png)

修改完点击底端的Commit Changes  即可保存修改:

看一下效果:
![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/github2_0.1.png)


### 1   让博客变得漂亮
但现在这个博客页面有点丑.反正就是不满意,我们去整个新的(好看的)
(参考博客: 
 https://zhengqing.blog.csdn.net/article/details/90765491?utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromMachineLearnPai2%7Edefault-9.control&dist_request_id=&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromMachineLearnPai2%7Edefault-9.control)


(当然,博客页面个性化设置的方式有很多,我仅以其中的一种作为示范,更多的方法可以参考这篇:  https://www.zhihu.com/question/20962496 )

我们去Jekyll官网fork一份自己喜欢的博客模板
http://jekyllthemes.org/

![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/github_1.1.png)

附上Jekyll模板网站: Jekyll模板网站：https://github.com/jekyll/jekyll/wiki/Sites

如果你懒得找,你可以直接用我的这个(也是很漂亮的):

https://github.com/kaeyleo/jekyll-theme-H2O

打开后点击Fork, 即可复制一份到自己的github仓库: 
![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/github_1.2.png)

然后点击Setting:
![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/github_1.3.png)

重命名仓库:
格式:  用户名.github.io

然后你就可以访问https://www.wzc520pyfm.github.io/查看效果了.(不会马上生效,这需要一点时间,原因应该是网络问题吧,大概要等3~5分钟才会生效)
(因为我的博客使用了自定义域名,如果你要看的话,需要访问这个地址:
https://www.wzc520pyf.cn/     )
(自定义的域名如何设置在之后讲解)
![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/github_1.4.png)

现在把主页内容进行修改,更具个性化:
(这个修改也不是马上生效,可能需要等待30秒左右)
![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/github_1.5.png)

![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/github_1.6.png)

你可以照猫画虎地进行更改,如果你想了解更多内容,你可以在这里找到答案:
![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/github_1.7.png)

现在你的博客主页已经十分个性化了.


最后, 我们需要知道写好的博客放在哪里:
博客放在_posts文件夹内:
![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/github_1.8.png)

打开可看到三篇模板自带的博客: 
![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/github_1.9.png)

打开第一个来看看:
![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/github2_0.2.png)

点击铅笔图标进入编辑:

每篇博客开头都应有一些头信息: 
![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/github2_0.3.png)


下面的内容可以看出就是熟悉的Markdown标记语法.
PS:  介绍一下, 博客是通过Markdown语法来书写的, 它与word写作相比,更关注写作本身而非排版.
虽说Markdown是一种标记语言, 但不必惊慌,它不能算是编程语言,学起来也非常简单,emmm…预估你10多分钟就能掌握它.

现在你知道博客怎么写了吧.
(当然你可以通过git工具来clone你的博客项目到本地,再在本地进行编辑,然后在推送到github仓库,这才是更好的做法, 关于git操作可以看我的其他博客: 
占位!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
)
推荐一个写博客的神器---马克飞象

马克飞象是一个可实时预览的在线编辑工具而且可实时将所写内容保存到印象笔记里, 十分好用,Markdown语法也可以在这里了解,这是地址: 
https://maxiang.io/


### 2  如何在博客里添加图片
接下来处理写博客时的图片问题,  写博客总难免要放图片吧,当然处理图片的方法也有多种,这里首推  图床  的形式.
图床 :  将图片存放在云端, 在必要的地方引用链接.
具体如何使用,见下文:



### 在GitHub上搭建免费图床:

参考博客: 
 https://blog.csdn.net/whbk101/article/details/102743250?utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7Edefault-8.control&dist_request_id=&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7Edefault-8.control

https://blog.csdn.net/qq_36361250/article/details/89920612?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.control&dist_request_id=&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.control 

用到的工具:  PicGo
PicGo是一款简易的图床上传工具，可以通过拖拽或者复制粘贴的方式将图片上传到图床。
下载地址:
https://github.com/Molunerfinn/PicGo/releases

打开后下拉找到:
![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/github_2.1.png)

如果是windows, 下载上面的exe即可

下载完成后直接安装即可.

现在有了上传工具,  我们还需要去github上建一个图片库:
![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/github_2.2.png)

![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/github_2.3.png)

Repository name  是仓库名,你可以按照图中的填写,也可以填其他的.(因为我已经有一个同名的仓库了,所以会提示错误)
Description是对这个仓库的描述.

滑到页面底端点击绿色按钮Create repository即可创建仓库: 
![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/github_2.4.png)

进入仓库:
![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/github_2.5.png)

输入master新建分支master.(如果你之前没有建过这个分支,下面会提醒你创建分支,创建即可).
切换到master分支:
![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/github_2.6.png)

点击Create new file新建文件(主要目的是新建文件夹)
![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/github_2.7.png)

输入img/

会看到:
![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/github_2.8.png)

这表明我们已经建好了文件夹(文件夹名为img)

现在随便填一个文件名:
![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/github_2.9.png)

拉到底部:
![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/github2_0.5.png)

点击创建即可.

回到刚刚的仓库可以看到:
![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/github2_0.6.png)

Ok,现在打开前面安装好的PicGo(双击打开),打开后的界面如下:
![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/github2_0.7.png)

点击左边的图层设置部分的GitHub图床: 
![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/github2_0.8.png)

仓库名就是刚刚在github建好的仓库:
![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/github2_0.9.png)

分支名就是刚刚在仓库新建的master分支.
指定存储路径就是刚刚在仓库新建的文件夹img
![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/github2_1.0.png)

自定义域名可不填.

最后是Token!
这相当于是一个代替密码验证的密钥,要注意保管,要去github里去建:
![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/github2_1.1.png)

![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/github2_1.2.png)

![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/github2_1.3.png)

![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/github2_1.5.png)

Note是token的名字(便于你知道这个token是被用来干什么的)
记得勾选repo 
![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/github2_1.6.png)

![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/github2_1.7.png)

![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/github2_1.8.png)

这里就是你刚刚建好的token了复制保存好了,页面一旦关闭就再也看不到了.

把刚刚复制的token粘贴到PicGo里:
![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/github2_1.9.png)

点击确定,系统会提醒设置成功.


切换到PicGo的上传区:

![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/github2_2.0.png)

把任意图片拖进来:
![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/github2_2.1.png)


右下角提示成功:
![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/github2_2.2.png)

现在Markdown形式的图片地址就已经在你的剪贴板了.

我们打开马克飞象(前面提到的博客编辑器)网页版,直接右键粘贴来试一下:
![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/github2_2.3.png)


左边即是我们刚刚粘贴进去的内容.

右边是实时预览,可以看到图片已经可以正常显示了.
(因网络原因,图片显示出来可能需要30秒左右)

So,现在你可以愉快地写博客了.


### 3.  图片无法加载(常见问题)
 不幸的是,  当你写完之后,把博客发布到你的gihub后, 你会发现你的图片并不能显示.
这是因为github使用的地址被墙了,   什么?我刚刚折腾那么久才弄好的图床,说不能用就不能用?  这肯定不性,办法还是有的:

**3.1**  
换图床!  Emmm..我…!   举一个其他图床的外链:  https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/import_project.png

**3.2**  
cdn加速(jsDelivrCND官方地址https://www.jsdelivr.com/?docs=gh),对外链稍作修改:
参考示例:
(只是用户名前面的一部分不同,    后面的master前的-改为@)
https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/import_project.png


### 4  为博客绑定自定义域名
还记得在前问提到的自定义域名了吗?  现在来填坑:
(ps:  现在放弃来得及)

现在的GitHub Pages免费为我们的网站提供https服务,这可是帮我们省下了一大笔钱!!!

但首先,你得有一个自己的域名才可以.

域名我是通过腾讯云购买的,

购买好后,进入你的控制台:
![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/github_4.1.png)

添加一条解析记录:
![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/github_4.2.png)

照着填就好,  lalala.GitHub.io就是之前自定义的GitHub Pages域名

DNS解析生效可能需要几分钟,甚至更长

然后回到之前进入过的Setting界面, 找到GitHub Pages的设置,  将你的域名填入
![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/github_4.3.png)

比如我的是  wzc520pyf.cn

记得勾选:
![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/github_4.4.png)

最后成功的话,应该是这样:
![](https://cdn.jsdelivr.net/gh/wzc520pyfm/Picbed_PicGo@master/img/github_4.5.png)

现在输入:  https://www.wzc520pyf.cn 即可访问到博客.


























