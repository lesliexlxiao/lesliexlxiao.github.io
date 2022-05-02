# Dockerfile 最佳实践（指令相关）


本文主要介绍了编写 Dockerfile 指令相关的一些最佳实践。

## 1. FROM
尽可能使用<font color=FF0099>**当前官方仓库**</font>作为你构建镜像的基础。如果公司内部使用，可下载官方仓库镜像，再推送至私有 registry。

推荐使用 <font color=FF0099>**Alpine 镜像（Alpine Linux 是一个完整的操作系统）**</font>，因为其被严格控制并保持在最小尺寸（目前大小 5.52M）。基于此基础镜像，再去构建自己的基础镜像，可以有效控制镜像的大小。


## 2. LABEL
通过给镜像添加标签可以帮助<font color=FF0099>**组织镜像、记录许可信息、辅助自动化构建**</font>等。示例如下：

```
LABEL com.example.version="0.0.1-beta"

LABEL vendor="ACME Incorporated"

LABEL com.example.release-date="2015-02-12"

LABEL com.example.version.is-production=""
```

注意：如果你的字符串中包含空格，<font color=FF0099>**必须将字符串放入引号中或者对空格使用转义**</font>。如果字符串内容本身就包含引号，<font color=FF0099>**必须对引号使用转义。**</font>

一个镜像可以包含多个标签，但建议将多个标签放入到一个 LABEL 指令中。

```
LABEL vendor=ACME\ Incorporated \
  com.example.is-beta= \
  com.example.is-production="" \
  com.example.version="0.0.1-beta" \
  com.example.release-date="2015-02-12"
```

标签可接受的键值参考：<a href="https://docs.docker.com/config/labels-custom-metadata/"  target="_blank">Understanding object labels</a>

查询标签信息参考：<a href="https://docs.docker.com/config/labels-custom-metadata/"  target="_blank">Managing labels on objects</a>

在实际运维过程中，容器的数量级一旦上升，就会给运维上带来很大的挑战。<font color=FF0099>**通过 label 可以很好的将容器分类，从而便于运维**</font>。
  ```shell
  # 创建容器的时候定义一个 label，表示该容器在 test 这个区域
  $ docker run -itd --name nginx-test --label zone=test

  # 使用自定义的 label 快速检索容器，并进行下一步操作
  $ docker ps -f label=zone=test --format='{{.NAMES}}'
  ```

## 3. RUN
为了保持 Dockerfile 文件的<font color=FF0099>**可读性，可理解性，以及可维护性**</font>，过长的或复杂的 RUN 指令使用反斜杠 \ 分行。
```
RUN yum install -y pip \
  git-1.9.3.1 \
  wget-1.14 && \
  yum clean all
```

Ubuntu，通常会使用 apt-get 去安装包。

不要使用 RUN apt-get upgrade 或 dist-upgrade，<font color=FF0099>**因为 upgrade 命令会导致升级所有包**</font>，其实常常用户并不想升级基础镜像里面的包。如果要单独升级某一个包，使用 apt-get install -y foo。

将 RUN apt-get update 和 apt-get install 组合成一条 RUN 声明：
```
RUN apt-get update && apt-get install -y \
  package-bar \
  package-baz
```

<font color=FF0099>**如果将 RUN apt-get update 和 apt-get install 拆解为两条命令，会导致缓存问题记忆后续的 install 失败**</font>，示例如下：
```
FROM ubuntu:14.04

RUN apt-get update

RUN apt-get install -y curl
```

构建镜像后，所有的镜像层都在 Docker 缓存中。这时修改 Dockerfile 如下：
```
FROM ubuntu:14.04

RUN apt-get update

RUN apt-get install -y curl nginx
```

再次构建镜像，Docker 发现  RUN apt-get update 指令一样。这样会导致 apt-get update 不再执行，使用缓存镜像。<font color=FF0099>**后面使用 apt-get install 安装的是过时的 curl 和 nginx 版本。**</font>

## 4. CMD
多数情况下都应该以 CMD ["executable", "param1", "param2"...] 的形式使用。

极少情况下才能以 CMD ["param", "param"] 的形式与 ENTRYPOINT 协同使用。


