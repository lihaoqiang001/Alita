# macOS Homebrew安装JDK的一些问题
***目录***  
[JDK8~JDK10/OpenJDK/AdoptOpenJDK](#JDK8至JDK10和OpenJDK和AdoptOpenJDK)  
[JDK12/JDK13/OracleJDK](#JDK12和JDK13和OracleJDK)  
[JDK7/Zulu](#JDK7和Zulu)  
[JDK6](#JDK6)  

---
#### [Homebrew](https://brew.sh/index_zh-cn)就不多做介绍了，开发人员肯定耳熟能详。这里推荐大家一篇：
> 1. [用 Homebrew 带飞你的 Mac](https://segmentfault.com/a/1190000014541169)
> 2. [我在 Mac 上都用什么](https://www.cnblogs.com/imzhizi/p/my-apps-on-mac.html)  

自从`Oracle`接手JDK之后，更新变快了，之前的“旧版本”也不容易下载了。最近一段时间`Oracle`一直不安生, 搞出来一堆幺蛾子, 所以安装方式也一直在变, 之前的方法已经不能用了, 网上找各种办法都不好使，下面针对各个版本给出了不同建议, 安装结束后, 可输入```java -version```确认是否安装成功。

## JDK8至JDK10和OpenJDK和AdoptOpenJDK
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

## JDK12和JDK13和OracleJDK
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
## JDK7和Zulu
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
---
***遇到问题耐心解决，如果还没解决，那肯定是时间没花够***  
- 9月21日心心念想、梦寐以求的MacBook Pro (13-inch, 2019, Four Thunderbolt 3 ports)入手的第一天晚上，我拆机用了多半个小时，就是边拆边拍照，拆个盒子都要洗个手😂那种。在这之前，我平时抽空就提前“上手macOS”
- 依稀还记得初一自己捣鼓的那台组装机，主板：华硕，CPU：英特尔奔腾E5400，硬盘512G HDD，金士顿2G，现在确实已经很卡了，尽管装了最新版的Windows v1903专业版。不过作为我的第一台电脑，好多东西都是在它上面学的，感谢下我老爸将它作为考了年级第一奖励台电脑送给我。
- 9月21日那天晚上，emmm，是晚上，大家应该和我有同感，一到晚上一些站点就特别慢，比如`GitHub`之类的，但强迫症的我肯定得在第一时间部署好我的开发环境吧，毕竟大二那会儿我快成专业的运维了～～同学电脑有毛病就找我，开发环境（Java/Android/Python/Node～）有问题还是找我。所以就先装Git、JDK、Maven吧。
- Git简单，现在macOS 虽然不自带Git，但是安装Homebrew之前安装的Command Line Tools里面包括了Git、gcc等工具，很方便，也比较快（**前提是[切换了Homebrew的源](https://mirrors.tuna.tsinghua.edu.cn/help/homebrew/)**）
- JDK确实费了老大劲才装好，还是第二天早晨6点10分起来干的，因为早晨访问GitHub这种站点确实比下午快很多。最后诞生了此文。
- Maven不说了，可以Homebrew安装，也可以在Maven官网下载包之后解压，然后使用，好多人可能会想着配Mavne的环境变量，其实我个人认为没必要。直接说下我是怎么使用的吧：IDEA现在是Java开发的主流IDE工具，里面的终端可以自己配置，结合zsh加上oh my zsh简直无可挑剔！我是使用了“两个Maven”，一个是公司用（公司有自己的Maven仓库），另一个是自己玩（配置的阿里云镜像），在同一个IDEA切换不同的`settings.xml`便可以实现多Maven切换，之间互不影响，主要是IDEA确实智能，智能在部分配置是每个项目单独的，多个项目可以完全配置不同的Maven，公司项目和自己项目随意切换，Maven也跟着换，很方便。至于不配置Maven环境mvn命令不能使用的问题我想说：IDEA里面依然可以执行你手敲的```mvn -U clean package -Dmaven.test.skip=true```，所以我不推荐配置Maven的环境变量。用多个Maven的原因我想大家也没明白，如果公司项目里修改了某个包的源码或者重写了某个方法，而你自己项目同样使用了该包的，那么这种情况下极易出错，使用Maven或多或少可能会遇到Maven存在一些Bug，这种迭代了N个版本依然存在的Bug，也许这就是包统一管理的缺陷，如果至今你还没碰过这种情况，说明你的项目比较稳定或者emmmm...你平时自己不捣鼓学习一些东西。