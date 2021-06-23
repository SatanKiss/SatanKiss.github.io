---
layout: post
title: Tomcat基于APR的调优
date: 2021-06-22 15:58:00 +0900
category: linux
---

> ### 撰写缘由
> &emsp;&emsp;笔者Java开发菜鸟一枚，由于项目基本使用Tomcat容器，部署过程中查看tomcat日志经常会发现warning提示开启APR，之前在mac操作系统上成功开启过，如今换用CentOS，需要重新部署一下，故此记录一下开启过程，避免以后需要的时候频繁去网上找轮子。
> ### 准备工作
> - Ⅰ. 相关源码包(如无特殊说明此处源码包格式一律以tar.gz格式结尾)
   - 1.1 jdk源码包，笔者使用的是jdk1.8最新版本，由于Oracle JDK旧版本需要自行注册Oracle账号并去官网下载，故此处不放下载链接。
   - 1.2 tomcat core 任意版本，此处以 [tomcat8](https://mirrors.tuna.tsinghua.edu.cn/apache/tomcat/tomcat-8/v8.5.68/bin/apache-tomcat-8.5.68.tar.gz) 为例
   - 1.3 tomcat APR系列，请移步此 [网站](https://mirrors.ustc.edu.cn/apache/apr/) ，下载apr、apr-iconv、apr-util源码包。请移步此 [网站](https://mirrors.ustc.edu.cn/apache/tomcat/tomcat-connectors/native/1.2.30/source/) 下载tomcat-native源码包。
> - Ⅱ. 常用编译命令
   - 2.1 ```tar zxvf XXX.tar.gz``` (解压缩源码包命令)
   - 2.2 ```./configure XXX``` (编译安装命令)

> ---
> ### 开始操作
> - Ⅰ. 环境准备
>   - 由于本次调优操作基于源码编译安装APR动态库，理论上Linux操作系统通用，前提是操作系统有必备的编译环境如gcc、make、openssl等编译依赖。
> - Ⅱ. 实操
>   - 2.1 为了便于安装动态库，本次操作以```/usr/local/```目录下为例，假设在该目录下已经准备好了如上所说的源码包。使用```tar zxf XXX.tar.gz```命令解压，并设置好相应的jdk环境变量。
>   - 2.2 以下操作采取纯命令记录。<br />
> 
    yum install -y openssl openssl-devel gcc make #安装相关依赖,非CentOS请自行用其他包管理命令替代<br>
    tar zxf jdk-8u291-linux-x64.tar.gz #解压jdk源码包,设置jdk环境变量请自行移步各大搜索引擎  <br>
    tar zxf apache-tomcat-8.5.68.tar.gz #解压tomcat core 源码包<br>
    tar zxf apr-1.7.0.tar.gz #解压apr源码包<br>
    tar zxf apr-iconv-1.2.2.tar.gz #解压apr-iconv源码包<br>
    tar zxf apr-util-1.6.1.tar.gz #解压apr-util源码包<br>
    tar zxf tomcat-native-1.2.30-src.tar.gz #解压tomcat-native源码包<br>
    cd apr-1.7.0<br>
    ./configure --prefix=/usr/local/apr<br>
    make<br>
    make install #从cd到make install实现了对apr的安装<br>
    cd apr-iconv-1.2.2<br>
    ./configure --prefix=/usr/local/apr-iconv --with-apr=/usr/local/apr<br>
    make && make install #实现对apr-iconv的安装<br>
    cd apr-util-1.6.1<br>
    ./configure --prefix=/usr/local/apr-util --with-apr=/usr/local/apr --with-apr-iconv=/usr/local/apr-iconv/bin/apriconv<br>
    make && make install #实现对apr-util的安装<br>
    cd tomcat-native-1.2.30<br>
    ./configure --with-ssl --with-apr=/usr/local/apr --with-java-home=/usr/local/jdk1.8.0_291<br>
    make && make install # 实现对tomcat-native的安装<br>
    vim ~/.zshrc #添加环境变量，由于笔者默认使用zsh，故在此添加<br>
    export LD_LIBRARY_PATH=/usr/local/apr/lib:$LD_LIBRARY_PATH<br>
    source ~/.zshrc<br>
>   - 2.3 重启tomcat服务，查看日志发现不再提示找不到基于APR的Apache Tomcat Native库，它可以在生产环境中实现最佳性能，大功告成。

---

> ### 感谢名单
> - [centos 7 Tomcat 8.5 的安装及生产环境的搭建调优](https://www.cnblogs.com/busigulang/articles/8529719.html)
> - 各大搜索引擎
> - 若本文内容有不足之处，请移步网络查询解决办法。


    
