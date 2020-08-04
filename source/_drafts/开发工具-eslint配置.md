---
title: 开发工具-eslint配置
comments: true
date: 2020-08-03 21:05:56
tags:
categories:
- 开发工具
---

# 概述

配置方式：
1. js 文件中配置
2. json 对象组织成单独的配置文件

配置内容：
1. Environments - 指定脚本的运行环境。每种环境都有一组特定的预定义全局变量。
2. Globals - 脚本在执行期间访问的额外的全局变量。
3. Rules - 启用的规则及其各自的错误级别。

<!--more-->

# 解析

```js
module.exports = {
  root: true, //默认情况下，ESLint 会在所有父级目录里寻找配置文件，一直到根目录。如果发现配置文件中有 “root”: true，它就会停止在父级目录中寻找。
  env: { // 环境，可同时定义多个
    browser: true,
    node: true
  },
  globals: { // 全局变量，避免在其他文件中引入未定义变量报错。"writable" 允许重写变量。"readonly" 不允许重写变量。"off" 禁用全局变量。
    $: 'readonly',
    var2: 'writable',
    Promise: "off"
  },
  plugins: [ // 配置插件。 使用 plugins 关键字来存放插件名字的列表。插件名称可以省略 eslint-plugin- 前缀
   "plugin1",
   "eslint-plugin-plugin2"
  ],
  extends: [ // 一个配置文件可以被基础配置中的已启用的规则继承
    'plugin:vue/essential',
    '@vue/standard'
  ],
  parserOptions: { // 解析选项
    parser: 'babel-eslint'
  },
  rules: { // 规则。
    // "off" 或 0 - 关闭规则; "warn" 或 1 - 警告。"error" 或 2 - 错误。
    // 数组格式，第一项总是规则的严重程度，后面是规则参数
    // 配置定义在插件中的一个规则的时候，你必须使用 插件名/规则ID 的形式
    'no-console': process.env.NODE_ENV === 'production' ? 'warn' : 'off',
    'no-debugger': process.env.NODE_ENV === 'production' ? 'warn' : 'off',
    'semi': 'off',
    'quotes': ["error", "double"],
    "plugin1/rule1": "error"
  },
  overrides: [ // 若要禁用一组文件中的规则，请使用 overrides 和 files
    {
      files: ["*-test.js","*.spec.js"],
      rules: {
        "no-unused-expressions": "off"
      }
    }
  ]
}

```