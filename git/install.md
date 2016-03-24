# Git的安装教程
安装最新版的Git。官网教程写的非常详细啦。下面是我的简化版，只有Linux平台上编译与安装的操作步骤。win平台只需下载安装程序直接安装即可。
> [官方安装教程](https://git-scm.com/book/zh/v2/%E8%B5%B7%E6%AD%A5-%E5%AE%89%E8%A3%85-Git)（推荐）
> win平台下载：[https://git-scm.com/downloads](https://git-scm.com/downloads)
> 源码下载：[https://www.kernel.org/pub/software/scm/git](https://www.kernel.org/pub/software/scm/git) 或 [https://github.com/git/git/releases](https://github.com/git/git/releases)

## 用yum编译并安装Git
- 下载Git源码
```
$ wget https://github.com/git/git/archive/v2.7.4.tar.gz
```

- 配置需要的编译环境
```
$ sudo yum install curl-devel expat-devel gettext-devel openssl-devel zlib-devel
$ sudo yum install asciidoc xmlto docbook2x
```

- 编译并安装
```
$ tar -zxf git-2.7.4.tar.gz
$ cd git-2.0.0
$ make configure
$ ./configure --prefix=/usr
$ make all doc info
$ sudo make install install-doc install-html install-info
```
> 若安装失败并提示 /bin/sh: line 1: docbook2texi: command not found 则还需要以下几步才能继续安装，只是我这里出现的问题，若一切顺利请无视。
```
$ sudo yum install docbook2X
$ cd /usr/bin
$ ln -s db2x_docbook2texi docbook2x-texi
```
成功安装后请重新编译并安装。

- 检查
```
$ git --version
```
成功安装的话会出现Git的版本号。

## Debian编译并安装Git
- [官网教程](https://git-scm.com/book/zh/v2/%E8%B5%B7%E6%AD%A5-%E5%AE%89%E8%A3%85-Git)