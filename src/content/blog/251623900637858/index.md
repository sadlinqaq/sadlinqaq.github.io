---
title: 'Spring Cloud'
description: '简单的笔记'
publishDate: '2026-05-10 16:05:25'
tags:
  - Spring Cloud
  - 微服务
  - 分布式
heroImage: { src: './thumbnail.png', alt: 'an image targeting my article', color: '#EDB6FA' }
---

## <span style="color:#BBF3F7">Spring Cloud</span>
### 微服务
是一种软件架构风格，核心是把大型单体应用拆成多个独立、松耦合、可独立部署的小型服务，每个服务专注单一业务能力。
### 分布式
把小型服务，跑在多台机器上，一起对外提供服务。
### 注册中心/配置中心 SpringCloud Alibaba <span style="color:#11EBFA">Nacos</span>
#### 启动nacos(2.4.3)
* 将nacos安装到非中文路径中
* 在目录**nacos/bin**中执行，命令行输入: **startup.cmd -m standalone** 启动单机模式
* 访问路径**localhost:8848/nacos**
#### 服务注册 <span style='color:red'>*</span>
* 导入nacos依赖
  ```xml
    <dependency>
        <groupId>com.alibaba.cloud</groupId>
        <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
    </dependency>
  ```
* 配置类
  ```properties
  spring.cloud.nacos.server=127.0.0.1:8848
  ```
在项目启动时自动注册。

#### 服务发现
* <span style="color:#F9B108">@EnableDiscoveryClient</span>
在启动类中添加,开启服务发现功能
* <span style="color:#B607BC">DiscoveryClient</span> 组件
  可以获取所有注册中心的所有ip与端口
* <span style="color:#B607BC">NacosServiceDiscovery</span> 组件
  可以获取nacos注册中心的所有ip与端口
* <span style="color:#B607BC">LoadBalancerClient</span> 组件
  可以负载均衡的选择服务地址
需要引入spring的依赖
  ```xml
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-loadbalancer</artifactId>
    </dependency>
  ```
* <span style="color:#F9B108">@LoadBalanced</span>
  在配置类中配置RestTemplate组件，在方法名上添加<span style="color:#F9B108">@LoadBalanced</span>注解，可以实现负载均衡的发起请求

#### 配置中心 <span style='color:red'>*</span>
Nacos 配置中心是集中管理、动态推送、实时生效的配置管理平台，解决微服务配置分散、修改需重启、多环境不一致等问题Nacos。
**依赖引入**
```xml
<dependency>
    <groupId>com.alibaba.cloud</groupId>
    <artifactId>spring-cloud-starter-alibaba-nacos-config</artifactId>
</dependency>
```
**配置类添加**
```properties
spring.config.import=nacos:XXX.properties
```

**自动刷新**
实时生效配置类
<span style="color:#F9B108">@RefreshScope</span>+<span style="color:#F9B108">@Value</span>
<span style="color:#F9B108">@ConfigurationProperties</span>

**禁用配置**
配置类
```properties
spring.cloud.nacos.config.import-check.enabled=false
```

### 远程调用 SpringCloud <span style="color:#07F988">OpenFeign</span>
#### 自动从注册中心负载均衡的远程调用
* 引入依赖
```xml
<dependency>
    <groupId>com.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-openfeign</artifactId>
</dependency>
```
* <span style="color:#F9B108">@EnableFeignClients</span>
在启动类添加<span style="color:#F9B108">@EnableFeignClients</span>注解开启Feign远程调用功能
* <span style="color:#F9B108">@FeignClient</span>
创建接口XXXFeignClient,并在接口上添加<span style="color:#F9B108">@FeignClient</span>注解（开启feign客户端），会自动注入容器组件
* 请求方式
<span style="color:#F9B108">@GetMapping</span> <span style="color:#F9B108">@PostMapping</span>...
* 携带数据
<span style="color:#F9B108">@RequestHeader</span> <span style="color:#F9B108">@RequestParm</span>...

#### 超时控制
* **connectTimeout**
在feign客户端发起请求时，会进行建立连接，超时则中断连接
* **readTimeout**
feign客户端发起请求后，客户端的业务处理时间，超时返回失败
```yml
spring.cloud.openfeign.client:
    xxx(feign客户端名称):
        connect-timeout: 3000
        read-timeout: 5000
```

#### 重试机制
feign客户端默认关闭
* 配置类中添加默认重试机制
默认初始间隔100ms，每次重试间隔$\times$1.5,最大间隔1s
```yml
spring.cloud.openfeign.client:
    xxx(feign客户端名称):
        retryer: feign.retryer.Defatult
```
* 也可以在配置类重写配置规则

#### 拦截器
* 请求拦截器
可以把数据放到请求头或其他地方中，使得整个链路可以共享数据
* <span style="color:#B607BC">RequestInterceptor</span> 接口
定义拦截器并实现**openFeign**的<span style="color:#B607BC">RequestInterceptor</span> 接口，将其放入容器，在每次使用远程调用都会自动使用这个拦截器

