# Jenkins 常用插件介绍


本文主要介绍了 Jenkins 的一些常用插件。

## 1. 常用插件介绍
### 1.1 CAS Plugin
用于 CAS 接入。

![CAS 插件介绍](01.png "CAS 插件介绍")

![CAS 插件配置](02.png "CAS 插件配置")

### 1.2 Matrix Authorization Strategy Plugin
![Matrix Authorization 插件介绍](03.png "Matrix Authorization 插件介绍")

![Matrix Authorization 插件配置](04.png "Matrix Authorization 插件配置")

### 1.3 Pipeline Plugin
用来创建 Pipeline Job。如果不配置，创建 Job 时将不会有下面的选项。

![创建 Pipeline Job](05.png "创建 Pipeline Job")

### 1.4 Timestamper Plugin
Adds timestamps to the Console Output，没有装该插件的报错如下：

![Timestamper 插件报错](06.png "Timestamper 插件报错")

### 1.5 Pipeline Utility Steps Plugin
Utility steps for pipeline jobs，没有装该插件的报错如下：

![Pipeline Utility Steps 插件报错](07.png "Pipeline Utility Steps 插件报错")

### 1.6 Git Plugin
This plugin integrates Git with Jenkins，如果不配置，Pipeline script from SCM 时无法选择到 git：
![Git 插件配置](08.png "Git 插件配置")

## 1.7 Kubernetes Plugin
This plugin integrates Jenkins with kubernetes。

![Kubernetes 插件介绍](09.png "Kubernetes 插件介绍")

![Kubernetes 插件配置步骤 1](10.png "Kubernetes 插件配置步骤 1")

![Kubernetes 插件配置步骤 2](11.png "Kubernetes 插件配置步骤 2")

![Kubernetes 插件配置步骤 3](12.png "Kubernetes 插件配置步骤 3")

![Kubernetes 插件配置步骤 4](13.png "Kubernetes 插件配置步骤 4")

![Kubernetes 插件配置步骤 5](14.png "Kubernetes 插件配置步骤 5")

## 2. 携程 build 使用的插件
主要包括：CAS、Matrix Authorization Strategy、Pipeline、Timestamper、Pipeline Utility Steps、Git、Kubernetes 等。

