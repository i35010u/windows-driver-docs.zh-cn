---
title: 指示 RSS 接收数据
description: 指示 RSS 接收数据
ms.assetid: 8d040d7d-3a8a-4d81-8508-8de225e000ab
keywords:
- 接收方缩放 WDK 网络，指示接收数据
- RSS WDK 网络，指示接收数据
- 指示接收数据 WDK RSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 77d44d54c6165e6440949c8b133292f5f3587fb0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824611"
---
# <a name="indicating-rss-receive-data"></a>指示 RSS 接收数据





微型端口驱动程序通过从其[*MiniportInterruptDPC*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_interrupt_dpc)函数调用[**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists)函数来指示收到的数据。

NIC 成功计算 RSS 哈希值后，驱动程序应将[**NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)中的哈希类型、哈希函数和哈希值存储在下面的宏\_列表结构中：

[**NET\_缓冲区\_列表\_集\_哈希\_类型**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-set-hash-type)

[**NET\_缓冲区\_列表\_集\_哈希\_函数**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-set-hash-function)

[**NET\_缓冲区\_列表\_设置\_哈希\_值**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-set-hash-value)

哈希类型标识已接收的数据包中应计算哈希值的区域。 有关哈希类型的详细信息，请参阅[RSS 哈希类型](rss-hashing-types.md)。 哈希函数标识用于计算哈希值的函数。 有关哈希函数的详细信息，请参阅[RSS 哈希函数](rss-hashing-functions.md)。 协议驱动程序在初始化时选择哈希类型和函数。 有关详细信息，请参阅[RSS 配置](rss-configuration.md)。

如果 NIC 找不到哈希类型指定的数据包区域，则不应执行任何哈希计算或缩放。 在这种情况下，微型端口驱动程序或 NIC 应该将接收的数据分配给默认 CPU。

如果 NIC 用尽接收缓冲区，则必须在原始接收 DPC 返回后立即返回每个缓冲区。 微型端口驱动程序可以指示收到的数据，其状态为 NDIS\_状态\_资源。 在这种情况下，过量驱动程序必须通过慢速路径来复制缓冲区描述符，并立即放弃原始副本的所有权。

有关接收网络数据的详细信息，请参阅[接收网络数据](receiving-network-data.md)。

 

 