## 5. EXPOSE
为应用程序 EXPOSE 常用端口，如 Apache web 服务的镜像使用 EXPOSE 80，MongoDB 服务的镜像使用 EXPOSE 27017。


## 6. ENV
主要有以下作用：

  - 为容器中安装的程序更新 PATH 环境变量，确保如 CMD ["nginx"] 正确运行。
    ```
    ENV PATH /usr/local/nginx/bin:$PATH
    ```

  - 为容器化服务提供必要的环境变量。


## 7. ADD 和 COPY
<font color=FF0099>**优先使用 COPY，COPY 语义更明确。**</font>

ADD 能够将本地 tar 文件自动提取到镜像中，这种场景用 ADD 更合适。

如果 Dockerfile 中需要 COPY 多个上下文中的文件，不要一次性 COPY 所有文件，这将保证每个步骤的构建缓存只在特定的文件变化时失效。最好的做法是按文件组织结构以及功能去 COPY 文件。

为了让镜像尽量小，最好不要使用 ADD 指令从远程 URL 获取包，而是使用 curl 和 wget 。这样可以避免使用 ADD 而会多出的额外镜像层，示例如下：
```
# invalid method
ADD http://example.com/big.tar.xz /usr/src/things/

RUN tar -xJf /usr/src/things/big.tar.xz -C /usr/src/things && \
  make -C /usr/src/things all
```

```
# valid method
RUN mkdir -p /usr/src/things \
&& curl -SL http://example.com/big.tar.xz \
| tar -xJC /usr/src/things \
&& make -C /usr/src/things all
```

可以看出第一种方法会比第二种方法多出额外的镜像层。


## 8. ENTRYPOINT
最佳用处是设置镜像的主命令，<font color=FF0099>**允许将镜像当成命令本身来运行。**</font>示例如下：
```
ENTRYPOINT ["s3cmd"]

CMD ["--help"]
```

运行容器：

```shell
$ docker run s3cmd

$ docker run s3cmd ls s3://mybucket
```

将 ENTRYPOINT 指令结合一个辅助脚本使用，去解决容器启动中多步骤问题。

  - 例如，Postgres 官方镜像使用下面的脚本作为 ENTRYPOINT:
    ```
    #!/bin/bash
    set -e

    if [ "$1" = 'postgres' ]; then
        chown -R postgres "$PGDATA"

        if [ -z "$(ls -A "$PGDATA")" ]; then
            gosu postgres initdb
        fi

        exec gosu postgres "$@"
    fi

    exec "$@"
    ```
    - <font color=FF0099>**注意：**</font> 该脚本使用了 Bash 的内置命令 exec，所以最后运行的进程就是容器的 PID 为 1 的进程。这样，进程就可以接收到任何发送给容器的 Unix 信号了。

  - 该辅助脚本被拷贝到容器，并在容器启动时通过 ENTRYPOINT 执行:
    ```
    COPY ./docker-entrypoint.sh /

    ENTRYPOINT ["/docker-entrypoint.sh"]
    ```

  - 这样可以使用多种方式和 postgres 交互：
    ```shell
    # 简单启动 Postgres
    $ docker run postgres

    # 执行 Postgres 并传递参数
    $ docker run postgres postgres --help
    ```

## 9. VOLUME
建议使用 VOLUME 来管理镜像中的可变部分和用户可以改变的部分，如数据库存储文件、配置文件、容器创建的文件和目录等。

## 10. USER
不需要使用特权执行的服务，建议使用 USER 指令切换到非 root 用户。使用下面的方法创建用户和用户组：
```
RUN groupadd -r postgres && \
  useradd -r -g postgres postgres
```

避免使用 sudo，因为它可预期的 TTY 和信号转发行为可能造成很多问题。可以使用 <a href="url">gosu</a> 来替代 sudo。

为了减少层数和复杂度，避免频繁地使用 USER 来回切换用户。

## 11. WORKDIR
为了清晰性和可靠性，应该总是在 WORKDIR 中使用绝对路径

使用 WORKDIR 来替代类似于 RUN cd ... && do-something 的指令，后者难以阅读、排错和维护。

## 12. 参考文献
[1] yeasy.Docker 从入门到实践[M]:369-375.

[2] 廖煜,晏东.Docker 容器实战[M].北京:电子工业出版社,2016:183-199.
