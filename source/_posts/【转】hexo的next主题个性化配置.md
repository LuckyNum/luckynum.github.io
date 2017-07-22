---
title: 【转】hexo的next主题个性化配置（一）
date: 2017-06-22 19:26:13
categories: 博客
tags:
    - hexo
    - 主题美化
toc: true
---
[原文](https://segmentfault.com/a/1190000009544924)

看到有些next主题的网站很炫酷，那么是怎么配置的呢？接下来我会讲一讲如何实现一些炫酷的效果看到有些next主题的网站很炫酷，那么是怎么配置的呢？接下来我会讲一讲如何实现一些炫酷的效果。
<!-- more -->



## 1. 在右上角或者右下角实现fork me on github

### 实现效果图
![Markdown](http://i4.piimg.com/1949/adaf6afa2fca8d17.jpg)
### 具体实现方法
点击[这里](https://github.com/blog/273-github-ribbons) 挑选自己喜欢的样式，并复制代码。例如，我是复制如下代码：
![Markdown](http://i4.piimg.com/1949/b36ac9cf034f5a49.jpg)
然后粘贴刚才复制的代码到 themes/next/layout/_layout.swig 文件中(放在`<div class="headband"></div>`的下面)，并把 href 改为你的github地址。
```html
<div class="headband">
    <!-- 左上角 fork me on github -->
    <a href="https://github.com/luckynum">
        <img style="position: absolute; top: 0; left: 0; border: 0;" src="https://camo.githubusercontent.com/567c3a48d796e2fc06ea80409cc9dd82bf714434/68747470733a2f2f73332e616d617a6f6e6177732e636f6d2f6769746875622f726962626f6e732f666f726b6d655f6c6566745f6461726b626c75655f3132313632312e706e67" alt="Fork me on GitHub" data-canonical-src="https://s3.amazonaws.com/github/ribbons/forkme_left_darkblue_121621.png">
    </a>
</div>
```

## 2.添加RSS
NexT5.1.1版本后，参考[这里](http://theme-next.iissnan.com/theme-settings.html)
### 实现效果图
![Markdown](http://i4.piimg.com/1949/fea73b8781bba3ac.jpg)
### 具体实现方法
切换到你的blog（我是取名blog，具体的看你们的取名是什么）的路径，例如我是在`/Users/chenzekun/Code/Hexo/blog`这个路径上，也就是在你的根目录下。
然后安装 Hexo 插件：(这个插件会放在 node_modules 这个文件夹里)
```bash
$ npm install --save hexo-generator-feed
```
然后打开hexo的配置文件`_config.yml`，在里面的末尾添加：( 请注意 在冒号后面要加一个空格，不然会发生错误！)
```xml
# Extensions
## Plugins: http://hexo.io/plugins/
plugins: hexo-generate-feed
```
然后打开next主题文件夹里面的`_config.yml`,在里面配置为如下样子：(就是在 rss: 的后面加上`/atom.xml`, 注意 在冒号后面要加一个空格)
```xml
# Set rss to false to disable feed link.
# Leave rss as empty to use site's feed link.
# Set rss to specific value if you have burned your feed already.
rss: /atom.xml
```
配置完之后运行：
```bash
$ hexo g
```
重新生成一次，你会在`./public` 文件夹中看到`atom.xml` 文件。然后启动服务器查看是否有效，之后再部署到 Github 中。
## 3. 添加动态背景
版本<5.1.0详情点击[`博客`](http://shenzekun.cn/hexo%E5%A6%82%E4%BD%95%E6%B7%BB%E5%8A%A0%E5%8A%A8%E6%80%81%E8%83%8C%E6%99%AF.html)

版本>=5.1.0详情点击[`官方配置`](http://theme-next.iissnan.com/theme-settings.html)
## 4. 实现点击出现桃心效果
在网址输入或直接点击[`http://7u2ss1.com1.z0.glb.clouddn.com/love.js`](http://7u2ss1.com1.z0.glb.clouddn.com/love.js)
然后将里面的代码copy一下，新建`love.js`文件并且将代码复制进去，然后保存。将`love.js`文件放到路径`/themes/next/source/js/src`里面，然后打开 `\themes\next\layout\_layout.swig`文件,在末尾（在前面引用会出现找不到的bug）添加以下代码：
```html
<!-- 页面点击小红心 -->
<script type="text/javascript" src="/js/src/love.js"></script>
```
## 5. 修改文章内链接文本样式
### 实现效果图
![Markdown](http://i2.muimg.com/1949/d1fd62276312ab66.jpg)
### 具体实现方法
修改文件`themes\next\source\css\_common\components\post\post.styl`，在末尾添加如下css样式：
```html
// 文章内链接文本样式
.post-body p a{
  color: #0593d3;
  border-bottom: none;
  border-bottom: 1px solid #0593d3;
  &:hover {
    color: #fc6423;
    border-bottom: none;
    border-bottom: 1px solid #fc6423;
  }
}
```
其中选择`.post-body`是为了不影响标题，选择`p` 是为了不影响首页“阅读全文”的显示样式,颜色可以自己定义。

## 6. 修改文章底部的那个带#号的标签
修改模板`/themes/next/layout/_macro/post.swig`，搜索`rel="tag">#`，将`#`换成`<i class="fa fa-tag"></i>`

