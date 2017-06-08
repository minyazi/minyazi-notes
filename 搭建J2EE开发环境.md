# <a name="top">搭建J2EE开发环境</a>
* [一、安装JDK](#jdk)
* [二、安装Eclipse](#eclipse)
* [三、安装Tomcat](#tomcat)
* [四、安装MySQL](#mysql)
* [五、安装Git](#git)
* [六、安装Maven](#maven)

## <a name="jdk">一、安装JDK</a>[【TOP】](#top)
1. 安装包：jdk-8u131-windows-x64.exe
2. 下载地址：http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html
```

```

## <a name="eclipse">二、安装Eclipse</a>[【TOP】](#top)
1. 安装包：eclipse-jee-neon-3-win32-x86_64.zip
2. 下载地址：https://www.eclipse.org/downloads/download.php?file=/technology/epp/downloads/release/neon/3/eclipse-jee-neon-3-win32-x86_64.zip
```

```

## <a name="tomcat">三、安装Tomcat</a>[【TOP】](#top)
1. 安装包：
2. 下载地址：
```

```

## <a name="mysql">四、安装MySQL</a>[【TOP】](#top)
1. 安装包：
2. 下载地址：
```

```

## <a name="git">五、安装Git</a>[【TOP】](#top)
1. 安装包：Git-2.13.0-64-bit.exe
2. 下载地址：https://github.com/git-for-windows/git/releases/download/v2.13.0.windows.1/Git-2.13.0-64-bit.exe
3. 安装步骤
```
(1)、安装Git-2.13.0-64-bit.exe，默认选项安装即可；
(2)、注册GitHub账号，如有则跳过；
(3)、运行Git Bash，执行以下命令配置Git：
    git config --global user.name "Your Name"              ##配置用户名
    git config --global user.email "email@example.com"     ##配置用户邮箱
    git config --global core.autocrlf false                ##配置提交时不自动转换换行符
    git config --global core.safecrlf true                 ##配置拒绝提交包含混合换行符的文件
(4)、打开DOS命令行界面，执行以下命令创建SSH Key：
    ssh-keygen -t rsa -C "email@example.com"
    说明：该命令执行过后，会在用户的主目录（如：C:\Users\Administrator）下生成.ssh文件夹，文件夹里面有id_rsa和id_rsa.pub两个文件，这两个文件
    是SSH Key的秘钥对，其中，id_rsa是私钥，id_rsa.pub是公钥。
(5)、将SSH Key公钥添加到GitHub中，过程如下：
    
```

## <a name="maven">六、安装Maven</a>[【TOP】](#top)
1. 安装包：apache-maven-3.5.0-bin.zip
2. 下载地址：https://archive.apache.org/dist/maven/maven-3/3.5.0/binaries/
```

```
