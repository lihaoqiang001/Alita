> ### Spring Boot版本升级：1.5.x -> 2.0.x

---
### 一、升级路线
```
1.5.6.RELEASE -> 2.0.x.RELEASE -> 2.1.x.RELEASE
```

### 二、理由

**Spring 官方推荐的升级2.0方式，援引[官方](https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-2.0-Migration-Guide)一段话：**  
We also recommend to upgrade in phases and not in one jump to the latest GA: first upgrade to 2.0, then 2.1, etc.

之所以最终要升级至2.1.x版本，是因为2.0.0版本存在诸多的问题，并在后续 >2.0.0 版本中得到了修复。

### 三、升级方法
##### 1.根据项目实际情况升级Spring Boot版本  
##### 2.加入依赖：
```
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-properties-migrator</artifactId>
	<scope>runtime</scope>
</dependency>
```
在项目启动时会检测之前的配置并打印到控制台，方便修改  
##### 3.升级与Spring Boot2.0.x匹配的中间件：MySQL、Redis、zk、Kafka等的版本

### 四、升级步骤（以下“升级”代表从1.5.6.RELEASE 升级至 2.0.x.RELEASE）
##### 1.升级Eureka集群  
##### 2.升级Config  
##### 3.升级其他项目  

### 五、已知升级后需要改动的地方
##### application.yml中：
```
1.mysql连接中 url 改为 jdbc-url

2.redis：
redis:
    pool:
      max-active: 1000
      max-wait: 50
      max-idle: 50
      min-idle: 0
改为：
redis:
    jedis:
      pool:
        max-active: 1000
        max-wait: 50
        max-idle: 50
        min-idle: 0

3.在1.5.x版本中通过management.security.enabled=false来暴露所有端点，升级后改为：
management:
  endpoints:
    web:
      exposure:
        include: "*"
```
##### pom.xml中：
```
1.除Spring外，其他中间件自行援引至相对应的Spring版本的包，比如Druid连接池比较挑Spring Boot版本

2.由于升级后Redis驱动程序由 Jedis 变为 Lettuce，经过验证，目前Redis更适合用Jedis，所以引用Redis时：
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
    <exclusions>
        <exclusion>
            <groupId>io.lettuce</groupId>
            <artifactId>lettuce-core</artifactId>
        </exclusion>
    </exclusions>
</dependency>
<dependency>
    <groupId>redis.clients</groupId>
    <artifactId>jedis</artifactId>
    <version>2.9.0</version>
</dependency>

3.Spring Cloud中部分引用需要变更，之前的已经不推荐使用，即将被弃用。以下列举了项目用几乎用到的所有的Spring Cloud相关组件：

spring-cloud-starter-eureka更新为：
<dependency>
  <groupId>org.springframework.cloud</groupId>
  <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
</dependency>

spring-cloud-starter-feign更新为：
<dependency>
  <groupId>org.springframework.cloud</groupId>
  <artifactId>spring-cloud-starter-openfeign</artifactId>
</dependency>

spring-cloud-starter-eureka更新为：
<dependency>
  <groupId>org.springframework.cloud</groupId>
  <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
</dependency>

spring-cloud-starter-hystrix更新为：
<dependency>
  <groupId>org.springframework.cloud</groupId>
  <artifactId>spring-cloud-starter-netflix-hystrix</artifactId>
</dependency>
```
### 其他说明/理由
```
1.框架大版本升级痛并快乐着。由于碰到了Spring Boot1.5.x的Bug导致在上线出现的严重问题加之Spring官方强烈推荐广大开发者尽快从Spring1.x版本迁移至2.x版本。所以考虑Spring Boot框架升级。  
2.由于Spring 2.0.x版本相对于Spring 1.5.x版本修复了许多问题、修改了许多源码，导致在配置、注解引用、某些配置类方法的删除等方面有许多改动。  
3.所以在升级Spring Boot版本时不可避免的需要修改上面所列（但不局限）的内容。  
4.升级后能带来什么，抱歉，没法解析。但就目前是用来看，无论是在性能、还是稳定性上都有大幅提升。  
5.就跟目前之所以升级JDK11动力不足的原因就是广大开发者没有认识到技术升级所带来的红利，这个因素主要在各种成本上。  
6.建议逐步升级Spring Boot至2.x版本。  
7.关于Spring Boot 与 Spring Cloud版本对应关系不用担心，已经梳理好，上文所说的Spring Boot升级囊括了Spring Cloud的升级。
```