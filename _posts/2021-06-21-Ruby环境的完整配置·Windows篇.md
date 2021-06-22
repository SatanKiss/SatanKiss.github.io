---
layout: post
title: Ruby环境的完整配置·Windows篇
date: 2021-06-21 15:58:00 +0900
category: windows
---

>### 撰写缘由
> 笔者需要在Windows环境上顺利部署本人的GithubPage，以便对现阶段个人所拥有的技术能力做汇总提升。
> ### 准备工作
> - 1 必备安装包(单击链接即可下载)
>   -  ① [RubyInstaller](https://github-releases.githubusercontent.com/78153411/875c4880-a15b-11eb-9f3a-7e769896fdc6?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAIWNJYAX4CSVEH53A%2F20210621%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20210621T061856Z&X-Amz-Expires=300&X-Amz-Signature=2a74a34007b45decd94d53dd0e5b3369b63eca951deb9df38110cc50db2e30d6&X-Amz-SignedHeaders=host&actor_id=62662264&key_id=0&repo_id=78153411&response-content-disposition=attachment%3B%20filename%3Drubyinstaller-3.0.1-1-x64.exe&response-content-type=application%2Foctet-stream)
>    - ② [MSYS2 Installer](https://repo.msys2.org/distrib/x86_64/msys2-x86_64-20210604.exe)  
> - 2 必备网站
>    - ① [MSYS 官网](https://www.msys2.org/)  
>    - ② [MSYS2 国内源使用帮助](http://mirrors.ustc.edu.cn/help/msys2.html)
>  - 2 环境变量配置
>    - 安装ruby之后请将ruby安装文件夹下的bin文件夹添加至Windows系统环境变量的Path中。
> - 3 后续完善步骤
>   - ① 更改MSYS2为国内源，详情参考MYS2 国内源使用帮助。
>   - ② 根据MSYS2 官网执行后续命令
>   - ③ 将自己的githubpage项目克隆到本地，用自己喜欢的IDE打开，在终端中依次执行:
> ```
> gem install jekyll bundler 
> bundle install
> bundle exec jekyll serve
>```  
> 执行完毕即可  
>
> ### 感谢名单
> - [Jekyll 官网](http://jekyllcn.com/)
> - [MSYS2 官网](https://www.msys2.org/)
> - [Ruby 官网](https://www.ruby-lang.org/zh_cn/)
> - [USTC 开源镜像站](https://mirrors.ustc.edu.cn/)