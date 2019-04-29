---
title: MUP 和 DFS 交互
description: MUP 和 DFS 交互
ms.assetid: 39c1f1e3-fb2d-46e7-b3dc-3d4bfab9608c
keywords:
- DFS WDK 网络重定向程序
- 分布式的文件系统 WDK 网络重定向程序
- 内核网络重定向程序 WDK MUP
- MUP WDK 网络重定向程序
- 多个 UNC 提供程序 WDK 网络重定向程序
- UNC WDK 网络重定向程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d94b1ee73289183e0b71dc00bc8bc697ddbbc432
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377951"
---
# <a name="mup-and-dfs-interactions"></a>MUP 和 DFS 交互


当应用程序使用通用命名约定 (UNC) 路径时，请求发送到多个 UNC provider (MUP) 来确定要使用的网络提供程序。 MUP 通道与相应的网络重定向 （UNC 访问接口），能够处理远程文件系统请求的请求。 如果启用了分布式文件系统 (DFS) 客户端，MUP 首先将传递特定的请求"\\\\server\\共享"到 DFS 客户端，以确定请求是否为 DFS 共享而不是正常的远程文件共享。

默认行为是，启用 DFS 客户端。 DFS 客户端将被禁用，具体取决于注册表项位于下方以下值：

```cpp
HKLM\System\CurrentControlSet\Services\Mup
```

当 DisableDfs 注册表项 DWORD 值 1 时，已禁用 DFS 客户端。

假设在基于名称的操作中指定的路径的前缀中维护 MUP，DFS 客户端 （如果启用） 的前缀缓存不是隐式将优先于所有重定向程序。 DFS 客户端尝试确定指定的 UNC 路径是否为 DFS 路径。 做到这一点通过将推荐请求发送到相应的服务器的 IPC$ 共享。 如果确定的路径为 DFS 路径，则 DFS 客户端处理操作。 否则，DFS 客户端将基于名称的请求传递给 MUP 的前缀解析要由适当的重定向程序。

若要访问的 IPC$ 共享的请求发送到系统时其中 LAN 管理器服务器 （有时称为 SMB 服务器），srv.sys，如果禁用或未安装 （例如，UNIX 系统），可能因为进行多次尝试连接到而引入的延迟IPC$ 共享。 这种延迟通常为 5 到 7 秒，但可以再基于的速度和延迟的连接的网络基础结构和其他条件。

 

 




