---
title: 使用hexo+github搭建个人博客
date: 2023-01-11 00:12:56
tags: 工具
categories: 配置教程
index_img: https://agust.oss-cn-guangzhou.aliyuncs.com/images/202301110055221.png
banner_img: https://agust.oss-cn-guangzhou.aliyuncs.com/images/202301110055221.png
---

# 配置使用环境

## 安装npm

## 安装git

## 配置Github pages





## 一键部署hexo

1.安装 hexo-deployer-git

```sh
npm install hexo-deployer-git --save
```

2.修改配置

```sh
deploy:
  type: git
  repo: <repository url> # github pages 仓库地址
  branch: [branch] # 分支名称 gh-pages (GitHub) 、coding-pages (Coding.net) 、master (others)
  message: [message] # 自定义提交信息
```

3.执行 `hexo clean && hexo deploy`，生成站点文件并推送至远程库。

4.登入 Github，在库设置（Repository Settings）中将默认分支设置为`_config.yml`配置中的分支名称。稍等片刻，您的站点就会显示在您的Github Pages中。





## 设置hexo支持Latex公式

网页上对`Latex`的支持需要借助能够解析`Latex`语法的插件引擎，将`Latex`语法转成`HTML`元素，常用的`Latex`公式引擎有`Katex`,`mathjax`引擎等，如CSDN使用的就是`Katex`，我们选择`mathjax`，这样渲染的公式更加好看。



1.删除原有的渲染引擎

```
npm uninstall hexo-renderer-marked
```



2.渲染引擎改成pandoc

```
npm install hexo-renderer-pandoc
```



3.安装mathjax插件

```
npm install hexo-filter-mathjax
```



4.修改站点`_config.yaml`文件，注意不是`themes`中的`_config.yaml`

```yaml
mathjax:
  tags: none # or 'ams' or 'all'
  single_dollars: true # enable single dollar signs as in-line math delimiters
  cjk_width: 0.9 # relative CJK char width
  normal_width: 0.6 # relative normal (monospace) width
  append_css: true # add CSS to pages rendered by MathJax
  every_page: false # if true, every page will be rendered by MathJax regardless the `mathjax` setting in Front-matter
```



5.在需要使用latex的页面`.md`头部加入`mathjax: true`







