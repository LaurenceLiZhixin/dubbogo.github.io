---
title: dubbo-go3.0快速开始
keywords: 快速开始,helloworld,
description: 快速上手dubbo-go3.0，编写一个简单的helloworld应用

---

# 安装 Dubbo-go 开发环境

## 1. 安装Go语言环境

建议使用最新版 go 1.17

go version >= go 1.15

[【Go 语言官网下载地址】](https://golang.google.cn/)

将 $GOPATH/bin 加入环境变量

## 2 安装序列化工具protoc

[【protoc 下载地址】](https://github.com/protocolbuffers/protobuf/releases)

## 3 安装 dubbogo-cli 以及相关插件

执行以下指令安装dubbogo-cli 至 $GOPATH/bin

```bash
$ export GOPROXY="https://goproxy.cn"
$ go install github.com/dubbogo/dubbogo-cli@latest
$ dubbogo-cli 
hello
```

安装依赖的工具插件

```bash
$ dubbogo-cli install all            
```

|      依赖      | Dubbo-go     | Triple | protoc-gen-go-triple |
| :------------: | ------------ | ------ | -------------------- |
| 适配版本号(>=) | v3.0.1       | v1.1.8 | v1.0.8               |
|                | v3.0.0       | v1.1.6 | v1.0.5               |
|                | v3.0.0-rc4-1 | v1.1.3 | v1.0.2               |
|                | v3.0.0-rc3   | v1.0.9 | v1.0.0               |

确保上述protoc 和安装的 protoc-gen-go-triple 位于$(GOPATH)/bin, 在系统环境变量内

```bash
$ protoc --version
libprotoc 3.14.0
$ protoc-gen-go --version
protoc-gen-go v1.26.0
$ protoc-gen-go-triple --version
protoc-gen-go-triple 1.0.8
```

## 