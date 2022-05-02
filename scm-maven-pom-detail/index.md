# Maven pom.xml 文件详解


本文主要介绍了 maven pom.xml 中各元素的详细意义。

## 1. pom.xml 文件详解

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
http://maven.apache.org/xsd/maven-4.0.0.xsd">

    <!--
    声明项目描述符遵循哪一个 POM 模型版本。
    模型本身的版本很少改变，虽然如此，但它仍然是必不可少的，
    这是为了当 Maven 引入了新的特性或者其他模型变更的时候，确保稳定性。
    maven2.0 必须使用如下写法，现在是 maven2.0 唯一支持的版本。
    -->
    <modelVersion>4.0.0</modelVersion>

    <!--
    父项目的坐标。如果项目中没有规定某个元素的值，那么父项目中的对应值即为项目的默认值。
    -->
    <parent>
        <groupId>com.bidu</groupId>
        <artifactId>super-pom</artifactId>
        <version>0.0.1</version>

        <!--
        父项目的 pom.xml 文件的相对路径。相对路径允许你选择一个不同的路径。默认值是../pom.xml。
        Maven 首先在构建当前项目的地方寻找父项目的 pom，然后在本地仓库，最后在远程仓库寻找父项目的 pom。
        RelativePath 允许你选择一个不同的位置。
        -->
        <relativePath>xxx</relativePath>
    </parent>

    <!--
    定义了项目属于哪个组，公司或者组织的唯一标识，
    并且构建时生成的路径也是由此生成，
    如 com.mycompany.app 生成的相对路径为：/com/mycompany/app
    -->
    <groupId>com.bidu</groupId>

    <!--
    定义了当前 maven 项目在组中的唯一的 ID。
    它和 group ID 一起唯一标识一个构件。
    -->
    <artifactId>super-pom</artifactId>

    <!-- 本项目目前所处的版本号 -->
    <version>0.0.1</version>

    <!--
    项目产生的构件类型，例如 jar、war、ear、pom。
    插件可以创建他们自己的构件类型，所以前面列的不是全部构件类型。默认为 jar。
    -->
    <packaging>pom</packaging>

    <!-- 项目的名称，Maven 产生的文档用 -->
    <name>Bidu company super pom</name>

    <!-- 项目主页的 URL，Maven 产生的文档用 -->
    <url> http://maven.apache.org </url>

    <!--
    项目的详细描述, Maven 产生的文档用。
    当这个元素能够用 HTML 格式描述时（例如，CDATA 中的文本会被解析器忽略，就可以包含HTML标签），
    不鼓励使用纯文本描述。
    如果你需要修改产生的 web 站点的索引页面，你应该修改你自己的索引页文件，而不是调整这里的文档。
    -->
    <description>Bidu 公司 super pom</description>

    <!-- 描述项目所属组织的各种属性。Maven 产生的文档用 -->
    <organization>
        <!-- 组织的全名 -->
        <name>Bidi</name>

        <!-- 组织主页的URL -->
        <url>http://www.bidu.com</url>
    </organization>

    <!--
    为 pom 定义一些常量，在 pom 中的其它地方可以直接引用，
    使用方式如下：${java.version} ，${maven-surefire-plugin.version}
    -->
    <properties>
        <java.version>1.7</java.version>
        <maven-surefire-plugin.version>2.19.1</maven-surefire-plugin.version>
        <spring.version>4.3.4.RELEASE</spring.version>
    </properties>

    <!-- 构建项目需要的信息 -->
    <build>
        <!--
        子项目可以引用的默认插件信息。
        该插件配置项直到被引用时才会被解析或绑定到生命周期。
        给定插件的任何本地配置都会覆盖这里的配置。
        -->
        <pluginManagement>
            <plugins>
                <plugin>
                    <!-- 插件在仓库里的 group ID -->
                    <groupId>org.apache.maven.plugins</groupId>

                    <!-- 插件在仓库里的 artifact ID -->
                    <artifactId>maven-enforcer-plugin</artifactId>

                    <!-- 被使用的插件的版本（或版本范围） -->
                    <version>${maven-enforcer-plugin_version}</version>

                    <!--
                    是否从该插件下载 Maven 扩展（例如打包和类型处理器），
                    由于性能原因，只有在真需要下载时，该元素才被设置成 enabled。
                    -->
                    <extensions>true/false</extensions>

                    <!-- 在构建生命周期中执行一组目标的配置。每个目标可能有不同的配置。 -->
                    <executions>
                        <execution>
                            <!-- 执行目标的标识符，用于标识构建过程中的目标，或者匹配继承过程中需要合并的执行目标 -->
                            <id></id>

                            <!-- 绑定了目标的构建生命周期阶段，如果省略，目标会被绑定到源数据里配置的默认阶段 -->
                            <phase></phase>

                            <!-- 配置的执行目标 -->
                            <goals></goals>

                            <!-- 配置是否被传播到子POM -->
                            <inherited>true/false</inherited>

                            <!-- 作为 DOM 对象的配置 -->
                            <configuration></configuration>
                        </execution>
                    </executions>

                    <!-- 项目引入插件所需要的额外依赖 -->
                    <dependencies>
                        <!-- 参见dependencies/dependency元素 -->
                        <dependency>
                            <groupId>bidu.scm</groupId>
                            <artifactId>enforcer-custom-rules</artifactId>
                            <version>${enforcer-custom-rules_version}</version>
                        </dependency>
                        <dependency>
                            <groupId>org.codehaus.mojo</groupId>
                            <artifactId>extra-enforcer-rules</artifactId>
                            <version>${extra-enforcer-rules_version}</version>
                        </dependency>
                    </dependencies>

                    <!-- 任何配置是否被传播到子项目 -->
                    <inherited>true/false</inherited>

                    <!-- 作为 DOM 对象的配置 -->
                    <configuration></configuration>
                </plugin>
            </plugins>
        </pluginManagement>

        <!-- 该项目使用的插件列表 -->
        <plugins>
            <plugin>
                <!-- 插件在仓库里的 group ID -->
                <groupId>org.apache.maven.plugins</groupId>

                <!-- 插件在仓库里的 artifact ID -->
                <artifactId>maven-enforcer-plugin</artifactId>

                <!-- 被使用的插件的版本（或版本范围）-->
                <version></version>

                <!--
                是否从该插件下载 Maven 扩展（例如打包和类型处理器），
                由于性能原因，只有在真需要下载时，该元素才被设置成 enabled。
                -->
                <extensions>true/false</extensions>


                <!-- 在构建生命周期中执行一组目标的配置。每个目标可能有不同的配置。 -->
                <executions>

                    <!-- execution 元素包含了插件执行需要的信息 -->
                    <execution>

                        <!-- 执行目标的标识符，用于标识构建过程中的目标，或者匹配继承过程中需要合并的执行目标 -->
                        <id>bidu-check</id>

                        <!-- 绑定了目标的构建生命周期阶段，如果省略，目标会被绑定到源数据里配置的默认阶段 -->
                        <phase>validate</phase>

                        <!-- 配置的执行目标 -->
                        <goals>
                            <goal>enforce</goal>
                        </goals>

                        <!-- 配置是否被传播到子 POM -->
                        <inherited>true/false</inherited>

                        <!-- 作为 DOM 对象的配置 -->
                        <configuration></configuration>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>

    <!--
    dependencyManagement 声明的依赖，既不会给父 pom 引入依赖，也不会给子模块 引入依赖。

    子模块会继承这段配置，子模块只需要配置简单的 groupID 和 artifactID 就能获得对应的依赖信息，
    从而引入正确的依赖。

    虽然使用这种依赖管理机制不能减少太多的 pom 配置。
    但是在父 pom 中使用 dependencyManagement 声明依赖能够统一项目范围中的版本，
    当依赖版本在父 pom 声明之后，子模块在使用依赖的时候就无须声明版本，
    也就不会发生多个子模块使用依赖版本不一致的情况，降低依赖冲突的几率。
    -->
    <dependencyManagement>
        <dependencies>
            <dependency>
                <groupId>org.springframework</groupId>
                <artifactId>spring-core</artifactId>
                <version>${spring.version}</version>

                <!--
                当计算传递依赖时，从依赖构件列表里，列出被排除的依赖构件集。
                即告诉 maven 你只依赖指定的项目，不依赖项目的依赖。
                此元素主要用于解决版本冲突问题。
                -->
                <exclusions>
                    <exclusion>
                        <groupId>commons-logging</groupId>
                        <artifactId>commons-logging</artifactId>
                    </exclusion>
                </exclusions>
            </dependency>
        </dependencies>
    </dependencyManagement>

    <!--
    项目分发信息，在执行 mvn deploy 后表示要发布的位置。
    有了这些信息就可以把网站部署到远程服务器或者把构件部署到远程仓库。
    -->
    <distributionManagement>
        <!-- 部署项目产生的构件到远程仓库需要的信息 -->
        <repository>
            <id>releases</id>
            <url>${releases.repo}</url>
        </repository>
        <!-- 构件的快照部署到哪里？如果没有配置该元素，默认部署到 repository 元素配置的仓库 -->
        <snapshotRepository>
            <id>snapshots</id>
            <url>${snapshots.repo}</url>
        </snapshotRepository>
    </distributionManagement>
</project>
```

## 2. 插件参考文档
文档地址：[https://maven.apache.org/plugins/](https://maven.apache.org/plugins/).

## 3. 参考文献
[1] [史上最全的 maven 的 pom.xml 文件详解](https://www.cnblogs.com/hafiz/p/5360195.html).

[2] [Maven 之 pom.xml 配置文件详解](https://blog.csdn.net/qq_33363618/article/details/79438044).
