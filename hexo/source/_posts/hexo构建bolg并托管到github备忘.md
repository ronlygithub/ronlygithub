---
title: Hexo加Github搭建个人Blog
date: 2019-06-06 17:25:35
tags: hexo
categories: 工具
---

近几天使用hexo及github搭建了个人blog，现将流程记录下来以作备忘。
### 准备工作
  #### Hexo
  ##### Hexo是什么 
  Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。
  - 支持Markdown，无需关注页面排版
  - 超快速度，Node.js 所带来的超快生成速度，让上百个页面在几秒内瞬间完成渲染。
  - 一键部署，只需一条指令即可部署到 GitHub Pages, Heroku 或其他网站。
  - 插件丰富，Hexo 拥有强大的插件系统，安装插件可以让 Hexo 支持 Jade, CoffeeScript。
##### Hexo 安装
  安装前请确保本地已安装Git及Nodejs.

  执行以下命令，安装Hexo：
  `npm install -g hexo-cli`

##### 本地部署
将`<folder>` 替换为本地储存Blog相关资源的文件夹名称，进行初始化。
``` 
    hexo init <folder>
    cd <folder>
    npm install
```
上述命令执行结束后，`<foler>`文件夹下目录结构如下所示：
```
    .
    ├── _config.yml
    ├── node_modules
    ├── package-lock.json
    ├── package.json
    ├── scaffolds
    ├── source
    └── themes
```



