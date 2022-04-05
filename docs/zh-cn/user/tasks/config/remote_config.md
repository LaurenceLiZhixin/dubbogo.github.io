---
title: 远程加载配置启动
keywords: 远程加载配置启动
description: 远程加载配置启动
---

# 远程加载配置启动

### 从配置中心读取

Dubbogo 服务框架支持将配置文件 'dubbogo.yaml' 的内容预先放入配置中心，再通过配置注册中心的地址。在本地 dubbogo.yaml 配置文件内只需写入配置中心的信息即可，目前支持作为配置中心的中间件有：apollo、nacos、zookeeper

可参考 [配置中心Samples](https://github.com/apache/dubbo-go-samples/tree/master/configcenter)，凡是正确配置了config-center 配置的服务，都会优先从配置中心加载整个配置文件。

```yaml
# 框架从apollo配置中最更新对应位置加载配置文件，并根据该配置文件启动
dubbo:
  config-center:
    protocol: apollo
    address: localhost:8080
    app-id: demo_server
    cluster: default
    namespace: demo-provider-config
```

下一章：[【Dubbo 协议快速开始】](./quickstart_dubbo.html)

### 