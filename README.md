# myblog

## 命令

[文档地址](https://hexo.io/zh-cn/docs/)

```bash
# 安装
$ npm install -g hexo-cli

# 建站
$ hexo init <folder>
$ cd <folder>
$ npm install

# 启动本地服务
$ hexo server

# 新建文章
$ hexo new [layout] <title>

# 生成静态文件
$ hexo generate

# 部署
$ hexo g -d
$ hexo d -g

# 清理
# 清除缓存文件 (db.json) 和已生成的静态文件 (public)。
$ hexo clean

```

## 分类

规则：大类不超过 6 类，级别不超过 2 层，大类优先级最高。

* 前端基础
  * HTML
  * CSS
  * JavaScript
  * HTTP
* 可视化
  * 算法
  * 2D
  * 3D
  * GIS
* 数据结构与算法
* 专题
  * 性能优化
  * 一周拾遗
* 开发工具
  * GIT
  * VSCODE
* 其他

## ISSUE

* 文章加 ```<!--more-->``` 是截取摘要部分
* 引入图片 `{% asset_img 1.jpg 主线程和合成线程 %}`
