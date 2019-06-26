---
title: NET_BUFFER_LIST 代系之间的关系
description: NET_BUFFER_LIST 代系之间的关系
ms.assetid: 37b3b08d-4656-47bc-b656-a03f208e4311
keywords:
- NET_BUFFER_LIST
- 父/子 NET_BUFFER_LIST 关系 WDK 网络
- 子/父 NET_BUFFER_LIST 关系 WDK 网络
- 关系 WDK NET_BUFFER_LIST
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b869a9b07250f99d5cfff8d83c41527e85222876
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359136"
---
# <a name="relationships-between-netbufferlist-generations"></a>NET 之间的关系\_缓冲区\_列表代





驱动程序编写人员应理解和维护父 （原始） 之间的关系[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构和 （派生） 的子结构由于克隆、 片段和重装配操作。

重装配克隆/片段函数的调用方维护的父/子关系，包括子网中的父指针\_缓冲区\_列表结构和子级计数。 子级计数可确保调用方释放父级，被释放所有子级之后。 以下规则适用：

-   驱动程序创建子结构从后[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构，它应保留父结构的所有权以及应传递子为其他驱动程序的结构。 该驱动程序应永远不会通过父 NET\_缓冲区\_列表结构到另一个驱动程序。

-   驱动程序应只更新父 NET 中的子计数\_缓冲区\_列表结构。 父结构永远不会传递给另一个驱动程序，因为不存在风险的子级计数值可能被覆盖。 驱动程序应将父指针设置为指向父结构的子结构中。

-   当驱动程序收到 NET\_缓冲区\_从另一个驱动程序，该驱动程序的列表必须不会覆盖父指针。 如果接收到的 NET\_缓冲区\_列表结构是子级，应已设置其父指针。 该驱动程序可以使用 NET\_缓冲区\_列表来自另一个驱动程序，因为父结构。

-   NDIS 不强制前面的规则。 当前所有者的 NET\_缓冲区\_列表结构必须管理的子计数和父指针。 例如，如果当前所有者将克隆并片段 NET\_缓冲区\_列表结构，它必须管理父指针和子计数器。

-   NDIS 设置子计数为零和父指向**NULL**时，它会分配 NET\_缓冲区\_列表结构。 NDIS 不会更改这些字段每次将驱动程序将传递 NET\_缓冲区\_列表结构到另一个驱动程序。

## <a name="related-topics"></a>相关主题


[派生 NET\_缓冲区\_列表结构](derived-net-buffer-list-structures.md)

 

 






