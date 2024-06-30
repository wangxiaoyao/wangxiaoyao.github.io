---
layout: single
title: "github.io搭建博客"
date: 2024-06-27
categories: [图床, 域名, ruby, jekyll]
---

## 一 本地配置

### 1 安装配置软件

```shell
## ruby: 舍弃mac自带。通过brew安装。
brew install ruby

## 解决mac自带与brew冲突：将brew安装的活动版本bin文件指向$PATH. 
echo 'export PATH="/usr/local/opt/ruby/bin:$PATH"' >> ~/.zshrc

## brew管理多版本：即切换版本。但是当前活动版本永远指向：`/usr/local/opt/ruby/bin`.
brew unlink ruby@3.1.0
brew link --force --overwrite ruby@3.3.3

## brew安装源文件在 /usr/local/Cellar. 但是会自动生成软连接在：/usr/local/opt

## ruby软件来自哪里
which ruby
```

关系：

- ruby ：语言（类似js）
- RubyGems（gem）：ruby包管理器（类似npm）。其中 jekyll 就是其中一个包。
- bundler：管理项目的gem



### 2 博客软件 jekyll

> 全局安装 jekyll会造成：版本依赖冲突。（在mac的lib库，查看： `bundle show jekyll` ）
>
> 以下局部安装（隔离依赖）：1 不同环境，相同的gem版本。 2 同一环境，避免不同软件版本冲突。

```shell
## 创建文件夹blog
mkdir blog
cd blog

## 安装bundler：ruby项目包管理器。并创建Gemsfile文件作为其配置文件。
## 注意：gem包：'github-pages'。包含了运行jekyll的很多插件。 [参见](https://github.com/github/pages-gem) 
gem install bundler
vim Gemsfile

## 局部安装：通过bundle安装并控制依赖。操作前缀：`bundle exec`：告诉ruby执行的项目依赖为自动生成的文件Gemsfile.lock
bundle install

## 查看局部安装的gem软件包.以及删除非Gemsfile上的包
bundle exec gem list
bundle clean

## 在blog文件夹使用：jekyll生成博客文件夹名为：jekyllBlog。（后续并将jekyllBlog所有内容复制到blog里。删除jekyllBlog文件夹）
bundle exec jekyll new jekyllBlog

## 查看jekyll版本,并本地运行jekyll
bundle exec jekyll -v
bundle exec jekyll serve
```



全局安装的gem 清洗。

```
## Gemsfile文件
source 'https://rubygems.org'

gem 'github-pages', group: :jekyll_plugins
gem 'webrick', '~> 1.7', require: false
```



##  二 github配置

[参见官方配置文档](https://docs.github.com/zh/pages/quickstart)



## 三 配置 jekyll

### 1 [选择主题：minimal-mistakes](https://github.com/mmistakes/minimal-mistakes)

> 注意点：使用主题：minimal-mistakes， 在github action的build和deploy部署的过程中。出现无法找到：minimal-mistakes情况而构建失败。解决办法：_config.yml中的theme设置为remote theme。详见： [配置remote主题]https://github.com/mmistakes/minimal-mistakes#remote-theme-method)。

[主题配置](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/)


### 2 图床
配置cloudfare




### 3 域名
配置cloudfare




