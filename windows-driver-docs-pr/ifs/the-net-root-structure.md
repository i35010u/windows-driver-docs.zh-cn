---
title: NET_ROOT 结构
description: NET_ROOT 结构
keywords:
- 网络根结构 WDK RDBSS
- 网络服务器共享连接数据 WDK RDBSS
- NET_ROOT 结构
- 服务器共享连接数据 WDK RDBSS
- 根结构 WDK RDBSS
- 数据结构 WDK 文件系统
- RDBSS WDK 文件系统、连接和文件结构
- 重定向的驱动器缓冲子系统 WDK 文件系统、连接和文件结构
- 连接结构 WDK RDBSS
- 文件结构 WDK RDBSS
- 结构 WDK RDBSS
- 连接信息 WDK RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce0565143f1a5506e67b77ca215ae7d6e74b95b6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822435"
---
# <a name="the-net_root-structure"></a>NET_ROOT 结构


## <span id="ddk_the_net_root_structure_if"></span><span id="DDK_THE_NET_ROOT_STRUCTURE_IF"></span>


NET_ROOT 的网络根结构包含 \\ 由网络小型重定向程序维护的每个特定网络服务器共享连接的信息。

NET_ROOT 是 RDBSS 和网络小型重定向程序驱动程序要处理的，而不是服务器。 相应地，RDBSS 通常会创建并打开 NET_ROOT 的结构，并调用负责打开服务器的网络微重定向器驱动程序。 网络微型重定向程序驱动程序应填充传入 NET_ROOT 结构中的相应字段。

NET_ROOT 结构的列表由每个 SRV_CALL 的 RDBSS 维护。 每个 NET_ROOT 结构都有几个与其他 RDBSS 结构共有的元素，以及对 NET_ROOT 结构唯一的元素。 管理 NET_ROOT 结构的 RDBSS 例程仅修改以下元素：

-   签名和引用计数

-   名称和关联的表信息

-   指向关联的 SRV_CALL 结构的返回指针

-   各种子结构的大小信息

-   关联的 FCB 结构的查找表

-   任何其他存储由网络小型重定向器 (或 NET_ROOT 数据结构的创建者请求) 

NET_ROOT 结构还包含 RX_CONTEXT 结构的列表，这些结构正在等待 NET_ROOT 转换完成，然后再恢复 IRP 处理。 当并发请求定向到服务器时，通常会发生这种情况。 在对其他请求进行排队时，将启动其中的一个请求。 保留给网络小型重定向程序使用的额外空间始于已知 NET_ROOT 数据结构的末尾，因此网络小型重定向程序只需使用包含文件中的上下文字段来引用此额外空间即可。

NET_ROOT 结构的终止由两部分组成：

1.  销毁与所有 V_NET_ROOTS 的关联

2.  释放内存

这两个操作之间可能存在延迟，NET_ROOT 结构中的字段会阻止复制第一步。

 

 




