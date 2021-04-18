---
title: sonar代码质量分析工具介绍
tags: [sonar, 代码质量]
keywords: 'sonar,代码质量'
categories: []
abbrlink: so0345BEkZBmgm
date: 2021-03-26 20:35:26
description:
cover:
top_img:
---

sonar是一款静态代码质量分析工具，支持Java、Python、PHP、JavaScript、CSS等25种以上的语言，而且能够集成在IDE、Jenkins、Git等服务中，方便随时查看代码质量分析报告；

sonar通过配置的代码分析规则，从可靠性、安全性、可维护性、覆盖率、重复率等方面分析项目，风险等级从A~E划分为5个等级；

同时，sonar可以集成pmd、findbugs、checkstyle等插件来扩展使用其他规则来检验代码质量；


参考讲解： <https://www.cnblogs.com/lfpriest/p/13366171.html>


## 工作流程

1. 开发人员在其IDE中进行编码，并使用SonarLint运行本地分析。
2. 开发人员将其代码推送到他们最喜欢的SCM中：git，SVN，TFVC等。
3. Continuous Integration Server会触发自动构建，并执行运行SonarQube分析所需的SonarScanner。
4. 分析报告将发送到SonarQube服务器进行处理。
5. SonarQube Server处理分析报告结果并将其存储在SonarQube数据库中，并在UI中显示结果。
6. 开发人员通过SonarQube UI审查，评论，挑战他们的问题，以管理和减少技术债务。
7. 经理从分析中接收报告。Ops使用API​​自动执行配置并从SonarQube提取数据。运维人员使用JMX监视SonarQube Server。


## 环境配置


### 1. 添加maven配置​

```xml
            <plugin>
                <groupId>org.sonarsource.scanner.maven</groupId>
                <artifactId>sonar-maven-plugin</artifactId>
                <version>3.6.1.1688</version>
            </plugin>​


```

### 2. 在setting文件中添加sonar配置

```xml
        <profile>
              <id>sonar</id>
              <activation>
                  <activeByDefault>true</activeByDefault>
              </activation>
              <properties>
                  <sonar.host.url>
                      http://192.168.1.1:9000
                  </sonar.host.url>
                  <sonar.branch.name>
                      walter
                  </sonar.branch.name>
           
              </properties>
        </profile>
```

## 3. Sonar规则扫描

如果有新增代码执行命令

```shell
mvn clean test verify sonar:sonar
```
