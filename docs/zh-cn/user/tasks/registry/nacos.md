---
title: 使用 Nacos 作为注册中心
keywords: 使用 Nacos 作为注册中心
description: 使用 Nacos 作为注册中心
---

# 使用 Nacos 作为注册中心



## 3. 如何配置注册中心

### 使用配置 API

- 客户端使用配置 API 设置注册中心

可通过调用config.NewRegistryConfigWithProtocolDefaultPort方法，快速设置用于调试的注册中心，支持zookeeper(127.0.0.1:2181) 和nacos(127.0.0.1:8848)

```go
rc := config.NewRootConfigBuilder().
    SetConsumer(config.NewConsumerConfigBuilder().
        SetRegistryIDs("zookeeperID"). // use defined registryID
        Build()).
    AddRegistry("zookeeperID", config.NewRegistryConfigWithProtocolDefaultPort("zookeeper")).
    Build()
```

全部接口：可通过调用RegistryConfigBuilder提供的丰富接口进行配置。

```go
rc := config.NewRootConfigBuilder().
    SetConsumer(config.NewConsumerConfigBuilder().
        SetRegistryIDs("nacosRegistryID"). // use defined registryID
        AddReference("GreeterClientImpl",/*...*/).
        Build()
    AddRegistry("nacosRegistryID", config.NewRegistryConfigBuilder().
        SetProtocol("nacos").
        SetAddress("127.0.0.1:8848").
        SetGroup("dubbo-go").
        SetNamespace("dubbo").
        SetUsername("admin").
        SetPassword("admin").
        SetTimeout("3s").
        Build()).
    Build()
```

- 服务端使用配置 API 设置配置中心

简易接口 config.NewRegistryConfigWithProtocolDefaultPort

```go
rc := config.NewRootConfigBuilder().
    SetProvider(config.NewProviderConfigBuilder().
        AddService("GreeterProvider", /*...*/).
        SetRegistryIDs("registryKey").  // use defined registryID
        Build()).
    AddRegistry("registryKey", config.NewRegistryConfigWithProtocolDefaultPort("zookeeper")).
    Build()
```

全部接口：可通过调用RegistryConfigBuilder提供的丰富接口进行配置。

```go
rc := config.NewRootConfigBuilder().
    SetProvider(config.NewProviderConfigBuilder().
        AddService("GreeterProvider",/*...*/)
        SetRegistryIDs("registryKey"). // use defined registryID
        Build()).
    AddRegistry("registryKey", config.NewRegistryConfigBuilder().
        SetProtocol("nacos").
        SetAddress("127.0.0.1:8848").
        SetGroup("dubbo-go").
        SetNamespace("dubbo").
        SetUsername("admin").
        SetPassword("admin").
        SetTimeout("3s").
        Build()).
    Build()
```

### 使用配置文件 

- 客户端/服务端

```yaml
dubbo:
  registries:
    demoZK: # define registry-id 'demoZK'
      protocol: zookeeper # set registry protocol
      timeout: 3s
      address: 127.0.0.1:2181
  protocols:
    triple:
      name: tri
      port: 20000
  provider:
    registry-ids:
      - demoZK # use registry-id 'demoZK'
    services:
      GreeterProvider:
        protocol-ids: triple
        interface: com.apache.dubbo.sample.basic.IGreeter 
  consumer:
    registry-ids:
      - demoZK # use registry-id 'demoZK'
    references:
      GreeterClientImpl:
        protocol: tri
        interface: com.apache.dubbo.sample.basic.IGreeter 
```





下一章：[【Dubbo 协议快速开始】](./quickstart_dubbo.html)