# virtualenv and virtualenvwrapper 工具的使用


本文主要介绍了 Python 开发中如何搭建虚拟的隔离环境，从而确保各应用之间的依赖互不影响。

<!-- more-->

## 1. 工具简介
virtualenv <font color=FF0099>**用来为一个应用创建一套"隔离"的 python 运行环境。**</font>

virtualenvwrapper 基于 virtualenv 之上的工具，<font color=FF0099>**用来对虚拟环境进行统一管理。**</font>

## 2. 工具安装
```shell
$ pip install virtualenv virtualenvwrapper
```

## 3. virtualenv 用法
创建环境（<font color=FF0099>**默认创建的环境会使用系统已经安装的包**</font>）

```shell
$ virtualenv venv
```

创建环境（<font color=FF0099>**不使用系统的包**</font>）

```shell
$ virtualenv --no-site-packages venv
```

激活环境

```shell
$ source venv/bin/activate
```

退出环境

```shell
$ deactive
```

## 4. virtualenvwrapper 用法
创建目录用来存放虚拟环境

```shell
$ mkdir ~/.virtualenvs
```

在 .bashrc 中添加

```shell
$ export WORKON_HOME=~/.virtualenvs
$ source /usr/local/bin/virtualenvwrapper.sh
```

激活 .bashrc

```shell
$ source ~/.bashrc
```

新建虚拟环境

```shell
$ mkvirtualenv test
```

列出虚拟环境列表

```shell
$ workon
$ lsvirtualenv
```

切换虚拟环境

```shell
$ workon test
```

删除虚拟环境

```shell
$ rmvirtualenv test
```

离开虚拟环境

```shell
$ deactivate
```
