# macOS Homebrew安装JDK的一些问题
***目录***  
[JDK8~JDK10/OpenJDK/AdoptOpenJDK](#JDK8~JDK10/OpenJDK/AdoptOpenJDK)  
[JDK12/JDK13/OracleJDK](#JDK12/JDK13/OracleJDK)  
[JDK7/Zulu](#JDK7/Zulu)  
[JDK6](#JDK6)  

---
#### [Homebrew](https://brew.sh/index_zh-cn)就不多做介绍了，开发人员肯定耳熟能详。这里推荐大家一篇：
> 1. [用 Homebrew 带飞你的 Mac](https://segmentfault.com/a/1190000014541169)
> 2. [我在 Mac 上都用什么](https://www.cnblogs.com/imzhizi/p/my-apps-on-mac.html)  

自从`Oracle`接手JDK之后，更新变快了，之前的“旧版本”也不容易下载了。最近一段时间`Oracle`一直不安生, 搞出来一堆幺蛾子, 所以安装方式也一直在变, 之前的方法已经不能用了, 网上找各种办法都不好使，下面针对各个版本给出了不同建议, 安装结束后, 可输入```java -version```确认是否安装成功。

## JDK8~JDK10/OpenJDK/AdoptOpenJDK
这些都是比较主流的JDK版本, 目前大多数企业还在使用,但想要通过 Homebrew 却并不容易,网上查询的`90%`Homebrew安装JDK8的方式都是不能用的, 必须要寻求开源世界的帮助, 对于 JDK8 ~ JDK10, 这时会推荐 AdoptOpenJDK.

AdoptOpenJDK 是免费的、完全无品牌的 OpenJDK 版本，基于 GPL 开源协议（+Classpath Extension），以免费软件的形式提供社区版的 OpenJDK 二进制包，公司也可安全且放心使用。与由 Oracle 的 OpenJDK 构建版本不同，这些版本会提供更长的支持，像 Java 11 一样，至少提供 4 年的免费长期支持(LTS)计划。

通过 AdoptOpenJDK 可以安装最多版本的 JDK.
```
brew cask install AdoptOpenJDK/openjdk/adoptopenjdk8
brew cask install AdoptOpenJDK/openjdk/adoptopenjdk9
brew cask install AdoptOpenJDK/openjdk/adoptopenjdk10
brew cask install AdoptOpenJDK/openjdk/adoptopenjdk11
brew cask install AdoptOpenJDK/openjdk/adoptopenjdk12
brew cask install AdoptOpenJDK/openjdk/adoptopenjdk
```

## JDK12/JDK13/OracleJDK
如果你想在电脑上装最新版的 JDK, 那么 Oracle 或许是你最想要的选择, 而 Oracle 家的最新版 JDK 也有两款, 一个是 Oracle 提供的 OpenJDK, 一个是商业版本 Oracle JDK, 但请注意 Oracle JDK 并不比 OpenJDK “更好”, 大家需要理性看待.
```
# 运行以下命令会安装 Oracle 提供的 Oracle JDK12
brew cask install oracle-jdk

# 在2019年5月
## 该命令会安装由 Oracle 提供的 OpenJDK12
brew cask install java
## 而该命令则安装由 Oracle 提供的 OpenJDK11
brew cask install java11
```
## JDK7/Zulu
JDK7 甚至 AdoptOpenJDK 都不提供了, 这时候需要的是有商业背景的 Azul Zulu, zulu 是 OpenJDK 的免费版本, 在提供商业付费支持之外, Azul 也有为 zulu 提供免费的社区技术支持.

通过安装 zulu7 我们可以安装 OpenJDK7.
```
# Azul Zulu 也提供其他版本的 OpenJDK 像 zulu8 zulu11 和最新版的 zulu 均可使用
brew cask install homebrew/cask-versions/zulu7
brew cask install homebrew/cask-versions/zulu8
brew cask install homebrew/cask-versions/zulu11
brew cask install homebrew/cask-versions/zulu
```
## JDK6
估计现在连好多企业都不用了吧，所以放到左后。 JDK6 主要由 Apple 自身提供。
```
brew cask install homebrew/cask-versions/java6
```