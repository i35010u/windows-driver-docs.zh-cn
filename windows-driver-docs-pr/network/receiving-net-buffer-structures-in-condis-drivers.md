---
title: 在 CoNDIS 驱动程序中接收 NET_BUFFER 结构
description: 在 CoNDIS 驱动程序中接收 NET_BUFFER 结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 233fdc93983682928344eb0d9862340227ef131e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782197"
---
# <a name="receiving-net_buffer-structures-in-condis-drivers"></a>\_在 CoNDIS 驱动程序中接收网络缓冲区结构





下图说明了一个基本 CoNDIS 接收操作，该操作涉及一个协议驱动程序、NDIS 和一个微型端口驱动程序。

![说明基本 condis 接收操作（涉及协议驱动程序、ndis 和微型端口驱动程序）的示意图](images/netbuffercoreceive.png)

如上图所示，微型端口驱动程序调用 [**NdisMCoIndicateReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatereceivenetbufferlists) 函数，以便向过量驱动程序指示 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer) 结构。 在大多数微型端口驱动程序中，每个网络 \_ 缓冲区结构都附加到单独的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构，因此协议驱动程序可以创建网络缓冲区列表结构的原始列表的子集 \_ \_ ，并将其转发到不同的客户端。 但是， \_ 附加到网络缓冲区列表的网络缓冲区的数量 \_ \_ 取决于驱动程序。

当微型端口驱动程序链接了所有网络 \_ 缓冲区 \_ 列表结构后，微型端口驱动程序会将指向列表中第一个网络 \_ 缓冲区列表结构的指针传递 \_ 到 **NdisMCoIndicateReceiveNetBufferLists** 函数。 NDIS 检查网络 \_ 缓冲区 \_ 列表结构，并调用与指定虚拟连接 (VC) 相关联的协议驱动程序的 [**ProtocolCoReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_receive_net_buffer_lists) 函数。 NDIS 传递列表的一个子集，该子集只包含 \_ \_ 与每个协议驱动程序的正确绑定关联的网络缓冲区列表结构。

如果在 \_ \_ \_ \_ *CoReceiveFlags* 参数中为协议驱动程序的 *ProtocolCoReceiveNetBufferLists* 函数设置了 ndis 接收标志状态资源标志，则在 *ProtocolCoReceiveNetBufferLists* 返回后，ndis 会立即重新获得 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构的所有权。

如果 \_ \_ \_ \_ 未在 *CoReceiveFlags* 参数中为协议驱动程序的 [**ProtocolCoReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_receive_net_buffer_lists) 函数设置 NDIS 接收标志状态资源标志，则协议驱动程序可以保留网络 \_ 缓冲区列表结构的所有权 \_ 。 在这种情况下，协议驱动程序必须 \_ \_ 通过调用 [**NdisReturnNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreturnnetbufferlists) 函数来返回网络缓冲区列表结构。

如果微型端口驱动程序在接收资源上运行较少，则可以 \_ \_ \_ \_ 在 [**NdisMCoIndicateReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatereceivenetbufferlists)函数的 *CoReceiveFlags* 参数中设置 NDIS 接收标志状态资源标志。 在这种情况下，只要 **NdisMCoIndicateReceiveNetBufferLists** 返回，驱动程序就可以回收所有指定的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构和嵌入的 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构的所有权。 如果微型端口驱动程序指示 \_ 设置了 NDIS \_ 接收标志资源标志的网络缓冲区结构 \_ \_ ，则协议驱动程序必须复制数据，因此应避免 \_ \_ \_ 以这种方式使用 NDIS 接收标记资源。 微型端口驱动程序应检测其接收资源不足的情况，并应完成避免此情况所需的任何步骤。

在协议驱动程序调用 **NdisReturnNetBufferLists** 后，NDIS 调用微型端口驱动程序的 [*MiniportReturnNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_return_net_buffer_lists)函数。

**注意**  如果微型端口驱动程序指示具有给定状态的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构，则不需要 NDIS 来向 \_ \_ 具有相同状态的过量驱动程序指示网络缓冲区列表结构。 例如，NDIS 可以 \_ \_ 使用 ndis 接收标志资源标志来复制网络缓冲区列表结构 \_ \_ \_ ，并通过清除此标志指示复制到过量驱动程序。

 

NDIS 可以按任意 \_ \_ 顺序和任意组合将网络缓冲区列表结构返回到微型端口驱动程序。 也就是说， \_ \_ 通过调用 [*MiniportReturnNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_return_net_buffer_lists) ，NDIS 返回到微型端口驱动程序的网络缓冲区列表结构的链接列表可以具有 \_ \_ 来自以前调用 [**NdisMCoIndicateReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatereceivenetbufferlists)的网络缓冲区列表结构。

微型端口驱动程序必须将 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构中的 **SourceHandle** 成员设置为与 **NdisMCoIndicateReceiveNetBufferLists** 的 *NdisVcHandle* 参数相同的值。 因此，NDIS 可以将网络 \_ 缓冲区 \_ 列表结构返回到正确的微型端口驱动程序。

中间驱动程序还将网络缓冲区列表结构中的 **SourceHandle** 成员设置 \_ \_ 为 *NdisVcHandle* 值。 如果中间驱动程序转发接收指示，则驱动程序必须保存基础驱动程序在写入 **SourceHandle** 成员之前提供的 **SourceHandle** 值。 当 NDIS \_ \_ 向中间驱动程序返回已转发的网络缓冲区列表结构时，中间驱动程序必须还原它保存的 **SourceHandle** 。

 

