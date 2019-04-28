---
title: SRV_CALL 结构
description: SRV_CALL 结构
ms.assetid: 9a3bb194-0289-47f4-a5c8-848d8d82cdd7
keywords:
- SRV_CALL 结构
- 服务器调用上下文结构 WDK RDBSS
- 网络服务器连接数据 WDK RDBSS
- 数据结构 WDK 文件系统
- RDBSS WDK 的文件系统、 连接和文件结构
- 重定向驱动器缓冲子系统 WDK 的文件系统、 连接和文件结构
- 连接结构 WDK RDBSS
- 文件结构 WDK RDBSS
- 结构 WDK RDBSS
- WDK RDBSS 的连接信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aeb31919d7303758c702e98993d0a233ba115631
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348369"
---
# <a name="the-srvcall-structure"></a>SRV\_调用结构


## <span id="ddk_the_srv_call_structure_if"></span><span id="DDK_THE_SRV_CALL_STRUCTURE_IF"></span>


服务器调用的上下文结构 SRV\_调用时，会维护有关维护网络微型重定向的每个特定的网络服务器连接信息。

全局列表的 SRV\_调用结构由 RDBSS 维护在全局数据中。 每个 SRV\_结构具有其他 RDBSS 结构，和元素，是唯一的 SRV 与常见的几个元素调用\_调用结构。 管理 SRV RDBSS 例程\_调用结构只能修改以下元素：

-   签名和引用计数

-   名称和关联的表信息

-   一组相关联的 NET\_根项

-   一组控制网络微型重定向是何种频率想要在不同情况下由 RDBSS 调用的计时参数 （例如空闲超时，）

-   关联的网络微型重定向程序驱动程序 ID

-   任何额外的存储是通过网络微型重定向的请求 (或创建者的 SRV\_调用数据结构)

SRV Unicode 名称\_调用结构执行结束时的结构本身中。 额外的空间保留用于已知 SRV 结束时开始使用网络微型重定向\_呼叫数据结构，使网络微型重定向可以只是指从包含文件中使用上下文字段此额外空间。

SRV 进行收尾工作\_调用结构由两部分组成：

1.  销毁与所有网络相关联的\_根

2.  释放内存

可能会有这两个操作和 SRV 中的字段之间延迟\_结构可防止第一步重复出现的调用。

 

 




