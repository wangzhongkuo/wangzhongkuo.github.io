# 开发环境

这里列出开发环境的配置和团队使用的协作系统。

## 源代码

#### 代码仓库 Github

#### [Git工作流说明](https://gist.github.com/Chaser324/ce0505fbed06b947d962)

#### [Git配置](https://intranet.rog2.org/docs/devenv/git/setup.md)

## JAVA

### JDK
本文描述SGSDK项目中做 Java 开发时，所使用的 JDK版本。

#### java -version

本项目使用 [Java 8]( https://openjdk.java.net/projects/jdk8/ ) 进行开发。

#### JDK Distribution

目前本地开发环境统一使用 [Amazon Corretto]( https://aws.amazon.com/cn/corretto/ )。
测试环境和生产环境，目前使用 [Open JDK]( https://openjdk.java.net/ )，jvm版本使用[1.8.0_144-b01]( https://www.oracle.com/technetwork/java/javase/downloads/java-archive-javase8-2177648.html)，后续将统一使用 [Amazon Corretto]( https://aws.amazon.com/cn/corretto/ )。

#### 下载

本地开发环境使用 Amazon Corretto-8.252.09.2 可以从 [Downloads for Amazon Corretto  8](https://docs.aws.amazon.com/corretto/latest/corretto-8-ug/downloads-list.html) 获得。
也可以从内网 [Downloads for Amazon Corretto  8](https://s3.intranet.rog2.org/minio/software/java/amazon-corretto/8.252.09.1/) 下载。

#### 安装

[java 8 User Guide](https://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html) 有各平台详细的安装步骤，按照文档操作即可。



### tomcat

本文描述SGSDK项目中做 Java 开发时，所使用的 tomcat版本。

#### 版本号

本项目使用 [tomcat 8]( http://tomcat.apache.org/ ) 进行开发。

#### 下载

最新的 tomcat 8 可以从 [Downloads Java  8](https://tomcat.apache.org/) 获得。

#### 安装

[tomcat 8 User Guide](https://tomcat.apache.org/) 有详细的安装步骤，按照文档操作即可。



### Maven

本文描述SGSDK项目中做 Java 开发时，所使用的 [Apache Maven](https://maven.apache.org/)。

#### 版本号

当前使用 [3.6.3](https://maven.apache.org/docs/3.6.3/release-notes.html) 进行开发和构建。

#### 下载

Maven 的安装包可以从 https://maven.apache.org/download.cgi 获得。

#### 配置

首先，安装 JDK(参照上文)。

接着，下载 Maven 并解压 **.zip** 到你中意的目录下，例如 `%USERPROFILE%\apps\maven`

以 Windows 举例，配置 **User** 级别的环境变量：

在 **Path** 中增加解压后的 **bin** 目录，例如 `%USERPROFILE%\apps\maven\apache-maven-3.6.3\bin`

验证：

```
Microsoft Windows [Version 10.0.18363.693]
(c) 2019 Microsoft Corporation. All rights reserved.

C:\Users\wangzhiguang>mvn --version
Apache Maven 3.6.3 (cecedd343002696d0abb50b32b541b8a6ba2883f)
Maven home: C:\Users\wangzhiguang\apps\maven\current\bin\..
Java version: 11.0.6, vendor: Amazon.com Inc., runtime: C:\Program Files\Amazon Corretto\jdk11.0.6_10
Default locale: en_US, platform encoding: GBK
OS name: "windows 10", version: "10.0", arch: "amd64", family: "windows"

C:\Users\wangzhiguang>
```

#### Maven Central 镜像

备注 (2020-03-07)

- 由于阿里云镜像从 **2019-11-15** 开始处于同步中断的状态，请切换回 Maven Central。

在配置文件中增加阿里云的 [Maven Central](https://maven.apache.org/repository/) 镜像，可改善下载速度和稳定性。

找到 `${user.home}/.m2/settings.xml`，若该文件不存在，可从 Maven 安装包中的 `conf/settings.xml` 复制而来。

找到 `` 部分，添加以下镜像配置：

```xml
<settings>
  ...
  <mirrors>
    <mirror>
      <id>aliyun</id>
      <name>Aliyun mirror of Maven Central</name>
      <url>https://maven.aliyun.com/repository/central/</url>
      <mirrorOf>central</mirrorOf>
    </mirror>
  </mirrors>
  ...
</settings>
```

关于仓库镜像配置的更详细内容，可阅读 [Using Mirrors for Repositories](https://maven.apache.org/guides/mini/guide-mirror-settings.html)。

#### 配置 Maven 私有仓库

参见 [Maven Repositories](https://intranet.rog2.org/docs/devenv/java/maven-repo.md)。



### IntelliJ IDEA

Use [IntelliJ IDEA](https://www.jetbrains.com/idea/) as team IDE.

#### Version

The IDEA version is [2020.1](https://www.jetbrains.com/idea/download/).

#### Download

| Platform        | Installer                                                    | Checksum                                                     |
| --------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **macOS/x64**   | [ideaIC-2020.1.dmg](https://s3.shiyou.kingsoft.com/software/idea/2020.1/ideaIC-2020.1.dmg) | [ideaIC-2020.1.dmg.sha256](https://s3.shiyou.kingsoft.com/software/idea/2020.1/ideaIC-2020.1.dmg.sha256) |
| **Windows/x64** | [ideaIC-2020.1.exe](https://s3.shiyou.kingsoft.com/software/idea/2020.1/ideaIC-2020.1.exe) | [ideaIC-2020.1.exe.sha256](https://s3.shiyou.kingsoft.com/software/idea/2020.1/ideaIC-2020.1.exe.sha256) |

#### IDEA Best Practices

- Settings in **File** -> **Settings** will only take effect in current project, but in **Other Settings** -> **Settings for New Projects** will take effect in global.
- IDEA synchronizes the Java version of the `Maven-Compiler-Plugin` which configured in the main pom.xml into the whole project without additional manual configuration.

#### Open Project

Select **File -> Open** choose main **pom.xml** which in target project. The dependent libraries configured in Maven will be downloaded automatically after the project opens.

#### Personal Settings

- Select **File** -> **Settings** -> **Appearance & Behavior** -> **Appearance** to set the `Appearance Font and Theme`(The recommendation is **Trebuchet MS 16** ).
- Select **File** -> **Settings** -> **Editor** -> **Color Scheme** -> **Color Scheme Font** to set the `Font of the editing area`(The recommendation is **Consolas 18** ).

#### Maven Settings

- Select **File** -> **Settings** -> **Build, Execution, Deployment** -> **Build Tools** -> **Maven** to set **Maven Home**。
- To configure Maven m2 wagon, please see [Maven Repositories](https://intranet.rog2.org/docs/devenv/java/maven-repo.md).
- After configuration, right click on the main **pom.xml** and choose **Reimport**, maven dependences will be download automatically.
- If download failed, please check settings.xml carefully.

#### Code Completion

Select **File** -> **Settings** -> **Editor** -> **General** -> **Code Completion** to adjust code completion.

- For unfamiliar methods, it is recommended to check `Show Full Method Signals` to prompt Javadocs.
- For function which has multiple parameters, it is recommended to check `Show parameter name hints on completion` to prompt parameter name.

#### Code Folding

Select **File -> Settings** -> **Editor** -> **General** -> **Code Folding** could customize whether some code blocks are folded up by default when open a file, such as import/SupressWarning or other code need to focus.

#### Tabs style

Select **File** -> **Settings** -> **Editor** -> **General** -> **Editor Tabs** could customize tabs, including display style and total counts, etc.

#### Code Templates

- SelectFile ->Settings -> Editor -> File and Code Templates in tabincludes, choose File Header, fill with

  ```java
  /**
  * @author ${USER} on ${YEAR}-${MONTH}-${DAY}
  */
  ```

  could customize the code templates. At the same time, make sure every kind of files in the tab files

  you needs has one line:

  ```
  #parse("File Header.java")
  ```

- You can click [HERE](https://s3.intranet.rog2.org/software/idea/settings.jar) to download **settings jar** and select **File** -> **Import Settings...** to import to your IDEA.



### MySQL

本文描述SGSDK项目中做 Java 开发时，所使用的 [MySQL](https://www.mysql.com/cn/)。

#### 版本号

开发环境和生产环境，均使用 [MySQL- 5.7.25](https://downloads.mysql.com/archives/community/)。

#### 下载

安装包可以从 [MySQL (Downloadable Version)](https://dev.mysql.com/downloads/mysql/) 获得。

#### 配置

首先，安装 JDK（参照上文）。

接着，下载 MySQL 并解压 **.zip** 到你中意的目录下，例如 `%USERPROFILE%\apps\mysql-local`

#### 运行

以 Windows 举例  在解压后的目录运行：

①以管理员身份打开命令行 下转到mysql的bin目录下：

②安装mysql的服务：mysqld --install

③初始化mysql，在这里，初始化会产生一个随机密码,如下图框框所示，记住这个密码，后面会用到(mysqld --initialize --console)

④开启mysql的服务(net start mysql)

#### 初始化项目数据库

使用项目 sql 目录中的 SQL 文件可在本地测试库中完成建库建表操作

xsjdb.sql 为 SDK 项目主数据库，包括用户、支付、应用信息、渠道信息等数据功能表

xsj_email.sql 为 SDK 邮件服务数据库，主要功能为邮件发送记录


### Memcached

本文描述SGSDK项目中做 Java 开发时，所使用的缓存数据库 [Memcached](https://memcached.org/)。

#### 版本号

开发环境和生产环境，均使用 [Memcached - 1.4.15](https://memcached.org/)。

#### 下载

安装包可以从 [Memcached (Downloadable Version)](https://github.com/memcached/memcached/wiki/ReleaseNotes) 获得。

#### 配置

首先，安装 JDK（参照上文）。

接着，下载 Memcached 并解压 **.zip** 到你中意的目录下，例如 `%USERPROFILE%\apps\memcached-local`

#### 运行

**Windows**

①以管理员身份打开命令行 下转到Memcached的目录下执行: memcached.exe -d install

② 然后使用下面的命令启动或停止memcached服务,

启动 :  memcached.exe -d start

停止 :  memcached.exe -d stop

卸载 :  memcached.exe -d uninstall

**Linux**

Requirements

- [libevent-2.0.21](https://s3.intranet.rog2.org/software/libevent/2.0.21/source/libevent-2.0.21-stable.tar.gz)

  Decompression

  `tar -xvf libevent-2.0.21-stable.tar.gz`

  Configure

  `./configure –prefix=/usr/local/libevent/2.0.21`

  Install

  `make && make install`

- [memcached-1.4.15](https://s3.intranet.rog2.org/software/memcached/1.4.15/source/memcached-1.4.15.tar.gz)

  Decompression

  `tar -xvf memcached-1.4.15.tar.gz`

  Configure

  `./configure --prefix=/usr/local/memcached/1.4.15 --with-libevent=/usr/local/libevent/2.0.21`

  Install

  `make && make install`

Run

`/usr/local/memcached/1.4.15/bin/memcached -vvv`


## 项目结构说明

bi	珠海 MBI 数据上报相关模块

|	-	bjob	数据上报任务模块，主要服务韩国仙剑4项目数据上报 MBI 系统（暂时停用）

channels	渠道功能模块，该模块内容最终将以单个jar包形式发布，并被 SDK 各业务模块依赖

|	-	app	原生移动应用类产品渠道

|	-	h5	H5 类游戏产品渠道

common	项目公共功能模块

|	-	conf_dev	测试环境配置文件

|	-	conf_prod	正式环境配置文件

|	-	common

​				|	-	config	SDK 私钥存放位置

​				|	-	dao	公共模型 dao 层处理类

​				|	-	datx	ip地址归属功能

​				|	-	filter	过滤模块，目前主要针对用户 token 有效性进行校验

​				|	-	repository	渠道 jar 包动态加载器

​				|	-	service	通用功能业务逻辑，如应用配置信息、用户黑名单等

email	邮件服务模块，主要用于 SDK 系统每日日报等功能发送邮件使用

frame	通用工具模块，包括 enum 、过滤器、id 生成器、memcache 模型、数据库操作类、常用工具方法等

model	功能模型模块，包含项目中所有使用到的数据表映射的模型类

pay	支付相关功能模块

|	-	pbase	支付模块公共功能

|	-	pchannel	渠道通用支付方法模块

|	-	pinner	供平台内部系统调用功能模块，支付相关

|	-	pjob	订单定时任务模块，主要用于订单扫描及自动补单

|	-	pmall	平台商城功能模块，支付相关

|	-	pout	官网支付订单相关功能模块，主要服务于 SDK 客户端及游戏 CP ，包括：创建支付订单、支付订单状态更新等功能

|	-	pserver	第三方支付渠道功能模块，如： PayPal 这类仅提供收付款功能的渠道用此模块接入

|	-	psgop	平台后台系统调用功能模块，支付相关

server	游戏服务器信息管理模块，主要用于平台收集游戏服务器信息，以便提供给平台相关功能使用

statistical	数据统计模块（暂时停用）

user	用户相关功能模块

|	-	ubase	用户模块公共功能

|	-	uchannel	渠道通用用户方法模块

|	-	ucpserver	后续预留给 CP 调用的功能聚合模块（暂时未启用）

|	-	uinner	供平台内部系统调用功能模块，用户相关

|	-	umall	平台商城功能模块，用户相关

|	-	uout	官网用户相关功能模块，主要服务于 SDK 客户端及游戏 CP ，包括：账号注册、登录、退出等

|	-	usgop	平台后台系统调用功能模块，用户相关

## 项目使用说明

目前项目打包方式:
    
|	-	默认国内测试环境 例 :
        |	-	命令行 : sudo mvn clean package -pl user/uout -am 
        |	-	Terminal : mvn clean package -pl user/uout -am
    
|	-	国内正式环境 例 :
        |	-	命令行 : sudo mvn clean package -Pprod_cn -pl user/uout -am 
        |	-	Terminal : mvn clean package -Pprod_cn -pl user/uout -am
    
|	-	国外测试环境 例 :
        |	- 命令行 : sudo mvn clean package  -Pdev_hw -pl user/uout -am 
        |	- Terminal : mvn clean package -Pdev_hw -pl user/uout -am
        
|	-	国外正式环境 例 :
        |	-	命令行 : sudo mvn clean package -Pprod_hw -pl user/uout -am 
        |	-	Terminal : mvn clean package -Pprod_hw -pl user/uout -am
    
    
channels 渠道功能模块中的app与h5模块内子渠道命名区分国内海外;                                              
        |	-	国内渠道项目名以cn开头, 例:
                |	-	 app端: cn_app_oppo   
                |	-	 h5端: cn_h5_oppo                                          
        |	-	海外渠道项目名以hw开头, 例:
                |	-	 app端: hw_app_oppo
                |	-	 app端: hw_h5_oppo 
        |	-	模块中的app与h5模块内子渠道 pom 中 build 下的 finalName 命名遵循下列规范;         
                |	-	渠道code名称_渠道模块上级名_当前渠道服务端版本  例 : oppo_app_1.0 或 oppo_h5_1.0
