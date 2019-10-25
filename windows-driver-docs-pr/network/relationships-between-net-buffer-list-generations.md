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
ms.openlocfilehash: 466b01723c7007bfc85f504c7eed65fa9f8bcd02
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842063"
---
# <a name="relationships-between-net_buffer_list-generations"></a>NET\_BUFFER\_列表生成之间的关系





驱动程序编写者应该理解并维护父（原始）[**网络\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构和派生自重新组合操作的子（派生）结构之间的关系。

克隆/分段/重组函数的调用方维护父/子关系，包括子网\_缓冲区中的父指针\_列表结构和子计数。 子计数确保调用方在释放所有子级后释放父级。 以下规则适用：

-   在驱动程序从[**NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)创建子结构\_列表结构时，它应保留父结构的所有权，并应将子结构传递到其他驱动程序。 驱动程序绝不应将 parent NET\_缓冲区\_列表结构传递到另一个驱动程序。

-   驱动程序只应更新 parent\_缓冲区\_列表结构中的子计数。 因为父结构决不会传递到另一个驱动程序，所以子计数的值可能不会被覆盖。 驱动程序应将子结构中的父指针设置为指向父结构。

-   当驱动程序收到来自另一驱动程序的 NET\_缓冲区\_列表时，驱动程序不得覆盖父指针。 如果收到的 NET\_缓冲区\_列表结构是子结构，则应设置其父指针。 驱动程序可以使用从另一个驱动程序接收的 NET\_缓冲区作为父结构\_列表。

-   NDIS 不强制执行上述规则。 NET\_缓冲区的当前所有者\_列表结构必须管理子计数和父指针。 例如，如果当前所有者同时克隆并分段网络\_缓冲区\_列表结构，则它必须管理父指针和子计数器。

-   NDIS 在分配 NET\_缓冲区\_列表结构时，会将子计数设置为零，并将父指针设置为**NULL** 。 每次驱动程序将 NET\_缓冲区\_列表结构传递到另一个驱动程序时，NDIS 不会更改这些字段。

## <a name="related-topics"></a>相关主题


[派生的 NET\_缓冲区\_列表结构](derived-net-buffer-list-structures.md)

 

 






