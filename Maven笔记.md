# Maven笔记
* [一、Maven命令](#anchor1)
* [二、基本配置](#anchor2)
* [三、配置依赖](#anchor3)
* [四、依赖范围](#anchor4)
* [五、配置本地仓库](#anchor5)
* [六、配置依赖的远程仓库](#anchor6)
* [七、配置插件的远程仓库](#anchor7)
* [八、配置仓库镜像](#anchor8)
* [九、配置远程仓库/仓库镜像的认证信息](#anchor9)
* [十、将项目生成的构件部署到远程仓库中](#anchor10)
* [十一、Maven生命周期和插件](#anchor11)
* [十二、配置Maven属性](#anchor12)
* [十三、配置Java编译器版本](#anchor13)
* [十四、配置处理资源文件时的编码](#anchor14)
* [十五、借助maven-shade-plugin插件生成可执行的jar包](#anchor15)
* [十六、借助maven-dependency-plugin插件将依赖jar包拷贝到指定目录](#anchor16)
* [十七、配置生成可执行jar包（包含运行时依赖jar包的Classpath配置）](#anchor17)
* [十八、借助maven-source-plugin插件生成源码的jar包](#anchor18)
* [十九、借助maven-javadoc-plugin插件生成javadoc文档的jar包](#anchor19)

## <a name="anchor1">一、Maven命令</a>
**mvn [options] [<goal(s)>] [<phase(s)>]**
```bash
echo %M2_HOME%                ##环境变量：Maven安装目录
mvn -v                        ##查看Maven安装版本
mvn -h                        ##查看mvn命令帮助信息

mvn help:system               ##执行maven-help-plugin插件的system目标，查看Java系统属性和环境变量
mvn help:effective-pom        ##执行maven-help-plugin插件的effective-pom目标，查看项目的有效POM
mvn help:effective-settings   ##执行maven-help-plugin插件的effective-settings目标，查看有效settings
mvn dependency:list           ##执行maven-dependency-plugin插件的list目标，查看项目的已解析依赖
mvn dependency:tree           ##执行maven-dependency-plugin插件的tree目标，查看项目的依赖树
mvn dependency:analyze        ##执行maven-dependency-plugin插件的analyze目标，分析项目的依赖
mvn compiler:compile          ##执行maven-compiler-plugin插件的compile目标，编译项目的主源码
mvn compiler:testCompile      ##执行maven-compiler-plugin插件的testCompile目标，编译项目的测试代码
mvn surefire:test             ##执行maven-surefire-plugin插件的test目标，使用单元测试框架运行测试

mvn clean                     ##执行到clean生命周期的clean阶段
mvn test                      ##执行到default生命周期的test阶段
mvn clean compile             ##执行到clean生命周期的clean阶段和default生命周期的compile阶段
mvn clean test                ##执行到clean生命周期的clean阶段和default生命周期的test阶段
mvn clean package             ##执行到clean生命周期的clean阶段和default生命周期的package阶段
mvn clean install             ##执行到clean生命周期的clean阶段和default生命周期的install阶段
mvn clean deploy              ##执行到clean生命周期的clean阶段和default生命周期的deploy阶段
mvn clean deploy site-deploy  ##执行到clean生命周期的clean阶段和default生命周期的deploy阶段，以及site生命周期的site-deploy阶段
mvn clean install -U          ##强制检查远程仓库中的构件更新

mvn archetype:generate        ##使用Archetype插件创建项目骨架

##查看maven-compiler-plugin插件2.1版本的简要信息
mvn help:describe -Dplugin=org.apache.maven.plugins:maven-compiler-plugin:2.1
##查看maven-compiler-plugin插件2.1版本的详细信息
mvn help:describe -Dplugin=org.apache.maven.plugins:maven-compiler-plugin:2.1 -Ddetail
##查看maven-compiler-plugin插件最新版本的简要信息
mvn help:describe -Dplugin=org.apache.maven.plugins:maven-compiler-plugin
mvn help:describe -Dplugin=compiler
mvn help:describe -Dplugin=compiler -Dgoal=compile
mvn help:describe -Dplugin=compiler -Dgoal=compile -Ddetail
```

## <a name="anchor2">二、基本配置</a>
**pom.xml**
```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.minyazi.mvntest</groupId>
    <artifactId>hello-world</artifactId>
    <packaging>jar</packaging>
    <version>1.0-SNAPSHOT</version>
    <name>First Maven Project</name>
</project>
```

## <a name="anchor3">三、配置依赖</a>
**pom.xml**
```xml
<project>
    ...
    <dependencies>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.7</version>
            <scope>test</scope>
        </dependency>
    </dependencies>
    ...
</project>
```

## <a name="anchor4">四、依赖范围</a>
**scope**
1. compile：**默认**，编译依赖范围。
2. test：测试范围依赖。
3. provided：已提供范围依赖。
4. runtime：运行时依赖范围。
5. system：系统依赖范围。
6. import：导入依赖范围。

## <a name="anchor5">五、配置本地仓库</a>
**settings.xml**
```xml
<settings>
    ...
    <localRepository>E:\maven\repository\</localRepository>
    ...
</settings>
```

## <a name="anchor6">六、配置依赖的远程仓库</a>
**pom.xml**
```xml
<project>
    ...
    <repositories>
        <repository>
            <id>jboss</id>
            <name>JBoss Repository</name>
            <url>http://repository.jboss.com/maven2/</url>
            <!-- 仓库布局 -->
            <layout>default</layout>
            <!-- 开启仓库的发布版构件下载支持 -->
            <releases>
                <enabled>true</enabled>
            </releases>
            <!-- 关闭仓库的快照版构件下载支持 -->
            <snapshots>
                <enabled>false</enabled>
            </snapshots>
        </repository>
    </repositories>
    ...
</project>
```

## <a name="anchor7">七、配置插件的远程仓库</a>
**pom.xml**
```xml
<project>
    ...
    <pluginRepositories>
        <pluginRepository>
            <id>central</id>
            <name>Central Repository</name>
            <url>https://repo.maven.apache.org/maven2</url>
            <layout>default</layout>
            <snapshots>
                <enabled>false</enabled>
            </snapshots>
            <releases>
                <updatePolicy>never</updatePolicy>
            </releases>
        </pluginRepository>
    </pluginRepositories>
    ...
</project>
```

## <a name="anchor8">八、配置仓库镜像</a>
**settings.xml**
```xml
<settings>
    ...
    <mirrors>
        <mirror>
            <id>mirrorId</id>
            <mirrorOf>repositoryId</mirrorOf>
            <name>mirrorName</name>
            <url>mirrorURL</url>
        </mirror>
    </mirrors>
    ...
</settings>
```

## <a name="anchor9">九、配置远程仓库/仓库镜像的认证信息</a>
**settings.xml**
```xml
<settings>
    ...
    <servers>
        <server>
            <id>repositoryId/mirrorId</id>
            <username>username</username>
            <password>password</password>
        </server>
    </servers>
    ...
</settings>
```

## <a name="anchor10">十、将项目生成的构件部署到远程仓库中</a>
**pom.xml**
```xml
<project>
    ...
    <distributionManagement>
        <!-- 发布版构件仓库 -->
        <repository>
            <uniqueVersion>false</uniqueVersion>
            <id>minyazi-maven-repository</id>
            <name>Minyazi Maven Repository</name>
            <url>file://E:/maven/repository</url>
            <!-- 仓库布局 -->
            <layout>default</layout>
        </repository>
        <!-- 快照版构件仓库，如果没有配置则部署到发布版构件仓库中
        <snapshotRepository>
            <uniqueVersion>true</uniqueVersion>
            <id>minyazi-maven-repository</id>
            <name>Minyazi Maven Repository</name>
            <url>file://E:/maven/repository</url>
            <layout>legacy</layout>
        </snapshotRepository>
        -->
    </distributionManagement>
    ...
</project>
```

## <a name="anchor11">十一、Maven生命周期和插件</a>
1. clean生命周期。该生命周期的目的是清理项目，其包含如下阶段：
```xml
<phases>
    <phase>pre-clean</phase>      <!-- 执行一些清理前需要完成的工作 -->
    <phase>clean</phase>          <!-- 清理上一次构建生成的文件 -->
    <phase>post-clean</phase>     <!-- 执行一些清理后需要完成的工作 -->
</phases>
```
2. default生命周期。该生命周期定义了真正构建时所需要执行的所有步骤，它是所有生命周期中最核心的部分，其包含的阶段如下：
```xml
<phases>
    <phase>validate</phase>                    <!--  -->
    <phase>initialize</phase>                  <!--  -->
    <phase>generate-sources</phase>            <!--  -->
    <phase>process-sources</phase>             <!-- 处理项目主资源文件 -->
    <phase>generate-resources</phase>          <!--  -->
    <phase>process-resources</phase>           <!--  -->
    <phase>compile</phase>                     <!-- 编译项目的主源码 -->
    <phase>process-classes</phase>             <!--  -->
    <phase>generate-test-sources</phase>       <!--  -->
    <phase>process-test-sources</phase>        <!-- 处理项目测试资源文件 -->
    <phase>generate-test-resources</phase>     <!--  -->
    <phase>process-test-resources</phase>      <!--  -->
    <phase>test-compile</phase>                <!-- 编译项目的测试代码 -->
    <phase>process-test-classes</phase>        <!--  -->
    <phase>test</phase>                        <!-- 使用单元测试框架运行测试，测试代码不会被打包或部署 -->
    <phase>prepare-package</phase>             <!--  -->
    <phase>package</phase>                     <!-- 接受编译好的代码，打包成可发布的格式，如JAR -->
    <phase>pre-integration-test</phase>        <!--  -->
    <phase>integration-test</phase>            <!--  -->
    <phase>post-integration-test</phase>       <!--  -->
    <phase>verify</phase>                      <!--  -->
    <phase>install</phase>                     <!-- 将包安装到Maven本地仓库，供本地其他Maven项目使用 -->
    <phase>deploy</phase>                      <!-- 将最终的包复制到远程仓库，供其他开发人员和Maven项目使用 -->
</phases>
```
3. site生命周期。该生命周期的目的是建立和发布项目站点，其包含如下阶段：
```xml
<phases>
    <phase>pre-site</phase>        <!-- 执行一些在生成项目站点之前需要完成的工作 -->
    <phase>site</phase>            <!-- 生成项目站点文档 -->
    <phase>post-site</phase>       <!-- 执行一些在生成项目站点之后需要完成的工作 -->
    <phase>site-deploy</phase>     <!-- 将生成的项目站点发布到服务器上 -->
</phases>
```
4. clean生命周期阶段与插件目标的绑定关系
```xml
<default-phases>
    <clean>
        org.apache.maven.plugins:maven-clean-plugin:2.5:clean
    </clean>
</default-phases>
```
| 生命周期阶段 | 插件目标 |
| ---------- | ----------- |
| pre-clean  |             |
| clean      | clean:clean |
| post-clean |             |
5. default生命周期阶段与插件目标的绑定关系（打包类型：jar / ejb / war / rar）
```xml
<phases>
    <process-resources>
        org.apache.maven.plugins:maven-resources-plugin:2.6:resources
    </process-resources>
    <compile>
        org.apache.maven.plugins:maven-compiler-plugin:3.1:compile
    </compile>
    <process-test-resources>
        org.apache.maven.plugins:maven-resources-plugin:2.6:testResources
    </process-test-resources>
    <test-compile>
        org.apache.maven.plugins:maven-compiler-plugin:3.1:testCompile
    </test-compile>
    <test>
        org.apache.maven.plugins:maven-surefire-plugin:2.12.4:test
    </test>
    <package>
        org.apache.maven.plugins:maven-jar-plugin:2.4:jar
        <!-- org.apache.maven.plugins:maven-ejb-plugin:2.3:ejb -->
        <!-- org.apache.maven.plugins:maven-war-plugin:2.2:war -->
        <!-- org.apache.maven.plugins:maven-rar-plugin:2.2:rar -->
    </package>
    <install>
        org.apache.maven.plugins:maven-install-plugin:2.4:install
    </install>
    <deploy>
        org.apache.maven.plugins:maven-deploy-plugin:2.7:deploy
    </deploy>
</phases>
```
| 生命周期阶段 | 插件目标 | 执行任务 |
| ---------------------- | ---------------------------------------- | ------------------------------ |
| process-resources      | resources:resources                      | 复制主资源文件至主输出目录        |
| compile                | compiler:compile                         | 编译主代码至主输出目录           |
| process-test-resources | resources:testResources                  | 复制测试资源文件至测试输出目录    |
| test-compile           | compiler:testCompile                     | 编译测试代码至测试输出目录        |
| test                   | surefire:test                            | 执行测试用例                    |
| package                | jar:jar or ejb:ejb or war:war or rar:rar | 创建项目jar / ejb / war / rar包 |
| install                | install:install                          | 将项目输出构件安装到本地仓库      |
| deploy                 | deploy:deploy                            | 将项目输出构件部署到远程仓库      |
6. default生命周期阶段与插件目标的绑定关系（打包类型：ear）
```xml
<phases>
    <generate-resources>
        org.apache.maven.plugins:maven-ear-plugin:2.8:generate-application-xml
    </generate-resources>
    <process-resources>
        org.apache.maven.plugins:maven-resources-plugin:2.6:resources
    </process-resources>
    <package>
        org.apache.maven.plugins:maven-ear-plugin:2.8:ear
    </package>
    <install>
        org.apache.maven.plugins:maven-install-plugin:2.4:install
    </install>
    <deploy>
        org.apache.maven.plugins:maven-deploy-plugin:2.7:deploy
    </deploy>
</phases>
```
| 生命周期阶段 | 插件目标 |
| ------------------ | ---------------------------- |
| generate-resources | ear:generate-application-xml |
| process-resources  | resources:resources          |
| package            | ear:ear                      |
| install            | install:install              |
| deploy             | deploy:deploy                |
7. default生命周期阶段与插件目标的绑定关系（打包类型：maven-plugin）
```xml
<phases>
    <process-resources>
        org.apache.maven.plugins:maven-resources-plugin:2.6:resources
    </process-resources>
    <compile>
        org.apache.maven.plugins:maven-compiler-plugin:3.1:compile
    </compile>
    <process-classes>
        org.apache.maven.plugins:maven-plugin-plugin:3.2:descriptor
    </process-classes>
    <process-test-resources>
        org.apache.maven.plugins:maven-resources-plugin:2.6:testResources
    </process-test-resources>
    <test-compile>
        org.apache.maven.plugins:maven-compiler-plugin:3.1:testCompile
    </test-compile>
    <test>
        org.apache.maven.plugins:maven-surefire-plugin:2.12.4:test
    </test>
    <package>
        org.apache.maven.plugins:maven-jar-plugin:2.4:jar,
        org.apache.maven.plugins:maven-plugin-plugin:3.2:addPluginArtifactMetadata
    </package>
    <install>
        org.apache.maven.plugins:maven-install-plugin:2.4:install
    </install>
    <deploy>
        org.apache.maven.plugins:maven-deploy-plugin:2.7:deploy
    </deploy>
</phases>
```
| 生命周期阶段 | 插件目标 |
| ---------------------- | -------------------------------------------- |
| generate-resources     | plugin:descriptor                            |
| process-resources      | resources:resources                          |
| compile                | compiler:compile                             |
| process-test-resources | resources:testResources                      |
| test-compile           | compiler:testCompile                         |
| test                   | surefire:test                                |
| package                | jar:jar and plugin:addPluginArtifactMetadata |
| install                | install:install                              |
| deploy                 | deploy:deploy                                |
8. default生命周期阶段与插件目标的绑定关系（打包类型：pom）
```xml
<phases>
    <install>
        org.apache.maven.plugins:maven-install-plugin:2.4:install
    </install>
    <deploy>
        org.apache.maven.plugins:maven-deploy-plugin:2.7:deploy
    </deploy>
</phases>
```
| 生命周期阶段 | 插件目标 |
| ------- | ---------------------- |
| package | site:attach-descriptor |
| install | install:install        |
| deploy  | deploy:deploy          |
9. site生命周期阶段与插件目标的绑定关系
```xml
<default-phases>
    <site>
        org.apache.maven.plugins:maven-site-plugin:3.3:site
    </site>
    <site-deploy>
        org.apache.maven.plugins:maven-site-plugin:3.3:deploy
    </site-deploy>
</default-phases>
```
| 生命周期阶段 | 插件目标 |
| ----------- | ----------- |
| pre-site    |             |
| site        | site:site   |
| post-site   |             |
| site-deploy | site:deploy |

## <a name="anchor12">十二、配置Maven属性</a>
**pom.xml**
```xml
<project>
    ...
    <properties>
        <java.version>1.8</java.version>
        <project.encoding>UTF-8</project.encoding>
        <!-- 文件拷贝时的编码 -->
        <project.build.sourceEncoding>${project.encoding}</project.build.sourceEncoding>
        <project.reporting.outputEncoding>${project.encoding}</project.reporting.outputEncoding>
        <!-- 编译时的编码 -->
        <maven.compiler.encoding>${project.encoding}</maven.compiler.encoding>
	</properties>
    ...
</project>
```

## <a name="anchor13">十三、配置Java编译器版本</a>
**pom.xml**
```xml
<project>
    ...
    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.1</version>
                <configuration>
                    <source>${java.version}</source>
                    <target>${java.version}</target>
                    <encoding>${project.encoding}</encoding>
                </configuration>
            </plugin>
        </plugins>
    </build>
    ...
</project>
```
或者
```xml
<project>
    ...
    <properties>
        <maven.compiler.source>${java.version}</maven.compiler.source>
        <maven.compiler.target>${java.version}</maven.compiler.target>
    </properties>
    ...
</project>
```

## <a name="anchor14">十四、配置处理资源文件时的编码</a>
**pom.xml**
```xml
<project>
    ...
    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-resources-plugin</artifactId>
                <version>2.6</version>
                <configuration>
                    <encoding>${project.encoding}</encoding>
                </configuration>
            </plugin>
        </plugins>
    </build>
    ...
</project>
```

## <a name="anchor15">十五、借助maven-shade-plugin插件生成可执行的jar包</a>
**PS**：该方式会同时打包运行时依赖jar包中的内容。
```xml
<project>
    ...
    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-shade-plugin</artifactId>
                <version>3.0.0</version>
                <executions>
                    <execution>
                        <phase>package</phase>
                        <goals>
                            <goal>shade</goal>
                        </goals>
                        <configuration>
                            <transformers>
                                <transformer implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
                                    <mainClass>com.minyazi.mvntest.helloworld.HelloWorld</mainClass>
                                </transformer>
                            </transformers>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
    ...
</project>
```

## <a name="anchor16">十六、借助maven-dependency-plugin插件将依赖jar包拷贝到指定目录</a>
```xml
<project>
    ...
    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-dependency-plugin</artifactId>
                <version>3.0.1</version>
                <executions>
                    <execution>
                        <phase>package</phase>
                        <goals>
                            <goal>copy-dependencies</goal>
                        </goals>
                        <configuration>
                            <outputDirectory>${project.build.directory}/lib</outputDirectory>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
    ...
</project>
```

## <a name="anchor17">十七、配置生成可执行jar包（包含运行时依赖jar包的Classpath配置）</a>
```xml
<project>
    ...
    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-jar-plugin</artifactId>
                <version>2.4</version>
                <configuration>
                    <archive>
                        <index>true</index>
                        <manifest>
                            <addClasspath>true</addClasspath>
                            <classpathPrefix>lib/</classpathPrefix>
                            <mainClass>com.minyazi.mvntest.helloworld.HelloWorld</mainClass>
                        </manifest>
                    </archive>
                </configuration>
            </plugin>
        </plugins>
    </build>
    ...
</project>
```

## <a name="anchor18">十八、借助maven-source-plugin插件生成源码的jar包</a>
```xml
<project>
    ...
    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-source-plugin</artifactId>
                <version>3.0.1</version>
                <executions>
                    <execution>
                        <phase>package</phase>
                        <goals>
                            <goal>jar-no-fork</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
    ...
</project>
```

## <a name="anchor19">十九、借助maven-javadoc-plugin插件生成javadoc文档的jar包</a>
```xml
<project>
    ...
    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-javadoc-plugin</artifactId>
                <version>2.10.4</version>
                <executions>
                    <execution>
                        <phase>package</phase>
                        <goals>
                            <goal>jar</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
    ...
</project>
```
