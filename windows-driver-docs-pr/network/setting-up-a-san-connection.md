---
title: 设置 SAN 连接
description: 设置 SAN 连接
ms.assetid: f5d5e759-d77c-4db8-9b63-fb4c79344dff
keywords:
- Windows 套接字直接 WDK，连接设置
- 连接 WDK San
- SAN 连接安装 WDK
- 有关设置 SAN 连接的 SAN 连接安装 WDK，
- SAN 服务提供商 WDK，连接设置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0fc5330f637ae8d672220e1dcc59fc55dba08c30
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520818"
---
# <a name="setting-up-a-san-connection"></a>设置 SAN 连接





连接在安装期间，Windows 套接字交换机确定哪个服务提供商将 TCP 套接字的服务。 此提供程序将处理大多数套接字上的后续操作。 无论是否开关选择 SAN 服务提供商，TCP/IP 提供程序以独占方式处理几个类型的安装程序操作。

本部分介绍 SAN 服务提供程序执行连接安装程序操作和 TCP/IP 访问接口处理连接安装程序操作。 以下主题中提供此信息：

[创建并绑定 SAN 套接字](creating-and-binding-san-sockets.md)

[启动的连接](initiating-a-connection.md)

[侦听在 SAN 上的连接](listening-for-connections-on-a-san.md)

[接受连接请求](accepting-connection-requests.md)

[注册在 SAN 上的操作内存](registering-memory-for-operations-on-a-san.md)

[缓存的已注册的内存](caching-registered-memory.md)

 

 