#### 兜底返回
不希望返回错误信息，需要默认数据
* 创建实现类实现**XXXFeignClient**接口
* 在<span style="color:#F9B108">@FeignClient</span>注解中标注**fallback = 类**
* 熔断配置
```yml
feign.sentinel.enable: true
```
### 服务熔断 SpringCloud Alibaba <span style="color:#B607BC">Sentinel</span>
微服务流量治理组件，核心做限流、熔断、降级、系统保护，是 Spring Cloud Alibaba 生态标配，用来防止服务雪崩、保障高可用。

**控制台启动 (sentinel-dashboard-1.8.8.jar)**
* 在本路径中启动命令行，输入**java -jar sentinel-dashboard-1.8.8.jar**
* 访问**localhost:8080**,默认账号密码: sentinel
* 
**依赖引入**
```xml
<dependency>
    <groupId>com.alibaba.cloud</groupId>
    <artifactId>spring-cloud-starter-alibaba-sentinel</artifactId>
</dependency>
```

**配置配置类**
```yml
spring.cloud.sentinel:
    transport: 
        dashboard: localhost:8080 #设置地址
    eager: true #关闭懒加载，即项目一启动就加载

```

#### 定义资源 
* 所有web接口均为资源(Web Servlet、Spring Cloud..)
* 编程式: SphU API
* 声名式: <span style="color:#F9B108">@SentinelResource</span>
<span style="color:#F9B108">@SentinelResource</span>注解定义资源，包括调用该资源的web接口，或者被其调用的web接口也同一视为资源

#### 异常处理
* Web接口
默认使用<span style="color:#B607BC">DefaultBlockExceptionHandler</span>组件,需自定义**XXXBlockExceptionHandler**组件实现sentinel的<span style="color:#B607BC">BlockExceptionHandler</span>异常处理接口
* <span style="color:#F9B108">@SentinelResource</span> 标注的资源
标注的资源会被<span style="color:#B607BC">SentinelResourceAspect</span>切面类切入，根据注解中是否有**blockHandler**标注或**fallback**标注去处理异常。不处理则抛给全局异常处理器
* <span style="color:#07F988">OpenFeign</span>调用
> 创建实现类实现**XXXFeignClient**接口
> 在<span style="color:#F9B108">@FeignClient</span>注解中标注**fallback = 类**
> 如果不处理，则抛给全局异常处理器
* SphU 硬编码

#### 规则-流量控制（FlowRule）
限制多余请求，从而保护系统资源不被耗尽
**流控模式**
* 直接
* 关联
* 链路

**流控效果**
* **快速失败**
直接拒绝
* **Warm Up**
预热/冷启动
* **排队等待**

#### 规则-熔断降级（DegradeRule）
切断不稳定调用（请求超时，失败，慢调用...），快速返回不积压，避免雪崩效应
> $慢调用/异常比例/异常数-->熔断（熔断时长）-->探测是否可以访问--> 熔断/放行$

#### 规则-热点参数
访问频率极高、瞬间流量集中的请求参数（如商品 ID、用户 ID、直播间 ID）。在微服务 / 高并发场景中，它是精准限流、防击穿、防雪崩的核心手段。

### 网关 SpringCloud <span style="color:#F99007">Gateway</span>
是所有客户端请求的统一入口，负责路由转发、安全、流量治理与监控，是微服务的 “流量总闸”。
**依赖引入**
```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-gateway</artifactId>
</dependency>
```
同时需要把网关服务注册到nacos注册中心中,并引入**Spring**的负载均衡依赖

**规则配置-配置类**
```yml
spring.cloud:gateway:
    routes: 
        - id: XXX #路由名字
          uri: lb://XXX #转给微服务的名字，lb(loadBalance)
          predicates:
            - Path=/api/order/** #转发路径为/api/order的所有请求
          filters:
            - RewritePath=/api/order/?(?<segment.*>),/$\{segment} #重写转发的路径
            - AddRequestHeader=X-Request-red, blue #添加自定义请求头
    globalcors: #跨域配置
        cors-configurations:
            '[/**]': #允许所有请求跨域
                allowed-origin-patterns: '*' #允许所有跨域
                allowed-headers: '*' #所有请求头
                allowed-methods: '*' #所有请求方法
```

### 分布式事务 SpringCloud Alibaba <span style="color:#01EB95">Seata</span>
让微服务跨库、跨服务操作像本地事务一样，要么全部成功，要么全部回滚，保证数据一致

#### 启动seata-server
* 安装apache-seata(2.1.0)
* 来的bin目录，打开命令行输入：**seata-server.bat**
* 访问**127.0.0.1:7091**,账号密码默认seata

#### 微服务开启seata客户端
* 依赖引入
```xml
<dependency>
    <groupId>com.alibaba.cloud</groupId>
    <artifactId>spring-cloud-starter-alibaba-seata</artifactId>
</dependency>
```
* 创建file.conf文件
```conf
service {
  #transaction service group mapping
  vgroupMapping.default_tx_group = "default"
  #only support when registry.type=file, please don't set multiple addresses
  default.grouplist = "127.0.0.1:8091"
  #degrade, current not support
  enableDegrade = false
  #disable seata
  disableGlobalTransaction = false
}
```

* 添加<span style="color:#F9B108">@GlobalTransaction</span> 注解
在最大的方法入口添加<span style="color:#F9B108">@GlobalTransaction</span> 全局事务注解