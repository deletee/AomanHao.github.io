---
title: 数据结构相关_6_16
date: 2018-07-10 21:48:00
tags: [GitHub, Mysql, Java, Maven]
---


Maven项目配置

<!--more-->

pom.xml配置

## 配置编码格式为UTF-8

```
<properties>
		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
		<project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
		<maven.compiler.encoding>UTF-8</maven.compiler.encoding>
		<spring.version>5.0.6.RELEASE</spring.version>//配置统一版本号
</properties>
```

## 配置编程环境版本 maven配置

```
	<build>
		<finalName>pp</finalName>
		<plugins>
			<plugin>
				<groupId>org.apache.maven.plugins</groupId>
				<artifactId>maven-compiler-plugin</artifactId>
				<version>3.7.0</version>
				<configuration>
					<source>1.8</source>
					<target>1.8</target>
				</configuration>
			</plugin>
		</plugins>
	</build>
```