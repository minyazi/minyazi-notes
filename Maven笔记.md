# Maven笔记
* [Maven命令](#anchor1)
* [基本配置](#基本配置)
* [配置依赖](#配置依赖)
* [依赖范围](#依赖范围)
* [配置Maven属性](#anchor2)
* [配置Java编译器版本](#anchor3)
* [借助maven-shade-plugin插件生成可执行的jar包](#anchor4)
* [配置本地仓库](#配置本地仓库)
* [配置远程仓库](#配置远程仓库)
* [配置仓库镜像](#配置仓库镜像)
* [配置远程仓库/仓库镜像的认证信息](#anchor5)
* [将项目生成的构件部署到远程仓库中](#将项目生成的构件部署到远程仓库中)

## <a name="anchor1">Maven命令</a>
```bash
echo %M2_HOME%                ##环境变量：Maven安装目录
mvn -v                        ##查看Maven安装版本
mvn help:system               ##查看Java系统属性和环境变量
mvn clean compile             ##清理输出目录并编译项目主代码
mvn clean test                ##清理输出目录并执行测试
mvn clean package             ##清理输出目录并打包
mvn clean install             ##清理输出目录并安装
mvn clean deploy              ##清理输出目录并将项目生成的构件部署到远程仓库中
mvn -U ...                    ##强制检查远程仓库中的构件更新
mvn archetype:generate        ##使用Archetype插件创建项目骨架
mvn dependency:list           ##查看项目的已解析依赖
mvn dependency:tree           ##查看项目的依赖树
mvn dependency:analyze        ##分析项目的依赖
```

## 基本配置
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

## 配置依赖
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

## 依赖范围
**scope**
1. compile：**默认**，编译依赖范围。
2. test：测试范围依赖。
3. provided：已提供范围依赖。
4. runtime：运行时依赖范围。
5. system：系统依赖范围。
6. import：导入依赖范围。

## <a name="anchor2">配置Maven属性</a>
**pom.xml**
```xml
<project>
    ...
    <properties>
        <java.version>1.8</java.version>
    </properties>
    ...
</project>
```

## <a name="anchor3">配置Java编译器版本</a>
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
                </configuration>
            </plugin>
        </plugins>
    </build>
    ...
</project>
```

## <a name="anchor4">借助maven-shade-plugin插件生成可执行的jar包</a>
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

## 配置本地仓库
**settings.xml**
```xml
<settings>
    ...
    <localRepository>E:\maven\repository\</localRepository>
    ...
</settings>
```

## 配置远程仓库
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

## 配置仓库镜像
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

## <a name="anchor5">配置远程仓库/仓库镜像的认证信息</a>
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

## 将项目生成的构件部署到远程仓库中
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
