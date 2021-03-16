---
layout: post
title: my-first-post
date: 2021-03-16 21:48:23 +0900
category: jekyll
---
# jekyll初次使用体验
> 跟着网上的教程乱七八糟的，终于搭好了自己的博客。
> 感谢少数派的教程，感谢jekyllThemes大佬们的贡献，
> 感谢jekyll官网的文档指点。
> 在本次搭建博客的过程中，遇到了几个比较坑的问题，
> 附上问题和解决办法。

### 问题及解决办法
>Q1:jekyll command not find<br>
>A1:参考jekyll官网，给出的解决方案是：<br>
在终端环境配置文件中(example:zshrc)添加环境变量<br>
export GEM_HOME=$HOME/gems<br>
export PATH=$HOME/gems/bin:$PATH<br>
> 添加完成后重新执行gem install jekyll命令即可<br>
> Q2:Error cannot load such file --webrick(LoadError)<br>
> A2:在博客项目文件夹下执行命令bundle add webrick<br>
> Q3：配置问题<br>
> A3:这是个细心活，缺少相关依赖，终端中gem安装缺少的包，在博客模板项目配置文件中注意版本号相匹配

# Note
> 1.尽量避免sudo gem XXX 的方式<br>
> 2.参考清华大学开源镜像站更改ruby国内源，加快下载速度<br>
> <a>https://mirrors.tuna.tsinghua.edu.cn/help/rubygems/