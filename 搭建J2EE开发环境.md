# <a name="top">搭建J2EE开发环境</a>
* [一、安装JDK](#jdk)
* [二、安装Tomcat](#tomcat)
* [三、安装Eclipse](#eclipse)
* [四、安装MySQL](#mysql)
* [五、安装Git](#git)
* [六、安装Maven](#maven)

## <a name="jdk">一、安装JDK</a>[【TOP】](#top)
1. 安装包：jdk-8u131-windows-x64.exe
2. 下载地址：http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html
3. 安装步骤：
```
(1)、安装jdk-8u131-windows-x64.exe，默认选项安装即可；
(2)、配置环境变量：
    在系统环境变量中增加变量JAVA_HOME，变量值为JDK的安装路径（如：C:\Program Files\Java\jdk1.8.0_131），并在
    Path环境变量中增加JDK的bin路径（%JAVA_HOME%\bin）。
```

## <a name="tomcat">二、安装Tomcat</a>[【TOP】](#top)
1. 安装包：apache-tomcat-7.0.78.zip
2. 下载地址：http://tomcat.apache.org/download-70.cgi
3. 安装步骤：
```
将安装包直接解压到硬盘中即可，如F盘。
```

## <a name="eclipse">三、安装Eclipse</a>[【TOP】](#top)
1. 安装包：eclipse-jee-neon-3-win32-x86_64.zip
2. 下载地址：https://www.eclipse.org/downloads/download.php?file=/technology/epp/downloads/release/neon/3/eclipse-jee-neon-3-win32-x86_64.zip
3. 安装步骤：
```
(1)、将安装包直接解压到硬盘中，如F盘；
(2)、设置用4个空格代替Tab键：
    Window -> Preferences -> General -> Editors -> Text Editors，将“Insert spaces for tabs”选项勾选上，并
    确认“Displayed tab width”的值是否为数字4，另外，也可将“Show whitespace characters(configure visibility)”
    选项勾选上，用于将空白字符及换行符显示出来。
    Window -> Preferences -> Java -> Code Style -> Formatter，由于“Eclipse [built-in]”样式模板修改不了，所以
    可先基于该模板新建一个属于自己的样式模板，然后进入模板配置页面的“Indentation”选项卡，将“General settings”中的
    “Tab policy”的值设置为“Spaces only”，另外，也可将“Line Wrapping”选项卡“General settings”中的“Maximum line
    width”的值设为120，表示格式化代码时，超过120个字符将会自动换行。
(3)、设置换行符使用Unix格式：
    Window -> Preferences -> General -> Workspace，将“New text file line delimiter”的值设置为“Unix”。
(4)、设置文件字符编码为UTF-8：
    Window -> Preferences -> General -> Workspace，将“Text file encoding”的值设置为“UTF-8”。
    Window -> Preferences -> General -> Content Types，选择“Text”中的“Java Properties File”，将底下的“Default
    encoding”的值设置为“UTF-8”。
(5)、设置主题风格：
    先在[Eclipse Color Themes](http://www.eclipsecolorthemes.org/)下载自己喜欢的主题风格（如：Obsidian.epf），
    然后通过File -> Import... -> General -> Preferences将所下载的EPF文件导入即可。
(6)、设置默认JDK版本：
    Window -> Preferences -> Java -> Installed JREs，在此增加已安装的JDK版本（如：jdk1.8.0_131），并勾选上作为
    默认版本。
    Window -> Preferences -> Java -> Compiler，将“JDK Compliance”中的“Compiler compliance level”的值设置为
    默认JDK版本（如：1.8）。
```

## <a name="mysql">四、安装MySQL</a>[【TOP】](#top)
1. 安装包：mysql-5.6.33-winx64.zip
2. 下载地址：https://dev.mysql.com/downloads/mysql/5.6.html#downloads
3. 安装步骤：
```
(1)、将安装包直接解压到硬盘中，如F盘MySQL文件夹中，并将解压后的文件夹改名为MySQL Server 5.6；
(2)、配置环境变量：
    在Path环境变量中增加MySQL的bin路径（F:\MySQL\MySQL Server 5.6\bin）；
(3)、配置MySQL：
    进入MySQL安装目录（F:\MySQL\MySQL Server 5.6），拷贝一份my-default.ini配置文件，并更名为my.ini，在其中增加以下配置项：
    [mysqld]
    ...
    basedir=F:\MySQL\MySQL Server 5.6
    datadir=F:\MySQL\MySQL Server 5.6\data
    port=3306
    ...
(4)、运行cmd，执行以下命令安装MySQL：
    F:
    cd F:\MySQL\MySQL Server 5.6\bin
    mysqld -install
    PS：卸载MySQL可在cmd中执行“mysqld -remove”命令。
(5)、MySQL安装成功后，继续执行以下命令启动MySQL服务：
    net start mysql
    PS：停止MySQL服务可在cmd中执行“net stop mysql”命令。
(6)、MySQL服务启动后，可执行以下命令进入MySQL命令行：
    mysql -uroot -p
    PS：第一次执行该命令不用输入密码，直接回车即可。
(7)、配置MySQL字符编码：
    修改my.ini配置文件，在其中增加以下配置项：
    [mysqld]
    ...
    port=3306
    character_set_server=utf8
    ...
    [client]
    port=3306
    default-character-set=utf8
    然后重启MySQL服务即可。
    PS：可在MySQL命令行中执行“show variables like 'char%';”命令查看字符编码。
(8)、配置root用户密码：
    MySQL服务启动后，在cmd中执行以下命令：
    mysqladmin -uroot -p password rootroot
    密码修改成功后即可执行“mysql -uroot -prootroot”命令进入MySQL命令行了。
(9)、配置MySQL允许远程连接：
    进入MySQL命令行，执行以下SQL：
    GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'rootroot' WITH GRANT OPTION;
    FLUSH PRIVILEGES;
```

## <a name="git">五、安装Git</a>[【TOP】](#top)
1. 安装包：Git-2.13.0-64-bit.exe
2. 下载地址：https://github.com/git-for-windows/git/releases/download/v2.13.0.windows.1/Git-2.13.0-64-bit.exe
3. 安装步骤：
```
(1)、安装Git-2.13.0-64-bit.exe，默认选项安装即可；
(2)、注册GitHub账号，如有则跳过；
(3)、运行Git Bash，执行以下命令配置Git：
    git config --global user.name "Your Name"              ##配置用户名
    git config --global user.email "email@example.com"     ##配置用户邮箱
    git config --global core.autocrlf false                ##配置提交时不自动转换换行符
    git config --global core.safecrlf true                 ##配置拒绝提交包含混合换行符的文件
(4)、运行cmd，执行以下命令创建SSH Key：
    ssh-keygen -t rsa -C "email@example.com"
    说明：该命令执行过后，会在用户的主目录（如：C:\Users\Administrator）下生成.ssh文件夹，文件夹里面有id_rsa和
    id_rsa.pub两个文件，这两个文件是SSH Key的秘钥对，其中，id_rsa是私钥，id_rsa.pub是公钥。
(5)、将SSH Key公钥添加到GitHub中，过程如下：
    登陆GitHub -> Settings -> SSH and GPG keys -> Add SSH key，在Key文本框中粘贴id_rsa.pub文件的内容即可。
```
**PS**：当第一次使用Git的clone或者push命令连接GitHub时，会出现如下警告：
```
The authenticity of host 'github.com (xx.xx.xx.xx)' can't be established.
RSA key fingerprint is xx.xx.xx.xx.xx.
Are you sure you want to continue connecting (yes/no)?
```
这是因为Git连接GitHub时使用的是SSH连接，而SSH连接在第一次验证GitHub服务器的Key时，需要确认GitHub的Key的指纹信息是否真的来自GitHub服务器，此时只需输入yes回车即可。

## <a name="maven">六、安装Maven</a>[【TOP】](#top)
1. 安装包：apache-maven-3.5.0-bin.zip
2. 下载地址：https://archive.apache.org/dist/maven/maven-3/3.5.0/binaries/
3. 安装步骤：
```
(1)、将安装包直接解压到硬盘中，如F盘；
(2)、配置环境变量：
    在系统环境变量中增加变量M2_HOME，变量值为Maven的安装路径（如：F:\apache-maven-3.5.0），并在Path环境变量中
    增加Maven的bin路径（%M2_HOME%\bin）；
(3)、配置Maven本地仓库：
    先从Maven安装路径的conf文件夹下拷贝settings.xml配置文件至用户主目录的.m2文件夹中，并在配置文件中增加如下配置：
    <settings>
        ...
        <localRepository>F:\maven\repository</localRepository>
        ...
    </settings>
    说明：“F:\maven\repository”即为自行创建的Maven本地仓库地址。
```
