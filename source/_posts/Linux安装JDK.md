---
title: Linux安装JDK
categories:
  - Linux
tags:
  - Linux
  - JDK
abbrlink: 1441854962
date: 2023-08-31 15:49:54
---

<a name="PHhuz"></a>

## 1、CentOS安装JDK

>
jdk1.8下载地址：[https://www.oracle.com/java/technologies/javase/javase-jdk8-downloads.html](https://www.oracle.com/java/technologies/javase/javase-jdk8-downloads.html)
>
jdk11下载地址：[https://www.oracle.com/java/technologies/javase-jdk11-downloads.html](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html)
>
jdk14下载地址：[https://www.oracle.com/java/technologies/javase-jdk14-downloads.html](https://www.oracle.com/java/technologies/javase-jdk14-downloads.html)

<a name="sacTz"></a>

### A、方式一（rpm方式）

```shell
#需要提前下载好rpm包
#安装之前检测jdk是否安装
rpm -qa | grep java

#执行安装
rpm -ivh jdk-8u251-linux-x64.rpm 

#检测jdk版本
java -version

```

<a name="owtxu"></a>

### B、方式二（压缩包）

```shell
#需要提前下载好jdk-8u251-linux-x64.tar.gz
tar -zvxf jdk-8u251-linux-x64.tar.gz

#配置环境变量
sudo vi /etc/profile

#将一下配置添加到文件末尾（注意JAVA_HOME的位置）
#java
export JAVA_HOME=/usr/java/jdk1.8.0_181
export PATH=$JAVA_HOME/bin:$PATH
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib



sudo tee /etc/profile <<-'EOF'
export JAVA_HOME=/home/yongzheng/application/jdk/jdk1.8.0_301
export PATH=$JAVA_HOME/bin:$PATH
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib
export M2_HOME=/home/yongzheng/application/maven
export PATH=$PATH:$M2_HOME/bin
EOF

#重新加载配置
source /etc/profile

#验证码
java -version


#MAC
sudo tee ~/.bash_profile <<-'EOF'
export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0_333.jdk/Contents/Home
export M2_HOME=/Library/Java/Maven/apache-maven-3.8.6
export GRADLE_HOME=/Library/Java/Gradle/gradle-7.4.2
export GRADLE_USER_HOME=/Library/Java/Repository

export PATH=$JAVA_HOME/bin:$M2_HOME/bin:$GRADLE_HOME/bin:$PATH
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib

EOF

```

<a name="7GrzW"></a>

### C、方式三（yum）

```bash
#搜索jdk安装包
yum search java|grep jdk

#搜索jdk 1.8.0版本
yum search java|grep jdk | grep 1.8.0

Repodata is over 2 weeks old. Install yum-cron? Or run: yum makecache fast
java-1.8.0-openjdk.i686 : OpenJDK Runtime Environment 8
java-1.8.0-openjdk.x86_64 : OpenJDK Runtime Environment 8
java-1.8.0-openjdk-accessibility.i686 : OpenJDK accessibility connector
java-1.8.0-openjdk-accessibility.x86_64 : OpenJDK accessibility connector
java-1.8.0-openjdk-accessibility-debug.i686 : OpenJDK 8 accessibility connector
java-1.8.0-openjdk-accessibility-debug.x86_64 : OpenJDK 8 accessibility
java-1.8.0-openjdk-debug.i686 : OpenJDK Runtime Environment 8 with full debug on
java-1.8.0-openjdk-debug.x86_64 : OpenJDK Runtime Environment 8 with full debug
java-1.8.0-openjdk-demo.i686 : OpenJDK Demos 8
java-1.8.0-openjdk-demo.x86_64 : OpenJDK Demos 8
java-1.8.0-openjdk-demo-debug.i686 : OpenJDK Demos 8 with full debug on
java-1.8.0-openjdk-demo-debug.x86_64 : OpenJDK Demos 8 with full debug on
java-1.8.0-openjdk-devel.i686 : OpenJDK Development Environment 8
java-1.8.0-openjdk-devel.x86_64 : OpenJDK Development Environment 8
java-1.8.0-openjdk-devel-debug.i686 : OpenJDK Development Environment 8 with
java-1.8.0-openjdk-devel-debug.x86_64 : OpenJDK Development Environment 8 with
java-1.8.0-openjdk-headless.i686 : OpenJDK Headless Runtime Environment 8
java-1.8.0-openjdk-headless.x86_64 : OpenJDK Headless Runtime Environment 8
java-1.8.0-openjdk-headless-debug.i686 : OpenJDK Runtime Environment with full
java-1.8.0-openjdk-headless-debug.x86_64 : OpenJDK Runtime Environment with full
java-1.8.0-openjdk-javadoc.noarch : OpenJDK 8 API documentation
java-1.8.0-openjdk-javadoc-debug.noarch : OpenJDK 8 API documentation for
java-1.8.0-openjdk-javadoc-zip.noarch : OpenJDK 8 API documentation compressed
java-1.8.0-openjdk-javadoc-zip-debug.noarch : OpenJDK 8 API documentation
java-1.8.0-openjdk-src.i686 : OpenJDK Source Bundle 8
java-1.8.0-openjdk-src.x86_64 : OpenJDK Source Bundle 8
java-1.8.0-openjdk-src-debug.i686 : OpenJDK Source Bundle 8 for packages with
java-1.8.0-openjdk-src-debug.x86_64 : OpenJDK Source Bundle 8 for packages with

#安装下载jdk1.8，下载之后默认的目录为： /usr/lib/jvm/
yum install java-1.8.0-openjdk


#验证码
java -version
```

<a name="aUpZZ"></a>

## 2、Ubuntu安装JDK

<a name="b2kF5"></a>

### A、方式一

```shell
#搜索可用jdk列表
sudo apt search openjdk-8

#安装jdk
sudo apt-get install openjdk-8-jdk


#验证码
java -version
```

<a name="txhv5"></a>

### B、方式二（压缩包）

```shell
#需要提前下载好jdk-8u251-linux-x64.tar.gz
tar -zvxf jdk-8u251-linux-x64.tar.gz

#配置环境变量
sudo vi /etc/profile

#将一下配置添加到文件末尾（注意JAVA_HOME的位置）
#java
export JAVA_HOME=/usr/java/jdk1.8.0_181
export PATH=$JAVA_HOME/bin:$PATH
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib

#重新加载配置
source /etc/profile

#验证码
java -version

```


