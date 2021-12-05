### node

查看node版本:  node -v

如何运行node.js程序:  node 文件名.js

如何进入node命令交互模式:  输入命令: node

输入待执行语句(例如console.log("Hello World");)

如何退出node命令交互模式: 两次: Ctrl+C

Npm:

查看版本:npm -v

版本升级: npm install npm -g

安装 Node.js 模块语法格式: npm install <Module Name>

安装好模块后如何使用: var express = require('express');

安装分全局与本地:

npm install express     # 本地安装

npm install express -g  # 全局安装

可能的错误:

npm err! Error: connect ECONNREFUSED 127.0.0.1:8087

解决办法:

npm config set proxy null

更多信息参考: https://www.runoob.com/nodejs/nodejs-npm.html

卸载模块:

npm uninstall express

检查包是否存在: npm ls

更新模块: npm update express

搜索模块: npm search express

创建模块参考: https://www.runoob.com/nodejs/nodejs-npm.html

NPM常用命令:

NPM提供了很多命令，例如install和publish，使用npm help可查看所有命令。

使用npm help <command>可查看某条命令的详细帮助，例如npm help install。

在package.json所在目录下使用npm install . -g可先在本地安装当前命令行程序，可用于发布前的本地测试。

使用npm update <package>可以把当前目录下node_modules子目录里边的对应模块更新至最新版本。

使用npm update <package> -g可以把全局安装的对应命令行程序更新至最新版。

使用npm cache clear可以清空NPM本地缓存，用于对付使用相同版本号发布新版本代码的人。

使用npm unpublish <package>@<version>可以撤销发布自己发布过的某个版本代码。

使用淘宝npm镜像:

```
npm install -g cnpm --registry=https://registry.npm.taobao.org
cnpm install [name]
```

 

### node安装模块报错

首先安装命令是:   npm install multer(multer是模块名)

如果报错,如下操作:

第一步还是：npm cache clean --force
npm cache clean --force
第二步：切换为淘宝镜像
npm config set registry https://registry.npm.taobao.org/
npm config get registry https://registry.npm.taobao.org/
验证时候切换淘宝镜像成功，命令行输入: npm config list


参考原博客网址:https://blog.csdn.net/zsl15039718107/article/details/104128166/

### 新建Express项目报错

执行 

npm cache clean --force
即可解决npm install出现”Unexpected end of JSON input while parsing near”错误。

文章参考来源：https://blog.csdn.net/wyhux/article/details/78041513

以上是个人操作。网上具体操作如下：

1、如果你的项目里存在 package-lock.json 文件，删除它。并且删除 node_modules。然后再 npm install。

2、第一步不行的话。运行 npm cache clean --force 或者 npm cache verify 。然后再 npm install。

3、如果上面的都不行，就升级 npm 。 npm i -g npm

