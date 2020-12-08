---
title: 指示 RSS 接收数据
description: 指示 RSS 接收数据
keywords:
- 接收方缩放 WDK 网络，指示接收数据
- RSS WDK 网络，指示接收数据
- 指示接收数据 WDK RSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e27452cb70c39ff4c95ab0b700228b1e56b650c6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803527"
---
# <a name="indicating-rss-receive-data"></a>指示 RSS 接收数据





微型端口驱动程序通过从其 [*MiniportInterruptDPC*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_interrupt_dpc)函数调用 [**NdisMIndicateReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)函数来指示收到的数据。

NIC 成功计算 RSS 哈希值后，驱动程序应将哈希类型、哈希函数和哈希值存储在 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构中，并附带以下宏：

[**网络 \_ 缓冲区 \_ 列表 \_ 集 \_ 哈希 \_ 类型**](/windows-hardware/drivers/ddi/ndis/nf-ndis-net_buffer_list_set_hash_type)

[**NET \_ BUFFER \_ 列表 \_ 集 \_ 哈希 \_ 函数**](/windows-hardware/drivers/ddi/ndis/nf-ndis-net_buffer_list_set_hash_function)

[**网络 \_ 缓冲区 \_ 列表 \_ 集的 \_ 哈希 \_ 值**](/windows-hardware/drivers/ddi/ndis/nf-ndis-net_buffer_list_set_hash_value)

哈希类型标识已接收的数据包中应计算哈希值的区域。 有关哈希类型的详细信息，请参阅 [RSS 哈希类型](rss-hashing-types.md)。 哈希函数标识用于计算哈希值的函数。 有关哈希函数的详细信息，请参阅 [RSS 哈希函数](rss-hashing-functions.md)。 协议驱动程序在初始化时选择哈希类型和函数。 有关详细信息，请参阅 [RSS 配置](rss-configuration.md)。

如果 NIC 找不到哈希类型指定的数据包区域，则不应执行任何哈希计算或缩放。 在这种情况下，微型端口驱动程序或 NIC 应该将接收的数据分配给默认 CPU。

如果 NIC 用尽接收缓冲区，则必须在原始接收 DPC 返回后立即返回每个缓冲区。 微型端口驱动程序可以指示收到的数据，状态为 NDIS \_ 状态 \_ 资源。 在这种情况下，过量驱动程序必须通过慢速路径来复制缓冲区描述符，并立即放弃原始副本的所有权。

有关接收网络数据的详细信息，请参阅 [接收网络数据](receiving-network-data.md)。

 

