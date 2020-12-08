---
title: SRV_CALL 结构
description: SRV_CALL 结构
keywords:
- SRV_CALL 结构
- 服务器调用上下文结构 WDK RDBSS
- 网络服务器连接数据 WDK RDBSS
- 数据结构 WDK 文件系统
- RDBSS WDK 文件系统、连接和文件结构
- 重定向的驱动器缓冲子系统 WDK 文件系统、连接和文件结构
- 连接结构 WDK RDBSS
- 文件结构 WDK RDBSS
- 结构 WDK RDBSS
- 连接信息 WDK RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b9a12a3ccc716bfcf9d1fbe1939f60c9f6815ce
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818431"
---
# <a name="the-srv_call-structure"></a>SRV \_ 调用结构


## <span id="ddk_the_srv_call_structure_if"></span><span id="DDK_THE_SRV_CALL_STRUCTURE_IF"></span>


服务器调用上下文结构 SRV 调用将 \_ 维护有关网络小型重定向程序所维护的每个特定网络服务器连接的信息。

\_RDBSS 在全局数据中维护 SRV 调用结构的全局列表。 每个 SRV \_ 调用结构都有几个与其他 RDBSS 结构共有的元素，以及对 SRV 调用结构唯一的元素 \_ 。 管理 SRV 调用结构的 RDBSS 例程 \_ 仅修改以下元素：

-   签名和引用计数

-   名称和关联的表信息

-   关联的网络 \_ 根项的列表

-   一组计时参数，用于控制在不同情况下 RDBSS 调用网络小型重定向程序的频率 (空闲超时，例如) 

-   关联的网络微型重定向程序驱动程序 ID

-   任何其他存储由网络小型重定向程序请求 (或 SRV \_ 调用数据结构的创建者) 

SRV 调用结构的 Unicode 名称 \_ 是在结构本身的末尾处携带的。 保留以供网络小型重定向器使用的额外空间从已知的 SRV \_ 调用数据结构结束，因此，网络小型重定向程序只需使用包含文件中的上下文字段来引用此额外空间即可。

SRV 调用结构的终止 \_ 由两部分组成：

1.  正在销毁与所有网络根的关联 \_

2.  释放内存

这两个操作之间可能存在延迟，并且 SRV 调用结构中的字段会 \_ 阻止重复第一步。

 

 




