# 记录使用Eclipse构建Spring Framework源码的过程

* [一、环境准备](#anchor1)
* [二、构建过程](#anchor2)
* [三、遇到的问题](#anchor3)

## <a name="anchor1">一、环境准备</a>

1. 工具

| 名称 | 版本 | 下载地址 |
| ---------------- | ------------------ | ----------------------------------------------------------------------------------------- |
| Spring Framework | v4.2.4.RELEASE     | https://github.com/spring-projects/spring-framework/releases                              |
| JDK              | Java SE 8          | http://www.oracle.com/technetwork/java/javase/downloads/java-archive-javase8-2177648.html |
| Eclipse          | Eclipse Neon (4.6) | https://www.eclipse.org/downloads/packages/release/Neon/3                                 |
| Git              | 2.9.3 for Windows  | https://git-scm.com/downloads                                                             |
| Gradle           | 2.6                | http://services.gradle.org/distributions/                                                 |

2. Eclipse插件

| 名称 | 版本 | 安装地址 |
| ----------------- | -------- | ---------------------------------------------------------------- |
| Eclipse Buildship | 2.x      | `http://download.eclipse.org/buildship/updates/e46/releases/2.x` |
| Groovy-Eclipse    | 2.9.2.xx | `http://dist.springsource.org/release/GRECLIPSE/e4.6`            |
| AJDT              | 2.2.4    | `http://download.eclipse.org/tools/ajdt/46/dev/update`           |

## <a name="anchor2">二、构建过程</a>

1. 安装JDK，配置环境变量**JAVA_HOME**和**Path**。

2. 安装Gradle，配置环境变量**GRADLE_HOME**、**GRADLE_USER_HOME**和**Path**。

3. 安装Eclipse。

4. 安装Eclipse插件，配置Gradle。

5. 使用Git进行Spring Framework源码的版本控制。

6. 执行Spring Framework源码中的**import-into-eclipse.bat**脚本，按照其中的步骤完成后续的源码导入工作。

## <a name="anchor3">三、遇到的问题</a>

1. spring-context和spring-web模块编译出错，如图所示：

![](blogs/images/1/3.1.1.jpg)

![](blogs/images/1/3.1.2.jpg)

解决办法如图所示：

![](blogs/images/1/3.1.3.jpg)

**PS**：添加Access Rule（Accessible，com/sun/net/httpserver/**）。

2. spring-build-src模块编译出错，如图所示：

![](blogs/images/1/3.2.1.jpg)

![](blogs/images/1/3.2.2.jpg)

解决办法如图所示：

![](blogs/images/1/3.2.3.jpg)

![](blogs/images/1/3.2.4.jpg)
