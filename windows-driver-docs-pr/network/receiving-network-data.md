---
title: 接收网络数据
description: 接收网络数据
ms.assetid: d929c956-73dc-433f-9e60-bc3f8e0bcc14
keywords:
- 网络数据 WDK，接收
- 数据 WDK 网络，接收
- 包 WDK 网络，接收
- 返回数据 WDK 网络
- 网络数据 WDK，返回
- 数据 WDK 网络，返回
- 包 WDK 网络，返回
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3aba9cb30d3f10d9731c1e5b240616278db06099
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216942"
---
# <a name="receiving-network-data"></a>接收网络数据





下图说明了一个基本的接收操作，该操作涉及微型端口驱动程序、NDIS 和协议驱动程序。

![阐释基本接收操作的关系图](images/netbufferreceive.png)

微型端口驱动程序调用 [**NdisMIndicateReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatereceivenetbufferlists) 函数，以指示更高级别驱动程序的 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer) 结构。 通常，每个网络 \_ 缓冲区结构都应附加到单独的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构。 这允许协议驱动程序创建网络缓冲区列表结构的原始列表的 \_ 子集 \_ ，并将其转发给不同的客户端。 某些驱动程序（例如本机 IEEE 802.11 微型端口驱动程序）可能会将多个网络 \_ 缓冲区结构附加到网络 \_ 缓冲区 \_ 列表结构。

链接所有网络 \_ 缓冲区 \_ 列表结构后，微型端口驱动程序将指向列表中第一个网络 \_ 缓冲区 \_ 列表结构的指针传递到 **NdisMIndicateReceiveNetBufferLists** 函数。 NDIS 检查网络 \_ 缓冲区 \_ 列表结构，并调用与网络[**ProtocolReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_receive_net_buffer_lists) \_ 缓冲区列表结构关联的每个协议驱动程序的 ProtocolReceiveNetBufferLists 函数 \_ 。 NDIS 传递列表的一个子集，该子集只包含 \_ \_ 与每个协议驱动程序的正确绑定关联的网络缓冲区列表结构。 NDIS 将网络缓冲区列表结构中指定的 **NetBufferListFrameType** 值 \_ 与 \_ 每个协议驱动程序注册的帧类型相匹配。

如果设置了 \_ \_ \_ 传递到协议驱动程序的*ProtocolReceiveNetBufferLists*函数的*ReceiveFlags*参数中的 NDIS 接收标志资源标志，则在*ProtocolReceiveNetBufferLists*调用返回后，ndis 会立即重新获取[**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构的所有权。

**注意**   如果设置了 NDIS \_ 接收 \_ 标志 \_ 资源标志，则协议驱动程序必须在链接列表中保留一组原始的网络 \_ 缓冲区 \_ 列表结构。 例如，当设置此标志时，驱动程序可能会处理这些结构，并一次一个地指示其堆栈，但在函数返回之前，必须还原原始链接列表。

 

如果 \_ \_ \_ 未设置传递给协议驱动程序的*ProtocolReceiveNetBufferLists*函数的*ReceiveFlags*参数中的 NDIS 接收标志资源标志，则协议驱动程序可以保留网络 \_ 缓冲区 \_ 列表结构的所有权。 在这种情况下，协议驱动程序必须 \_ \_ 通过调用 [**NdisReturnNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreturnnetbufferlists) 函数来返回网络缓冲区列表结构。

如果微型端口驱动程序在接收资源上运行较低，则可以在调用 NdisMIndicateReceiveNetBufferLists 时，在 ReceiveFlags 参数中设置 NDIS \_ 接收 \_ 标志 \_ 资源标志。 *ReceiveFlags* **NdisMIndicateReceiveNetBufferLists** 在这种情况下，只要**NdisMIndicateReceiveNetBufferLists**返回，驱动程序就可以回收所有指定的[**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构和嵌入的[**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构的所有权。 指示 \_ 设置了包含 NDIS 接收标志资源标志的网络缓冲区结构将 \_ \_ \_ 强制协议驱动程序复制数据，因此应避免这样做。 微型端口驱动程序应检测即将用完接收资源的时间，并采取必要的步骤来避免这种情况。

在协议驱动程序调用**NdisReturnNetBufferLists**后，NDIS 调用微型端口驱动程序的[*MiniportReturnNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_return_net_buffer_lists)函数。

**注意**   如果微型端口驱动程序指示 \_ 设置了 \_ NDIS 接收标志资源标志的网络缓冲区列表结构 \_ ，则 \_ \_ 并不意味着 ndis 将 \_ \_ 向具有相同状态的协议驱动程序指示网络缓冲区列表结构。 例如，NDIS 可以 \_ \_ 使用 ndis 接收标志资源标志来复制网络缓冲区列表结构， \_ 并在清除了标志的情况下 \_ \_ 指出向协议驱动程序复制。

 

NDIS 可以按任意顺序和任意组合将 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构返回到微型端口驱动程序。 也就是说， \_ \_ 通过调用 *MiniportReturnNetBufferLists* 函数返回给微型端口驱动程序的网络缓冲区列表结构的链接列表，可以具有 \_ \_ 来自以前对 **NdisMIndicateReceiveNetBufferLists**的不同调用的网络缓冲区列表结构。

微型端口驱动程序应将 NET BUFFER LIST 结构中的 **SourceHandle** 成员设置 \_ \_ 为 *MiniportAdapterHandle* ，NDIS 在 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数中提供给微型端口驱动程序。 筛选器驱动程序必须将筛选器驱动程序发出的每个网络缓冲区列表结构的**SourceHandle**成员设置为该筛选器 \_ \_ 驱动程序的 NdisFilterHandle，该结构由 NDIS 在[*FilterAttach*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)函数中提供给筛选器驱动程序的**NdisFilterHandle** 。 筛选器驱动程序不能**SourceHandle**修改任何 \_ \_ 不由筛选器驱动程序生成的网络缓冲区列表结构中的 SourceHandle 成员。

中间驱动程序还将 NET BUFFER LIST 结构中的 **SourceHandle** 成员设置 \_ \_ 为 *MiniportAdapterHandle* 值，NDIS 在 *MiniportInitializeEx* 函数中提供给中间驱动程序。 如果中间驱动程序转发接收指示，则驱动程序必须保存基础驱动程序在写入**SourceHandle**成员之前提供的**SourceHandle**值。 当 NDIS \_ \_ 向中间驱动程序返回已转发的网络缓冲区列表结构时，中间驱动程序必须还原它保存的 **SourceHandle** 。

 

