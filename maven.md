# 自动化构建工具 Maven

maven 是 apache 基金会的开源项目

---

# 1.简介

## 1.1 Maven作用

---

1. 项目的自动构建，帮助开发人员做项目代码的编译，测试，打包，安装，部署等工作
2. 管理依赖（管理项目中使用的各种 jar 包）



## 1.2 Maven 中的概念

---

>1. POM
>2. 约定的目录结构
>3. 坐标
>4. 依赖管理
>5. 仓库管理
>6. 生命周期
>7. 插件与目标
>8. 继承
>9. 聚合



## 1.3 Maven 工具的获取

---

[Maven – Welcome to Apache Maven](https://maven.apache.org/)

1. 确定 JAVA_HOME 指定的 jdk 安装路径
2. 解压缩 apache-maven-3.3.9.-bin.zip
3. 把 maven 安装目录中下载的 bin 的路径添加到 path 中
4. 测试 maven 的安装，在命令行执行 `mvn -v`

# 2.Maven 的核心概念

---



## 2.1 约定的目录结构

---

maven 项目使用的大多人遵循的目录结构，叫做约定的目录结构。

一个 maven 项目就是一个文件夹。例如这个项目叫做 hello

```java
hello	项目文件夹
    \src
    	\main	主程序目录：完成项目功能的代码和配置文件
    		\java	源代码：饱和相关类的定义
    		\resources	配置文件
    	\test	测试程序代码
    		\java
    		\resources
    \pom.xml
```

Maven 的使用方式：1.独立使用；2.和idea一起使用



独立使用：

> ```java
> package com.lzy;
> 
> public class HelloMaven{
> 	
> 	public int add(int a, int b){
> 		System.out.println("HelloMaven add!");
> 		return a + b;
> 	}
> 
> 	public static void main(String[] args){
> 		HelloMaven helloMaven = new HelloMaven();
> 		System.out.println(helloMaven.add(1, 2));
> 	}
> 	
> }
> ```
>
> 在 pom.xml 所在的文件夹执行 `mvn compile`
>
> ![image-20220722164551972](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20220722164551972.png)
>
> 会在该目录下生成一个 target 文件夹里面有编译的 .class 文件
>
> ![image-20220722164950863](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20220722164950863.png)





## 2.2 POM

---

POM：Project Object Model 项目对象模型，maven 把项目当成模型处理。通过 pom.xml 完成项目的构建和依赖的管理。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!-- project 是根标签，后面是约束文件 -->
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <!-- pom 模型版本 -->
  <modelVersion>4.0.0</modelVersion>
  <!-- 坐标 -->
  <groupId>com.bjpowernode</groupId>
  <artifactId>ch01-maven</artifactId>
  <version>1.0-SNAPSHOT</version>
  
  <properties>
     <java.version>1.8</java.version>
     <maven.compiler.source>1.8</maven.compiler.source>
     <maven.compiler.target>1.8</maven.compiler.target>
  </properties>
  
</project>

```



## 2.3 坐标

---

坐标的作用：确定资源，是资源的唯一标识。在 maven 中，每个资源都是有坐标的。坐标是唯一的，简称 gav

```xml
<!-- 坐标 -->
<!-- groupId:组织名称，代码。公司，团体或单位的标识 -->
<groupId>com.bjpowernode</groupId>
<!-- artifactId:项目名称，若groupId中有项目，此时当前的值就是子项目名。项目名称唯一 -->
<artifactId>ch01-maven</artifactId>
<!-- version:项目的版本号 -->
<version>1.0-SNAPSHOT</version>
```

- 每一个 maven 项目，都需要一个自己的 gav
- 管理依赖，需要使用其他的 jar 也需要 gav



## 2.4 依赖 dependency

---

依赖：项目中使用的其他资源 jar

需要使用 maven 管理依赖。通过使用 dependency 和 gav 一起完成依赖的管理。

在 pom.xml 配置文件中，使用标签 `dependencies` `dependency`标签，还有 gav 完成依赖的说明。

```xml
<dependencies>
    <!-- 导入日志 jar 包为例-->
	<dependency>
		<groupId>log4j</groupId>
		<artifactId>log4j</artifactId>
		<version>1.2.17</version>
    </dependency>
</dependencies>
<!-- maven 以 gav 为标识，从互联网下载依赖的 jar 到本机上，由 maven 管理这些 jar -->
```



## 2.5 仓库

---

Maven 仓库存放：

1. maven 工具自己的 jar 包
2. 第三方的其他 jar 包
3. 自己写的程序，可以打包为 jar ，保存在仓库中



仓库分类：

1. 本地仓库：默认在 c盘当前用户的目录下；通过修改 maven 工具的配置文件（maven 的安装路径 `\conf\setting.xml`）来更改本地仓库位置

   >创建一个目录，作为仓库使用。目录中不要有中文和空格
   >
   >修改 setting.xml 文件指定，我们自己创建的仓库路径
   >
   >```xml
   ><localRepository>E:\openrepository</localRepository>
   >```

2. 私服，公司自己的 maven 服务器

3. 中央仓库或者中央仓库的镜像 [Maven Repository: Search/Browse/Explore (mvnrepository.com)](https://mvnrepository.com/)

![image-20220722192455395](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20220722192455395.png)



## 2.6 maven 的生命周期，插件和命令

---

**maven 的生命周期**：项目构建的各个阶段。清理，编译，测试，报告，打包，安装，部署

**插件**：要完成构建项目的各个阶段，要使用 maven 的命令，执行命令的功能是通过插件完成的。插件就是 jar ，一些类。

**命令**：执行 maven 功能是由命令发出的

> `mvn clean`：清理之前生成的数据，删除 target 目录 
>
> `mvn compile`：编译代码
>
> `mvn test-compile`：编译代码，编译 src/test/java 目录中的源文件，生成的 class 拷贝到 target/test-classes 目录。同时把 src/test/sources 目录中的文件拷贝到 test-classes 目录
>
> `mvn test`：测试命令，执行 test-classes 目录下文件
>
> `mvn package`：打包，把项目中的资源 class 文件和配置文件都放到一个压缩文件中，默认压缩文件是 jar 类型的。web 应用是 war 类型。
>
> `mvn install`：把生成的打包文件安装到 maven 仓库中

设置插件：

```xml
<!-- 设置构建项目相关内容 -->
<build>
	<plugins>
        <!-- 设置插件 -->
		<groupId>org.apache.maven.plugins</groupId>
		<artifactId>maven-compiler-plugin</artifactId>
		<version>3.8.1</version>
		<configuration>
            <!-- 指定编译代码的 jdk 版本 -->
            <source>1.8</source>
            <!-- 指定运行代码的 jdk 版本 --> 
            <target>1.8</target>
		</configuration>
    </plugins>
</build>
```





# 3. Maven 在 idea 中的使用

---



## 3.1 idea 中集成 Maven

---

idea 中自带一个 maven。我们要让 idea 使用自己安装的 maven

![image-20220722205248745](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20220722205248745.png)

`-DarchetypeCatalog=internal`

![image-20220722205754563](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20220722205754563.png)

这样配置后在当前项目是有效的。我们还需要在导入其他项目时也生效的时候，还应该：

![image-20220722210210564](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20220722210210564.png)在这里再配置一遍。



## 3.2 创建基于 maven 的普通 java 项目

---

普通项目创建选择模板

![image-20220722211215352](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20220722211215352.png)



## 3.3 创建 web项目

---

![image-20220722215722616](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20220722215722616.png)

手动在 pom.xml 中配置还需要的依赖

```xml
<!-- servlet 依赖 -->
<dependency>
    <groupId>javax.servlet</groupId>
    <artifactId>javax.servlet-api</artifactId>
    <version>4.0.1</version>
    <scope>provided</scope>
</dependency>

<!-- jsp 依赖 -->
<dependency>
    <groupId>javax.servlet.jsp</groupId>
    <artifactId>javax.servlet.jsp-api</artifactId>
    <version>2.3.3</version>
    <scope>provided</scope>
</dependency>
```

![image-20220722221907274](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20220722221907274.png)

与 tomcat 加载的区别，servlet jar 不在使用 tomcat 自带的 jar 包，使用的是我们自己仓库中的 jar 包，由 maven 管理。



## 3.4 导入模块到 idea

![image-20220722230525611](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20220722230525611.png)

![image-20220722230558691](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20220722230558691.png)

![image-20220722231011318](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20220722231011318.png)



# 4. 依赖管理

---



## 4.1 依赖范围

---

```xml
<dependency>
    <groupId>javax.servlet</groupId>
    <artifactId>javax.servlet-api</artifactId>
    <version>4.0.1</version>
    <!-- scope 标签指定依赖范围 -->
    <scope>provided</scope>
</dependency>
```

依赖范围表示：这个依赖在项目构建的哪个阶段起作用。

- compile：默认，参与构建项目的所有阶段
- test：测试阶段使用
- provided：提供者，项目在部署到服务器时，不需要依赖这个 jar 包，而是会由服务器提供依赖的 jar 包。例如 servelet，j's'p

![image-20220722231940388](https://taro-note-pic.oss-cn-hangzhou.aliyuncs.com/image-20220722231940388.png)



# 5. Maven 常用设置

---



## 5.1 自定义变量

---

properties标签 里面的配置

```xml
<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding> 项目构建使用的字符集
    <project.report.outputEncoding>UTF-8</project.report.outputEncoding> 生成报告使用的字符集
    <maven.compiler.source>1.7</maven.compiler.source>源码编译 jdk 版本
    <maven.compiler.target>1.7</maven.compiler.target>运行代码的 jdb 版本
</properties>
```

在 properties 定义标签，这个标签就是一个变量，标签的文本就是变量的值。

**使用全局变量表示多个依赖使用的版本号**

1. 在 properties 标签中，定义一个标签，指定版本的值

   ```xml
   <properties>
   	...
       <!-- 自定义变量 servlet.version 自定义变量名，标签内变量值-->
       <servlet.version>4.0.1</servlet.version>
   </properties>
   ```

2. 使用全局变量，语法`${变量名}`

   ```xml
   <dependencies>
   
       <dependency>
         <groupId>javax.servlet</groupId>
         <artifactId>javax.servlet-api</artifactId>
         <!-- 自定义全局变量的使用 -->
         <version>${servlet.version}</version>
         <scope>provided</scope>
       </dependency>
       
       ...
       
     </dependencies>
   ```



## 5.2 指定资源位置

---

处理配置文件信息，maven 默认处理配置文件

1. maven 会把 src/main/resources 目录中文件，拷贝到 target/classes 目录下
2. maven 只处理 src/main/java 目录中的 .java 文件，把这些 java 文件编译位 .class，拷贝到 traget/classes 目录中。不处理其他文件。

所以当我们需要拷贝其它资源到 raget/classes 目录中时，就需要配置**资源插件**来帮助我们完成。不要为了插件需要配置在 bulid 标签中。

```xml
<build>
    <!-- 资源插件 -->
    <resources>
        <resource>
            <directory>src/main/java</directory>
            <includes>
                <!-- 包括目录下的 .properties, .xml 文件都会扫描到 -->
                <include>**/*.properties</include>
                <include>**/*.xml</include>
            </includes>
            <!-- filtering 选项 false 不启用过滤器 *.properties 已经起到过滤作用-->
            <filtering>false</filtering>
        </resource>
    </resources>
</build>
```
