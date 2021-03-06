---
title: NET_BUFFER_LIST 代系之间的关系
description: NET_BUFFER_LIST 代系之间的关系
keywords:
- NET_BUFFER_LIST
- 父/子 NET_BUFFER_LIST 关系 WDK 网络
- 子/父 NET_BUFFER_LIST 关系 WDK 网络
- 关系 WDK NET_BUFFER_LIST
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5442a0420a82fb50c4f4cf3dbb22f7d95e0e11ad
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102247979"
---
# <a name="relationships-between-net_buffer_list-generations"></a>网络 \_ 缓冲区 \_ 列表生成之间的关系





驱动程序编写者应该理解并维护父 (初始) [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list) 结构和子 (派生自克隆、片段和重新组合操作生成的) 结构之间的关系。

克隆/分段/重组函数的调用方维护父/子关系，包括子网络缓冲区列表结构中的父指针 \_ \_ 和子计数。 子计数确保调用方在释放所有子级后释放父级。 下列规则适用：

-   在驱动程序从 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list) 结构创建子结构后，它应保留父结构的所有权，并应将子结构传递给其他驱动程序。 驱动程序绝不应将父网络 \_ 缓冲区 \_ 列表结构传递到另一个驱动程序。

-   驱动程序只应更新父网络 \_ 缓冲区列表结构中的子计数 \_ 。 因为父结构决不会传递到另一个驱动程序，所以子计数的值可能不会被覆盖。 驱动程序应将子结构中的父指针设置为指向父结构。

-   当驱动程序收到 \_ \_ 来自另一驱动程序的网络缓冲区列表时，驱动程序不得覆盖父指针。 如果收到的网络 \_ 缓冲区 \_ 列表结构是子结构，则应设置其父指针。 驱动程序可以使用 \_ \_ 从另一个驱动程序接收的网络缓冲区列表作为父结构。

-   NDIS 不强制执行上述规则。 网络 \_ 缓冲区列表结构的当前所有者 \_ 必须管理子计数和父指针。 例如，如果当前所有者将克隆网络 \_ 缓冲区列表结构并对其进行分段 \_ ，则它必须管理父指针和子计数器。

-   NDIS 在分配网络 \_ 缓冲区列表结构时，将子计数设置为零，并将父指针设置为 NULL \_ 。 每次驱动程序将网络 \_ 缓冲区 \_ 列表结构传递到另一个驱动程序时，NDIS 不会更改这些字段。

## <a name="related-topics"></a>相关主题


[派生的网络 \_ 缓冲区 \_ 列表结构](derived-net-buffer-list-structures.md)

 

