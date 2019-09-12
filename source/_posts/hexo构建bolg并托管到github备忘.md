---
title: Hexo加Github搭建个人Blog
date: 2019-06-06 17:25:35
tags: hexo
categories: 工具
---

近几天使用hexo及github搭建了个人blog，现将流程记录下来以作备忘。


  ### Hexo是什么 
  Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。
  - 支持Markdown，无需关注页面排版
  - 超快速度，Node.js 所带来的超快生成速度，让上百个页面在几秒内瞬间完成渲染。
  - 一键部署，只需一条指令即可部署到 GitHub Pages, Heroku 或其他网站。
  - 插件丰富，Hexo 拥有强大的插件系统，安装插件可以让 Hexo 支持 Jade, CoffeeScript。

### Hexo 安装
  安装前请确保本地已安装Git及Nodejs.

  执行以下命令，安装Hexo：
  `npm install -g hexo-cli`


### 本地部署

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

#### 编译生成静态文件
```
hexo generate 或 hexo g
```

#### 运行本地服务
```
hexo server 或 hexo s
```
 在浏览器中访问localhost:4000 即可看到效果

 #### 清空生成文件
 ```
 hexo clean
 ```

 #### 构建并部署到GitHub Pages
 ```
 hexo g -d
 ```

 ### 将Blog 关联到GitHub Pages
 #### 创建远程仓库: `<githubUserName>.github.io`，将`<githubUserName>`替换为你的github账号。远程仓库命名必须遵循此格式，否则无法访问。

### 文章中展示图片
#### 安装插件：
```
npm install hexo-asset-image --save
```
#### 替换 JS 代码
将 `node_modules\hexo-asset-image\index.js` 文件中内容替换为如下代码:
```js
'use strict';
var cheerio = require('cheerio');

// http://stackoverflow.com/questions/14480345/how-to-get-the-nth-occurrence-in-a-string
function getPosition(str, m, i) {
  return str.split(m, i).join(m).length;
}

var version = String(hexo.version).split('.');
hexo.extend.filter.register('after_post_render', function (data) {
  var config = hexo.config;
  if (config.post_asset_folder) {
    var link = data.permalink;
    if (version.length > 0 && Number(version[0]) == 3)
      var beginPos = getPosition(link, '/', 1) + 1;
    else
      var beginPos = getPosition(link, '/', 3) + 1;
    // In hexo 3.1.1, the permalink of "about" page is like ".../about/index.html".
    var endPos = link.lastIndexOf('/') + 1;
    link = link.substring(beginPos, endPos);

    var toprocess = ['excerpt', 'more', 'content'];
    for (var i = 0; i < toprocess.length; i++) {
      var key = toprocess[i];

      var $ = cheerio.load(data[key], {
        ignoreWhitespace: false,
        xmlMode: false,
        lowerCaseTags: false,
        decodeEntities: false
      });

      $('img').each(function () {
        if ($(this).attr('src')) {
          // For windows style path, we replace '\' to '/'.
          var src = $(this).attr('src').replace('\\', '/');
          if (!/http[s]*.*|\/\/.*/.test(src) &&
            !/^\s*\//.test(src)) {
            // For "about" page, the first part of "src" can't be removed.
            // In addition, to support multi-level local directory.
            var linkArray = link.split('/').filter(function (elem) {
              return elem != '';
            });
            var srcArray = src.split('/').filter(function (elem) {
              return elem != '' && elem != '.';
            });
            if (srcArray.length > 1)
              srcArray.shift();
            src = srcArray.join('/');
            $(this).attr('src', config.root + link + src);
            console.info && console.info("update link as:-->" + config.root + link + src);
          }
        } else {
          console.info && console.info("no src attr, skipped...");
          console.info && console.info($(this));
        }
      });
      data[key] = $.html();
    }
  }
});

```

#### MarkDown语法插入图片
`![示例图片](./images/image.png)`

    



