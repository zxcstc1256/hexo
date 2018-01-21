---
title: 使用 hexo 和 github 搭建博客
date: 2017-11-19 16:54:11
tags:
---
# 安装node
自动忽略 windows 系统，在 mac 系统下使用 brew 安装 node
``` bash
brew install node
```
_[如何安装brew](https://brew.sh)_
# 安装hexo
``` bash
npm install -g hexo 
```
# 生成hexo项目
``` bash
hexo init [folder]
```
新建一个网站。如果没有设置 `folder` ，Hexo 默认在目前的文件夹建立网站。
# 发布一篇新文章
``` bash
hexo new [layout] <title>
```
新建一篇文章。如果没有设置 `layout` 的话，默认使用 [_config.yml](https://hexo.io/zh-cn/docs/configuration.html) 中的 default_layout 参数代替。如果标题包含空格的话，请使用引号括起来。
# 生成静态页面
``` bash
hexo generate
```
| 选项 | 描述 |
| :--- | :--- | 
| -d, --deploy | 文件生成后立即部署网站 |
| -w, --watch | 监视文件变动 |
该命令可以简写为
``` bash
hexo g
```
# 发布
``` bash
hexo publish [layout] <filename>
```
# 预览
``` bash
hexo server
```
| 选项 | 描述 |
| :--- | :--- | 
| -p, --port | 重设端口 |
| -s, --static | 只使用静态文件 |
| -l, --log | 启动日记记录，使用覆盖记录格式 |
# 配置github
当然，首先需要注册 [GitHub](https://www.github.com) 账号，然后在 hexo 项目目录下找到 _config.yml，配置如下内容：
``` yml
deploy:
  type: git
  repo: git@github.com:[your account name]/[your repository].git
  branch: master
```
# 发布到github
``` bash
hexo deploy
```
# 生成博客链接
在 github 找到你博客对应的 repository，到Settings下找到 GitHub Pages，配置 master branch 为 GitHub Pages，会看到Your site is published at https://<your account>.github.com/<your repository>，该链接即博客主页地址。
# 绑定自己的域名
在域名商的 DNS 解析中配置cname，然后在上一步的配置中，找到Custom domain，填上自己的域名。
[参考文档](https://help.github.com/articles/using-a-custom-domain-with-github-pages/)
