---
title: 设置 SAN 连接
description: 设置 SAN 连接
keywords:
- Windows 套接字直接 WDK，连接设置
- 连接 WDK San
- SAN 连接设置 WDK
- SAN 连接设置 WDK，关于 SAN 连接设置
- SAN 服务提供商 WDK，连接设置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b775ffa2b966d4971e184693859be43508b6561b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819999"
---
# <a name="setting-up-a-san-connection"></a>设置 SAN 连接





在建立连接的过程中，Windows 套接字交换机决定哪个服务提供商将为 TCP 套接字提供服务。 此提供程序将处理套接字上的大多数后续操作。 无论交换机是否选择 SAN 服务提供程序，TCP/IP 提供程序都将独占处理几种类型的设置操作。

本部分介绍了 SAN 服务提供商执行的连接设置操作以及 TCP/IP 提供程序处理的连接设置操作。 以下主题提供了此信息：

[创建和绑定 SAN 套接字](creating-and-binding-san-sockets.md)

[发起连接](initiating-a-connection.md)

[侦听 SAN 上的连接](listening-for-connections-on-a-san.md)

[接受连接请求](accepting-connection-requests.md)

[为 SAN 上的操作注册内存](registering-memory-for-operations-on-a-san.md)

[缓存已注册的内存](caching-registered-memory.md)

 

 





