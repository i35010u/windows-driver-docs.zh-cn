---
title: NET_ROOT 结构
description: NET_ROOT 结构
ms.assetid: f7846343-9af6-4b7f-9c8d-190abb524946
keywords:
- net 根结构 WDK RDBSS
- 网络服务器共享连接数据 WDK RDBSS
- NET_ROOT 结构
- 服务器共享连接数据 WDK RDBSS
- 根结构 WDK RDBSS
- 数据结构 WDK 文件系统
- RDBSS WDK 的文件系统、 连接和文件结构
- 重定向驱动器缓冲子系统 WDK 的文件系统、 连接和文件结构
- 连接结构 WDK RDBSS
- 文件结构 WDK RDBSS
- 结构 WDK RDBSS
- WDK RDBSS 的连接信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 982e668d07bc6965847a001cce73b72857c4648b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566935"
---
# <a name="the-netroot-structure"></a>NET_ROOT 结构


## <span id="ddk_the_net_root_structure_if"></span><span id="DDK_THE_NET_ROOT_STRUCTURE_IF"></span>


Net 根结构，NET_ROOT，包含每个特定的网络服务器信息\\共享连接维护的网络微型重定向。

NET_ROOT 为哪些 RDBSS 和网络微型重定向程序驱动程序想要处理的不能是服务器。 相应地，RDBSS 通常情况下创建和打开 NET_ROOT 结构并调用网络微型重定向程序驱动程序负责打开服务器。 网络微型重定向程序驱动程序需要填充相应字段中传递 NET_ROOT 结构中。

对于每个 SRV_CALL 情况下，由 RDBSS 维护 NET_ROOT 结构列表。 每个 NET_ROOT 结构具有几个常见的其他 RDBSS 结构，以及是唯一的 NET_ROOT 结构的元素的元素。 管理 NET_ROOT 结构 RDBSS 例程只能修改以下元素：

-   签名和引用计数

-   名称和关联的表信息

-   指向相关联的 SRV_CALL 结构的后

-   各种子结构的大小信息

-   查找表的关联 FCB 结构

-   任何额外的存储是由网络微型重定向 （或 NET_ROOT 数据结构的创建者） 请求

NET_ROOT 结构还包含一系列等待 NET_ROOT 转换完成后才继续 IRP 处理 RX_CONTEXT 结构。 这通常发生在并发请求定向到服务器。 这些请求之一启动而对其他请求进行排队。 保留以供网络微型重定向的额外空间开始已知 NET_ROOT 数据结构的末尾，以便网络微型重定向可以只是指从包含文件中使用上下文字段此额外空间。

NET_ROOT 结构进行收尾工作由两部分组成：

1.  销毁与所有 V_NET_ROOTS 的关联

2.  释放内存

这两个操作之间可能存在延迟和 NET_ROOT 结构中的字段可防止第一步重复出现。

 

 




