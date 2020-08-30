---
title: 前端基础-npm包相关知识
comments: true
tags:
  - npm
categories:
  - 前端基础
date: 2020-08-24 20:45:28
---


# npm

npm 是世界上最大的软件注册表。全世界的开源开发人员都使用 npm 共享和借用软件包，许多组织也使用 npm 来管理私人开发。

npm 包含三个不同的组件：

* npm 网站：用与搜索 npm 包，注册账号，管理你的 npm 包。
* CLI 工具：开发者用得最多的命令行工具。
* 注册表(registry)：大型的 JavaScript 软件公共数据库及其周边的元信息。

## 常用 CLI 命令

[CLI 命令汇总文档](https://docs.npmjs.com/cli-documentation/cli)

* `npm init`：创建 npm 包。
* `npm install`：安装包。别名：npm i, npm add。
* `npm uninstall`：卸载包。别名：remove, rm, r, un, unlink。
* `npm run <script name>`：运行 scripts 配置内容。
* `npm version <new version>`：更新包的版本号。
* `npm update`：更新包。别名：up, upgrade。


## package.json 文件

[package-json 文档](https://docs.npmjs.com/configuring-npm/package-json.html)

* `name`[必选]：包名，必须为小写和一个单词，并且可能包含连字符和下划线。
* `version`[必选]：版本号，x.x.x 格式，符合[语义化版本规范](https://docs.npmjs.com/about-semantic-versioning)。
* `description`：包描述，一段文字。
* `keywords`：关键词，字符串数组。
* `homepage`：主页地址，一段 url 链接。
* `bugs`：bug 地址。
* `license`：版权。
* `author`：作者。
* `contributors`：贡献者。
* `funding`：资助者。
* `files`：描述了将软件包作为依赖项安装时要包括的文件类型。
* `main`：包的入口文件。当引入一个包时，main文件导出的内容将作为包的入口。
* `browser`：客户端使用，browser 替代 main 作为入口。
* `bin`：一些包包含了要引入环境的可执行文件。
* `man`：指定要放置的单个文件或文件名数组，以供man程序查找。
* `directories`：CommonJS Packages规范详细介绍了几种可以使用目录对象指示软件包结构的方法。
* `repository`：指定代码所在的位置。
* `scripts`：运行脚本。
* `config`：script 脚本的配置。
* `dependencies`：项目依赖。安装方式：npm i <package-name> or npm i <package-name> -S or npm i <package-name> [--save-prod]。
* `devDependencies`：开发依赖。安装方式： npm i <package-name> -D or npm i <package-name> --save-dev。
* `peerDependencies`：前置库，如编写一个 jquery 插件，它的前置库是 jquery。
* `bundledDependencie`：这定义了一组软件包名称，这些名称将在发布软件包时捆绑在一起。执行 npm pack 可以将其打包到一起。
* `optionalDependencies`：可选的依赖。
* `engines`：指定 node 版本。
* `os`：操作系统。
* `cpu`：cpu 信息。
* `private`：是否私有。
* `publishConfig`：发布配置项。

## 语义化版本号(semantic versioning)

[关于语义化版本号](https://docs.npmjs.com/about-semantic-versioning)


## 参考文档

* [npm](https://www.npmjs.com/)
* [npm 模块安装机制简介](https://www.ruanyifeng.com/blog/2016/01/npm-install.html)
* [npm scripts 使用指南](https://www.ruanyifeng.com/blog/2016/10/npm_scripts.html)
* [使用 npm 的语义版本控制](http://nodejs.cn/learn/semantic-versioning-using-npm)