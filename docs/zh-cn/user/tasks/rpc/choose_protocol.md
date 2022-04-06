---
title: 选择使用的网络协议
keywords: 选择使用的网络协议
description: 选择使用的网络协议

---

# 选择使用的网络协议

## 1. 如何配置网络协议

在快速开始章节可以看到，在配置的过程中将 Protocol 设置为 tri，表明使用 Triple 协议进行服务暴露和服务调用。快速开始章节使用的配置 API 进行配置的写入，这样的好处是无需使用配置文件。我们摘取出和网络协议相关的内容进行说明。

### 使用配置 API

- 客户端使用配置 API 设置网络协议

```go
rc := config.NewRootConfigBuilder().
    SetConsumer(config.NewConsumerConfigBuilder().
        AddReference("GreeterClientImpl", config.NewReferenceConfigBuilder().
            SetInterface("org.apache.dubbo.UserProvider").
            SetProtocol("tri"). // set reference protcol to triple
            Build()).
        Build()).
    Build()
```

- 服务端使用配置 API 设置网络协议

```go
rc := config.NewRootConfigBuilder().
    SetProvider(config.NewProviderConfigBuilder().
        AddService("GreeterProvider", config.NewServiceConfigBuilder().
            SetInterface("org.apache.dubbo.UserProvider").
            SetProtocolIDs("tripleProtocolKey"). // use protocolID 'tripleProtocolKey'
            Build()).
        Build()).
    AddProtocol("tripleProtocolKey", config.NewProtocolConfigBuilder(). // define protocol config with protocolID 'tripleProtocolKey'
        SetName("tri"). // set service protocol to triple
        Build()).
    Build()
```

### 使用配置文件 

参考 samples/helloworld

- 客户端使用配置文件设置网络协议

```yaml
dubbo:
  consumer:
    references:
      GreeterClientImpl:
        protocol: tri # set protcol to tri
        interface: com.apache.dubbo.sample.basic.IGreeter 
```

- 服务端使用配置文件设置网络协议

```yaml
dubbo:
  protocols:
    triple: # define protcol-id 'triple'
      name: tri # set protcol to tri
      port: 20000 # set port to be listened
  provider:
    services:
      GreeterProvider:
        protocol-ids: triple # use protocol-ids named 'triple'
        interface: com.apache.dubbo.sample.basic.IGreeter
```

