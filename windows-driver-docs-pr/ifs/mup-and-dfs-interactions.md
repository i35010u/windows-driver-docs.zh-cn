---
title: MUP 和 DFS 交互
description: MUP 和 DFS 交互
keywords:
- DFS WDK 网络重定向器
- 分布式文件系统 WDK 网络重定向器
- 内核网络重定向 WDK，MUP
- MUP WDK 网络重定向器
- 多 UNC 提供程序 WDK 网络重定向程序
- UNC WDK 网络重定向器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b5ccaa8d251fe60987fe8d922f64b083b4af0f75
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831447"
---
# <a name="mup-and-dfs-interactions"></a>MUP 和 DFS 交互


当应用程序使用通用命名约定 (UNC) 路径时，请求将发送到多个 UNC 提供程序 (MUP) ，以确定要使用的网络提供程序。 MUP 会将请求通道到 (UNC 提供程序) 的相应网络重定向程序，以便能够处理远程文件系统请求。 如果启用了分布式文件系统 (DFS) 客户端，则 MUP 首先将针对特定 " \\ \\ 服务器共享" 的请求传递 \\ 给 dfs 客户端，以确定请求是用于 dfs 共享而不是正常的远程文件共享。

默认行为是启用 DFS 客户端。 根据以下注册表项的值，禁用 DFS 客户端：

```cpp
HKLM\System\CurrentControlSet\Services\Mup
```

如果 DisableDfs 注册表项的 DWORD 值为1，则会禁用 DFS 客户端。

假设在基于名称的操作中指定的路径的前缀不在 MUP 维护的前缀缓存中，则启用 DFS 客户端 (时，) 隐式优先于所有重定向程序。 DFS 客户端尝试确定指定的 UNC 路径是否为 DFS 路径。 它通过向适当服务器的 IPC $ 共享发送引用请求来实现此功能。 如果将路径确定为 DFS 路径，则 DFS 客户端将处理该操作。 否则，DFS 客户端会将基于名称的请求传递给 MUP，以便使用相应的重定向程序来处理前缀解析。

如果将访问 IPC $ 共享的请求发送到 LAN Manager 服务器 (有时称为 SMB 服务器) 、srv.sys、禁用或未安装 (UNIX 系统（例如) ），则可能会出现延迟，因为有多次尝试连接到 IPC $ 共享。 此延迟通常为5-7 秒，但可以更长时间基于连接网络基础结构和其他条件的速度和延迟时间。

 

 




